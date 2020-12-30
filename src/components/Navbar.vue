<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <b-navbar-brand href="#"><strong>Makan</strong>Yuk</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <ul class="navbar-nav">
            <li class="nav-item active">
              <router-link class="nav-link" to="/">Home</router-link>
            </li>
            <li class="nav-item active">
              <router-link class="nav-link" to="/foods">Menu</router-link>
            </li>
          </ul>
            <router-link class="nav-link" to="/keranjang"
              >
              <b-icon-bag></b-icon-bag>
              <span class="badge badge-success ml-2">{{
                updateKeranjang ? updateKeranjang.length : jumlah_pesanan.length
              }}</span>
            </router-link>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Navbar",
  data() {
    return {
      jumlah_pesanan: [],
    };
  },
  props: ["updateKeranjang"],
  methods: {
    setJumlah(data) {
      this.jumlah_pesanan = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setJumlah(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>