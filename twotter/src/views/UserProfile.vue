<template>
  <div class="user-profile">
    <div class="user-profile-wrapper">
      <div class="user-profile-user-panel">
        <h1 class="user-profile-suername">@{{ state.user.username  }} </h1>
        <div class="user-profile-admin-badge" v-if="state.user.isAdmin">Admin</div>
        <div class="suer-profile-follower-count">
          <strong> Followers: </strong> {{ state.follower}}
        </div>
      </div>
        <createTwootPanel 
        :user="user" 
        @addTwoot = "createTwootFromChild"
        />
    </div>

    <div class="user-profile-twoots-wrapper">
      <TwootItem
        v-for="twoot in state.user.twoots"
        :key="twoot.id"
        :username="state.user.username"
        :twoot="twoot" 
      />
    </div>
  </div>
</template>

<script>
import {reactive ,computed} from "vue";
import {useRoute} from "vue-router"
import TwootItem from "../components/TwootItem";
import createTwootPanel from "../components/createTwootPanel.vue";
import {users} from "../assets/users"

export default {
  name: "UserProfile",
  components: { TwootItem, createTwootPanel },
  setup (){
    const route = useRoute();
    const userId = computed(()=>
    route.params.userId

    ) 


    const state = reactive({
     isloading: false,
     follower : userId.value,
      user: users[userId.value -1] || users[0]
    })
    function createTwootFromChild(textField){
        state.user.twoots.push({
       id:state.user.length +1,
       content : textField
     })
    }
    return {
      state,
      createTwootFromChild,
      userId 
       
    }
  }

};
</script>


<style lang="scss" scoped>
.--exceed .new-twoot {
  color: red;
}
.--exceed .submit-buttone:hover {
  color: #dddddd;
  background-color: red;
}
.user-profile {
  display: flex;
  justify-content: space-around;
  padding: 10px;

  .user-profile-wrapper {
    /* width: 50%; */
    .user-profile-user-panel {
      display: flex;
      flex-direction: column;
      position: relative;
      padding: 5px;
      text-decoration: none;
      background-color: white;
      border-radius: 4px;
      box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
      transition: all 0.3s;
      &:hover {
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19),
          0 6px 6px rgba(0, 0, 0, 0.23);
      }

    }
  }
}

// ---------------------------

.user-profile-twoots-wrapper {
  display: flex;
  flex-direction: column;
  position: relative;
  width: 50%;
}

.suer-profile-follower-count {
  display: flex;
  justify-content: start;
  margin-bottom: 5px;
}
.user-profile-create-twoot {
  display: flex;
  flex-direction: column;
  align-content: space-around;
  justify-content: stretch;
}
.user-profile-create-twoot-type {
  display: flex;
  justify-content: start;
  padding: 5px;
}
.twoot-type {
  margin-right: 5px;
}
.submit-buttone {
  text-align: center;
  display: inline-block;
  padding: 0.5em 3em;
  border: 0.16em solid #ffffff;
  margin: 0 0.3em 0.3em 0;
  transition: all 0.3s;
  border-radius: 5px;
}
.submit-buttone:hover {
  color: #dddddd;
  background-color: teal;
}
.new-twoot {
  display: flex;
  justify-content: start;
  align-items: flex-start;
}

.h1 {
  margin: 0;
}
</style>