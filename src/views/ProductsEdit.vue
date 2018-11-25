<template>
  <div class="Edit">
    <div class="container">
      <form>
        <h1>Edit</h1>
        <ul>
        </ul>
        <div class="form-group">
          <label>name:</label> 
          <input type="text" class="form-control" v-model="name">
        </div>
        <div class="form-group">
          <label>description:</label>
          <input type="text" class="form-control" v-model="description">
        </div>
        <div class="form-group">
          <label>price:</label>
          <input type="text" class="form-control" v-model="price">
        </div>
        <input type="submit" class="btn btn-primary" value="Submit">
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Edit your product!",
      name: "",
      price: "",
      description: "",
      product: [],
    };
  },
  created: function() {
    axios.patch('http://localhost:3000/api/products/' + this.$route.params.id).then(response =>{
      console.log(response.data);
      this.product = response.data;
      })
  },
  methods: {},
  computed: {}
};
</script>