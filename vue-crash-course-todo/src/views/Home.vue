<template>
  <div id="app">
    <addImmobile v-on:add-immobile="addImmobile" />
    <Immobiles v-bind:immobiles="immobiles" />
  </div>
</template>

<script>
import Immobiles from "../components/immobiles.vue";
import addImmobile from "../components/addImmobile.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Immobiles,
    addImmobile,
  },
  data() {
    return {
      immobiles: [],
    };
  },
  methods: {
    deleteImmobile(id) {
      //IMMOBILE NAO SE DELETA
      axios
        .get(`http://homologacao.sistemaeris.com.br:84/immobiles/${id}`) //details
        .then(
          (this.immobiles = this.immobiles.filter(
            (immobile) => immobile.id !== id
          ))
        ) //atualiza a ui
        .catch((err) => console.log(err));
    },
    addImmobile(newImmobile) {
      const { address, number } = newImmobile;

      axios
        .post("http://homologacao.sistemaeris.com.br:84/immobiles", {
          address,
          number,
        }) // it posts then updates the ui
        .then((res) => (this.immobiles = [...this.immobiles, res.data]))
        .catch((err) => console.log(err));
      console.log("immobiles refreshed");
    },
  },
  created() {
    axios
      .get("http://homologacao.sistemaeris.com.br:84/immobiles")
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
