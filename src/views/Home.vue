<template>
  <div class="home">
    <h1>{{ message }}</h1>
      search by name: <input v-model="nameFilter" list="names">
      <datalist id="names">
        <span v-for="product in products">
          <option>{{ product.name }} </option>
          <option>{{ product.description }} </option>
        </span>
      </datalist>
      <div>
        <button v-on:click="setSortAttribute('name')">Sort by name</button>
        <button v-on:click="setSortAttribute('description')">Sort by description> </button>
      </div>
    <div class="container">
      <div class="row">
        <!-- <div class="col-sm-4" v-for="product in filterBy(products, nameFilter, 'name')"> -->
          <transition-group name="fade">
          <div v-for="product in orderBy(products, sortAttribute, sortAscending)" v-bind:key="product.id">
          <div class="card" style="width: 18rem;">
            <div class="card-body">
              <h5 class="card-title">Name: {{ product.name }}</h5>
              <h6 class="card-subtitle mb-2 text-muted">Price: {{ product.price }}</h6>
               <h6 class="card-subtitle mb-2 text-muted">Id: {{ product.id }}</h6>
              <p class="card-text">Descsription: {{ product.description }}</p>
              <a href="#" class="card-link">Card link</a>
              <a href="#" class="card-link">Another link</a>          
            </div>           
          </div>
        </div>
      </transition-group>
      </div>
    </div>
      <p class="red" v-for="error in errors">{{error}}</p>
      <p>name:<input type="text" v-model="newProduct.name"></p>
      <p>description:<input type="text" v-model="newProduct.description"></p>
      <p>price:<input type="text" v-model="newProduct.price"></p>
      <button v-on:click="addProduct()">add a new product</button> 
  </div>

</template>

<style>
.red {
  color: red;
}
/* Vue.js fade */
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to {
  opacity: 0
}

/* Vue.js slide-right */
.slide-right-enter-active {
  transition: all .3s ease;
}
.slide-right-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-right-enter, .slide-right-leave-to {
  transform: translateX(10px);
  opacity: 0;
}

/* Vue.js slide-left */
.slide-left-enter-active {
  transition: all .3s ease;
}
.slide-left-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-left-enter, .slide-left-leave-to {
  transform: translateX(-10px);
  opacity: 0;
}

</style>

<script>
var axios = require('axios');
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      products: [],
      newProduct: { name: "", description: "", price: ""},
      errors: [],
      nameFilter: "",
      sortAttribute:  "name",
      sortAscending: 1
    };
  },
  created: function() {
    axios.get('http://localhost:3000/api/products').then(function(response) {
      console.log(response.data);
      this.products = response.data;
      }.bind(this))
  },
  // setSortAttribute: function(inputAttribute) {
  //   this.sortAttribute = inputAttribute;
  // },
  methods: {
    addProduct: function() {
      var params = {
        name: this.newProduct.name,
        description: this.newProduct.description,
        price: this.newProduct.price
      }
      axios.post('http://localhost:3000/api/products', params).then(function(response) {
        console.log(response.data);
        this.errors = [];
      }.bind(this)).catch(function(errors) {
        console.log('in the .catch function');
        console.log(errors.response);
        this.errors = errors.response.data.errors;
      }.bind(this))
      console.log('add the person');

    },
    setSortAttribute: function(inputAttribute) {
      if (this.sortAttribute === inputAttribute) {
        this.sortAscending *= -1;
      } else {
        this.sortAttribute = inputAttribute;       
      }
    },
  },
  computed: {}
};
</script>