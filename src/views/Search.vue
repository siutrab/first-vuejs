<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search:</label>
      <input id="searh" type="text" name="search" v-model="searchValue" @input="inputHandler">
    </div>
    <ul>
      <li v-for="item in results" :key="item.data[0].nasa_id">
        <p>{{item.data[0].description}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
//Axios is an request menager
import axios from "axios";

// debounce is an method from lodash bibliotec.
// debounce func. activates some block of code after
// there is no events noticed for given time
import debounce from "lodash.debounce";

//Api handling
const API = "http://images-api.nasa.gov/search";

export default {
  name: "Search",
  data() {
    return {
      searchValue:
        "" /*v-model jest obsługiwany poprzez funkcję zwracającą wartość v-modelu*/,

      results: []
    };
  },

  methods: {
    inputHandler: debounce(function() {
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(response => {
          this.results = response.data.collection.items;
          console.log(this.results);
        })
        .catch(error => {
          console.log(error);
        });
    }, 500)
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
