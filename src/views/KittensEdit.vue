<template>
  <div class="Create - Kitten">
    <form v-on:submit.prevent="submit()">
      <h1>Edit Kitten</h1>
      <div>
        <label>Name:</label>
        <input type="text" v-model="editKittenParams.name" />
      </div>
      <div>
        <label>Breed:</label>
        <input type="breed" v-model="editKittenParams.breed" />
      </div>
      <div>
        <label>Age:</label>
        <input type="Age" v-model="editKittenParams.age" />
      </div>
      <div>
        <label>Image</label>
        <input type="Age" v-model="editKittenParams.image" />
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
    };
  },
  created: function () {
    this.getKitten();
  },
  methods: {
    submit: function () {
      axios.patch("/kittens/" + this.$route.params.id, this.editKittenParams).then((response) => {
        console.log(response.data);
        this.$router.push("/kittens");
      });
    },
    getKitten: function () {
      axios.get(`/kittens/${this.$route.params.id}`).then((response) => {
        console.log(response.data);
        this.editKittenParams = response.data;
      });
    },
  },
};
</script>
