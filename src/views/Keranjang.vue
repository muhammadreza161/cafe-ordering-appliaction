<template>
  <div class="keranjang">
    <Navbar :updateKeranjang="keranjangs"/>
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
                My Cart
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h3>My <b> Order List </b></h3>
          <div class="table-responsive mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">No</th>
                  <th scope="col">Photos</th>
                  <th scope="col">Foods</th>
                  <th scope="col">Description</th>
                  <th scope="col">Amount</th>
                  <th scope="col">Price</th>
                  <th scope="col">Total</th>
                  <th scope="col">Action</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(keranjang, index) in keranjangs"
                  :key="keranjang.id"
                >
                  <th>{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="'../assets/images/' + keranjang.products.gambar"
                      class="img-fluid sahadow"
                      width="200"
                    />
                  </td>
                  <td>
                    <b>{{ keranjang.products.nama }}</b>
                  </td>
                  <td>
                    {{ keranjang.keterangan ? keranjang.keterangan : "-" }}
                  </td>
                  <td>
                    {{ keranjang.banyak }}
                  </td>
                  <td>Rp. {{ keranjang.products.harga }}</td>
                  <td>
                    <b>
                      Rp. {{ keranjang.products.harga * keranjang.banyak }}</b
                    >
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash
                      @click="hapusKeranjang(keranjang.id)"
                    ></b-icon-trash>
                  </td>
                </tr>

                <tr>
                  <td colspan="6" align="right">
                    <b>GRAND TOTAL :</b>
                  </td>
                  <td>
                    <b>Rp. {{ totalHarga }}</b>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "viKeranjang",
  components: {
    Navbar,
  },
  data() {
    return {
      keranjangs: [],
    };
  },
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data;
    },
    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          this.$toast.error("Success Deleted Product", {
            type: "error",
            position: "top-right",
            duration: 3000,
            dismissible: true,
          });

          axios
            .get("http://localhost:3000/keranjangs")
            .then((response) => this.setKeranjangs(response.data))
            .catch((error) => console.log(error));
        })
        .catch((error) => console.log(error));
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setKeranjangs(response.data))
      .catch((error) => console.log(error));
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce(function (items, data) {
        return items + data.products.harga * data.banyak;
      }, 0);
    },
  },
};
</script>

<style>
</style>