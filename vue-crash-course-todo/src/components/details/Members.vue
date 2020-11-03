<template>
  <div>
    <div v-bind:key="member.id" v-for="member in members">
      <MemberItem
        v-bind:member="member"
        v-on:del-member="$emit('del-member', member.id)"
      />
    </div>
  </div>
</template>

<script>
import MemberItem from "./MemberItem.vue";

export default {
  name: "Members",
  props: ["members"],
  components: {
    MemberItem,
  },
};
</script>

<style scoped>
/*scoped means that this style is just for this component*/
</style>