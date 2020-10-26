<template>
  <div>
    <form @submit="addTodo">
      <input
        type="text"
        name="title"
        v-model="title"
        placeholder="Add Todo..."
      />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
import uuid from "uuid";
export default {
  name: "addTodo",
  data() {
    return {
      title: "",
    };
  },

  methods: {
    addTodo(e) {
      console.log(this.title);
      e.preventDefault(); //it stops the default behavior (sending the todo to a file) and keeps to follow method

      const newTodo = {
        id: uuid.v4(),
        title: this.title,
        completed: false,
      };
      //send to parent
      this.$emit("add-todo", newTodo);
      this.title = "";
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 5px;
}
input[type="submit"] {
  flex: 2;
}
</style>