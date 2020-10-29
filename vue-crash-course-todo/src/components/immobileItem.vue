<template>
  <div
    class="immobile-item"
    v-bind:class="{ 'is-complete': immobile.completed }"
  >
    <p>
      {{ immobile.address }}, {{ immobile.number }}
      <button @click="$emit('del-immobile', immobile.id)" class="del">x</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "ImmobileItem",
  props: ["immobile"],
  /*methods: {
    markComplete() {
      console.log("marked as completed");
      this.immobile.completed = !this.immobile.completed;
    },
  },*/
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
.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>