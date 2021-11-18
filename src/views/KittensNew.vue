<template>
  <div class="Create - Kitten">
    <form v-on:submit.prevent="submit()">
      <h1>Make Kitten</h1>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newKittenParams.name" />
      </div>
      <div>
        <label>Breed:</label>
        <input type="breed" v-model="newKittenParams.breed" />
      </div>
      <div>
        <label>Age:</label>
        <input type="Age" v-model="newKittenParams.age" />
      </div>
      <div>
        <label>Image</label>
        <input type="Age" v-model="newKittenParams.image" />
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
      newKittenParams: {},
    };
  },
  methods: {
    submit: function () {
      axios.post("/kittens", this.newKittenParams).then((response) => {
        console.log(response.data);
        this.$router.push("/");
      });
    },
  },
};
</script>
