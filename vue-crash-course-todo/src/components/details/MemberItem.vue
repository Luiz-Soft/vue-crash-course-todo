<template>
  <div class="member-item">
    <p>
      <strong>Name:</strong>{{ this.member.name }}, <strong>Birthday:</strong
      >{{ this.member.age }}, <strong>Gender:</strong>{{ this.member.gender }}

      <button @click="$emit('del-member', member.id)" class="del">❌</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "MemberItem",
  props: ["member"],
  components: {},
};
</script>

<style scoped>
.member-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
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