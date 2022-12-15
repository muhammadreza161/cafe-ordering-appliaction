<template>
  <div class="food-details">
    <Navbar />
    <div class="container">
      <!-- breadcrumb -->
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <router-link to="/" class="breadcrumb-item text-dark">
                Home
              </router-link>
              <router-link to="/foods" class="breadcrumb-item text-dark">
                Foods
              </router-link>
              <li class="breadcrumb-item active" aria-current="page">
                Food Order
              </li>
            </ol>
          </nav>
        </div>
      </div>
      
      <div class="row mt-3">
        <div class="col-md-6">
          <img
            :src="'../assets/images/' + product.gambar"
            class="img-fluid shadow"
            style="border-radius: 10px"
          />
        </div>
        <div class="col">
          <h3>
            <b> {{ product.nama }} </b>
          </h3>
          <hr />
          <h4>
            Harga : <b>Rp. {{ product.harga }} </b>
            <form class="mt-4" v-on:submit.prevent>
              <div class="form-group">
                <label for="banyak"> amount </label>
                <input
                  type="number"
                  class="form-control"
                  id="banyak"
                  min="1"
                  v-model="pesan.banyak"
                />
              </div>
              <div class="form-group">
                <label for="keterangan"> Description </label>
                <textarea
                  v-model="pesan.keterangan"
                  type="text"
                  class="form-control"
                  id="keterangan"
                  placeholder="description.."
                ></textarea>
              </div>
              <button type="submit" class="btn btn-primary" @click="pemesanan">
                <b-icon-cart></b-icon-cart> Order
              </button>
            </form>
          </h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "viFoodDetails",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      pesan: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesan.banyak) {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push ({ path: "/keranjang" })
            this.$toast.success("input successfully to cart", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("can not be empty", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>