<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div class="container">
      <div class="row">
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
</template>

<style>
</style>

<script>
var axios = require('axios');
export default {
  data: function() {
    return {
      message: "Welcome to the show component!",
      name: "",
      price: "",
      description: "",
      product: [],
    };
  },
  created: function() {
    axios.get('http://localhost:3000/api/products' + this.$route.params.id).then(response =>{
      console.log(response.data);
      this.product = response.data;
      })
  },
  methods: {},
  computed: {}
};
</script>