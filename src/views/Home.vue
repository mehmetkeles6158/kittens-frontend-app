<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="kitten in kittens">
      <p>{{ kitten.name }}</p>
      <router-link v-bind:to="`kittens/${kitten.id}`">More Info</router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      kittens: [],
    };
  },
  created: function () {
    this.kittensIndex();
  },
  methods: {
    kittensIndex: function () {
      console.log("get all kittens");
      axios.get("/kittens").then((response) => {
        console.log(response.data);
        this.kittens = response.data;
      });
    },
  },
};
</script>
