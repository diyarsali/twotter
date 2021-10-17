// shit + ald +f for formating
<template>
  <div class="createTwootPanel">
    <form
      class="user-profile-create-twoot"
      @submit.prevent="addTwoot()"
      :class="{ '--exceed': newTwootcharacterCounte > 100 }"
    >
      <div class="new-twoot">
        <strong> New twoot</strong> ({{ newTwootcharacterCounte }}/100 )
      </div>
      <textarea v-model="state.newTwootContent" id="newTwoot " rows="4" />
      <div class="user-profile-create-twoot-type">
        <div class="twoot-type"><strong> Twoot Type</strong></div>
        <select id="newTwootType">
          <option
            :value="option.value"
            v-for="(option, index) in state.twootType"
            :key="index"
          >
            {{ option.value }}
          </option>
        </select>
      </div>
      <button class="submit-buttone">submit</button>
      <div class="alert" v-if="state.fillTheGap">{{ state.alertFill }}</div>
    </form>
  </div>
</template>

<script>
import { computed, reactive } from "vue";

export default {
  props: ["user"],
  setup(props, ctx) {
    const state = reactive({
      alertFill: "text box is empty !",
      fillTheGap: false,
      newTwootContent: "",
      selecteTwootType: "instant",
      //   mutableUser:this.user,
      twootType: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "intant Twoot" },
      ],
    });

    const newTwootcharacterCounte = computed(
      () => state.newTwootContent.length
    );
    function addTwoot() {
      if (state.newTwootContent !== "") {
        ctx.emit("addTwoot", state.newTwootContent);
        state.newTwootContent = "";
      } else {
        state.fillTheGap = true;
      }
    }
    return {
      state,
      newTwootcharacterCounte,
      addTwoot,
    };
  },
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

.createTwootPanel {
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
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
  }
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
