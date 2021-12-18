<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <hr />
    <hr />
    <div v-for="kitten in kittens">
      <h2>{{ kitten.name }}</h2>
      <router-link v-bind:to="`kittens/${kitten.id}`">
        <img v-bind:src="kitten.image" />
      </router-link>
      <hr />
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "------KITTENS------",
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
