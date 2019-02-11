<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search:</label>
      <input id="searh" type="text" name="search" v-model="searchValue" @input="inputHandler">
    </div>
  </div>
</template>

<script>
//Api handling
const API = "http://images-api.nasa.gov";

export default {
  name: "Search",
  data() {
    return {
      searchValue:
        "" /*v-model jest obsługiwany poprzez funkcję zwracającą wartość v-modelu*/
    };
  },
  methods: {
    inputHandler() {
      console.log(this.searchValue);
    }
  }
};
</script>

<style lang="scss" scoped>
* {
  font-family: Arial, Helvetica, sans-serif;
}
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0;
  padding: 30px;
  width: 100%;
}

.search {
  display: flex;
  flex-direction: column;
  width: 300px;
}

input {
  height: 30px;
  border-bottom: 1px solid;
  border-bottom-color: cadetblue;
}
</style>
