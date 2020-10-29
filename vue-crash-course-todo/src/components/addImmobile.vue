<template>
  <div>
    <form @submit="addImmobile">
      <input
        type="text"
        name="address"
        v-model="address"
        placeholder="Adress..."
        required
      />
      <input
        type="number"
        name="number"
        v-model="number"
        placeholder="Number..."
        required
      />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
//import uuid from "uuid";
export default {
  name: "addImmobile",
  data() {
    return {
      address: "",
      number: "",
    };
  },

  methods: {
    addImmobile(e) {
      e.preventDefault(); //it stops the default behavior (sending the immobile to a file) and keeps to follow method

      const newImmobile = {
        address: this.address,
        number: this.number,
      };
      //send to parent
      this.$emit("add-immobile", newImmobile);
      this.address = "";
      this.number = "";

      console.log("Immobile added");
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