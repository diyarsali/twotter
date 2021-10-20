<template>
  <div class="twoot-item">
    <div class="twoot-profile-item">
      <div class="twoot-username">@{{ username }} </div>
      <div class="twoot-content">{{ twoot.content }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwootItem",
  props: {
    username: {
      type: String,
      required: true,
    },
    twoot: {
      type: Object,
      required: true,
    },
    
  },

};
</script>
<style >
.twoot-item {
  display: flex;
  flex-direction: column;
  justify-content: start;
  margin: 10px;
  padding: 10px;
  background-color: #ccffcc;
  border-radius: 5px;
}
.twoot-item:hover{
  background-color: #e6fce6;

}
.twoot-profile-item {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.twoot-username {
  margin: 5px;
  /* padding: 10px; */
}
</style>