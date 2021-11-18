<template>
  <div class="kittens-edit">
    <form v-on:submit.prevent="submit()">
      <h1>Kitten edit</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="editKittenParams.name" />
      </div>
      <div>
        <label>Breed:</label>
        <input type="text" v-model="editKittenParams.breed" />
      </div>
      <div>
        <label>Age:</label>
        <input type="text" v-model="editKittenParams.age" />
      </div>
      <div>
        <label>Images:</label>
        <input type="text" v-model="editKittenParams.image" />
      </div>   
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      editKittenParams: {},
      errors: []
    };
  },
  methods: {
    submit: function () {
      axios
        .patch("/kittens/" + this.$route.params.id, this.editKittenParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    getKitten: function() {
      axios.get("/kittens/" + this.$route.params.id).then(response => {
        console.log(response.data);
        this.editKittenParams = response.data;
      });      
    }
  },
  created: function() {
    this.getKitten();
  }
};