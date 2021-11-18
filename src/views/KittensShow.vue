<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>
      <b>Name:</b>
      {{ kitten.name }}
    </p>
    <p>
      <b>Breed:</b>
      {{ kitten.breed }}
    </p>
    <p>
      <b>Age:</b>
      {{ kitten.age }}
    </p>
    <p>
      <b>Image:</b>
      {{ kitten.image }}
    </p>
    <p><router-link v-bind:to="`/kittens/${kitten.id}/edit`">Edit kitten</router-link></p>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Show",
      kitten: {},
    };
  },
  created: function () {
    this.getKitten();
  },
  methods: {
    getKitten: function () {
      console.log("get kitten");
      axios.get(`/kittens/${this.$route.params.id}`).then((response) => {
        console.log(response.data);
        this.kitten = response.data;
      });
    },
  },
};
</script>
