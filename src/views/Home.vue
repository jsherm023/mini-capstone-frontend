<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div class="container">
      <div class="row">
        <div class="col-sm-4" v-for="product in products">
          <div class="card" style="width: 18rem;">
            <div class="card-body">
              <h5 class="card-title">Name: {{ product.name }}</h5>
              <h6 class="card-subtitle mb-2 text-muted">Price: {{ product.price }}</h6>
              <p class="card-text">Descsription: {{ product.description }}</p>
              <a href="#" class="card-link">Card link</a>
              <a href="#" class="card-link">Another link</a>
            </div>
          </div>
        </div>
      </div>
    </div>
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