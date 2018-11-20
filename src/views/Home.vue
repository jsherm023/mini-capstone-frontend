<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p v-for="product in products"> {{product.name}}</p>
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      products: [],
    };
  },
  created: function() {
    axios.get('http://localhost:3000/api/products').then(function(response) {
      console.log(response.data);
      this.products = response.data;
      }.bind(this))
  },
  methods: {},
  computed: {}
};
</script>