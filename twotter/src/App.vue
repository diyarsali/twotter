<template>
  <div id="app">
    <nav>
      <div class="navagation_logo">
        <router-link to="/"> Twooter</router-link>
      </div>
      <div class="navigation_user" v-if="user">@{{ user.username }}</div>
    </nav>
    <router-view />
  </div>
</template>
<script>
import { useStore } from "vuex";
import { computed } from "vue";
export default {
  name: "App",
  setup() {
    const store = useStore();
    const user = computed(() => store.state.User.user);
    return {
      user,
    };
    
  },
};
</script>
<style lang="scss">
.navagation_logo a {
  color: white;
  text-decoration: none;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 5%;
    color: white;
    background-color: deeppink;

    .navigation_logo {
      font-weight: bold;
      font-size: 24px;
    }
    .navigatio_user {
      font-weight: bold;
    }
  }
}
</style>
