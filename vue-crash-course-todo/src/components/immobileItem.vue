<template>
  <div
    class="immobile-item"
    v-bind:class="{ 'is-complete': immobile.completed }"
  >
    <p>
      {{ immobile.address }}, {{ immobile.number }}
      <router-link
        v-bind:to="{ path: 'detail', query: { id: this.immobile.id } }"
      >
        <button class="details" @click="getDetails">🔎</button></router-link
      >
    </p>
  </div>
</template>

<script>
//import ImmobileDetails from "./immobileDetails.vue";
import axios from "axios";
export default {
  name: "ImmobileItem",
  props: ["immobile"],
  components: {
    //   ImmobileDetails,
  },
  methods: {
    getDetails() {
      axios
        .get(
          `http://homologacao.sistemaeris.com.br:84/immobiles/${this.immobile.id}`
        )
        .then((res) => (this.members = res.data))
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style scoped>
.immobile-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.details {
  background: #00ccff;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>