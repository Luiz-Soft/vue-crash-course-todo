<template>
  <div class="about">
    <addMember v-on:add-member="addMember" />
    <Members v-bind:members="members.members" v-on:del-member="deleteMember" />
  </div>
</template>

<script>
//import immobileItem from "../components/immobileItem.vue"
import addMember from "../components/details/addMember.vue";
import Members from "../components/details/Members";
import axios from "axios";
export default {
  name: "App",
  components: {
    Members,
    addMember,
  },
  data() {
    return {
      members: [],
    };
  },
  methods: {
    deleteMember(id) {
      console.log(id);
      console.log("Requisicao delete não funciona");
      axios
        .delete(
          `http://homologacao.sistemaeris.com.br:84/immobiles/${this.$route.query.id}/members/${id}`
        ) //details
        .then(
          (this.members.members = this.members.members.filter(
            (members) => members.members.id !== id
          ))
        ) //atualiza a ui
        .catch((err) => console.log(err));
    },
    addMember(newMember) {
      const { name, age, gender } = newMember;

      axios
        .post(
          `http://homologacao.sistemaeris.com.br:84/immobiles/${this.$route.query.id}/members`,
          {
            name,
            age,
            gender,
          }
        ) // it posts then updates the ui
        .then(
          (res) => (this.members.members = [...this.members.members, res.data])
        )
        .catch((err) => console.log(err));
      console.log("immobiles refreshed");
    },
  },
  created() {
    axios
      .get(
        `http://homologacao.sistemaeris.com.br:84/immobiles/${this.$route.query.id}`
      )
      .then((res) => (this.members = res.data))
      .catch((err) => console.log(err));
  },
};
</script>
