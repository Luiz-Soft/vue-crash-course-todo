<template>
  <div>
    <form @submit="addMember">
      <input
        type="text"
        name="Name"
        v-model="name"
        placeholder="Name..."
        required
      />
      <input
        type="date"
        name="age"
        v-model="age"
        value="1990-07-22"
        min="1900-01-01"
        required
      />
      <label for="genders">Gender</label>
      <select v-model="gender" name="gender">
        <option name="gender" value="MASCULINO">MASCULINO</option>
        <option name="gender" value="FEMININO">FEMININO</option>
      </select>
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
//import uuid from "uuid";
export default {
  name: "addMember",
  data() {
    return {
      name: "",
      age: "",
      gender: "",
    };
  },

  methods: {
    addMember(e) {
      e.preventDefault(); //it stops the default behavior (sending the member to a file) and keeps to follow method

      const newMember = {
        name: this.name,
        age: this.age,
        gender: this.gender,
      };
      //send to parent
      this.$emit("add-member", newMember);
      this.name = "";
      this.age = "";
      this.gender = "";

      console.log("Member added");
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