<template>
  <div>
    <div v-bind:key="immobile.id" v-for="immobile in immobiles">
      <ImmobileItem
        v-bind:immobile="immobile"
        v-on:del-immobile="$emit('del-immobile', immobile.id)"
      />
    </div>
  </div>
</template>

<script>
import ImmobileItem from "./immobileItem.vue";

export default {
  name: "Immobiles",
  props: ["immobiles"],
  components: {
    ImmobileItem,
  },
};
</script>

<style scoped>
/*scoped means that this style is just for this component*/
</style>