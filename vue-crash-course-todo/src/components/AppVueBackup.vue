<template>
  <div id="app">
    <Header />
    <addImmobile v-on:add-immobile="addImmobile" />
    <Immobiles
      v-bind:immobiles="immobiles"
      v-on:del-immobile="deleteImmobile"
    />
  </div>
</template>

<script>
import Header from "./components/layout/header.vue";
import Immobiles from "./components/immobiles.vue";
import addImmobile from "./components/addImmobile.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Immobiles,
    Header,
    addImmobile,
  },
  data() {
    return {
      immobiles: [],
    };
  },
  methods: {
    deleteImmobile(id) {
      axios
        .delete(`http://jsonplaceholder.typicode.com/immobiles/${id}`) //deleta
        .then(
          (this.immobiles = this.immobiles.filter(
            (immobile) => immobile.id !== id
          ))
        ) //atualiza a ui
        .catch((err) => console.log(err));
    },
    addImmobile(newImmobile) {
      const { title, completed } = newImmobile;

      axios
        .post("http://jsonplaceholder.typicode.com/immobiles", {
          title,
          completed,
        }) // it posts then updates the ui
        .then((res) => (this.immobiles = [...this.immobiles, res.data]))
        .catch((err) => console.log(err));
    },
  },
  created() {
    axios
      .get("http://jsonplaceholder.typicode.com/immobiles?_limit=5")
      .then((res) => (this.immobiles = res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
