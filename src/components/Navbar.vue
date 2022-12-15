<template>
  <nav class="navbar navbar-expand-lg navbar-light">
    <div class="container ">
      <a class="navbar-brand" href="/">Food Court</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" to="/"> Home </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/Foods"> Foods </router-link>
          </li>
        </ul>

        <ul class="navbar-nav ml-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" to="/Keranjang">
            Cart 
            <b-icon-bag></b-icon-bag>
            <span class="badge badge-primary ml-2"> {{ updateKeranjang ? updateKeranjang.length : banyaks.length }} </span>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from "axios";

export default {
  name: "compNavbar",
  data (){
    return {
      banyaks:[]
    }
  },
  props:['updateKeranjang'],
  methods: {
    setBanyak(data){
      this.banyaks = data
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setBanyak(response.data))
      .catch((error) => console.log(error))
      
  },
};
</script>

<style>
</style>