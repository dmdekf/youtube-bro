<template>
  <div class="search-bar">
    <input @keypress.enter="onInput" />
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  methods: {
    onInput(event) {
      //emit 1. 부모에게 커스텀 이벤트를 준다.
      this.$emit("input-change", event.target.value);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div.search-bar {
  text-align: center;
  margin: 20px;
}

div.search-bar > input {
  width: 75%;
}
</style>
