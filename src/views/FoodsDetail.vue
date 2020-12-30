<template>
<div>
<Navbar/>
  <div class="container">
    <div class="row mt-5">
      <div class="col-12 col-sm-12 col-md-6 col-lg-6">
        <img
          :src="'../assets/images/' + product.gambar"
          class="img-fluid shadow"
          alt=""
        />
      </div>
      <div class="col-12 col-sm-12 col-md-6 col-lg-6">
        <h2>
          <strong>{{ product.nama }}</strong>
        </h2>
        <hr />
        <h4>
          Harga : <strong>Rp. {{ product.harga }}</strong>
        </h4>
        <form class="mt-4" v-on:submit.prevent>
          <div class="form-group">
            <label for="jumlah_pemesanan">Jumlah Pesan</label>
            <input
              v-model="pesan.jumlah_pemesanan"
              type="number"
              class="form-control"
            />
          </div>
          <div class="form-group">
            <label for="keterangan">Keterangan</label>
            <textarea
              v-model="pesan.keterangan"
              class="form-control"
              placeholder="Keterangan : Pedas Cabai 10, Nasi 2..."
            ></textarea>
          </div>
          <button type="submit" class="btn btn-success" @click="pemesanan">
            <b-icon-cart></b-icon-cart> Pesan
          </button>
        </form>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "FoodsDetail",
  components: {
      Navbar
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
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({
                path: "/keranjang"
            })
            this.$toast.success("Sukses Masuk Keranjang", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((error) => console.log(error));
      } else {
        this.$toast.error("Jumlah Pemesanan Harus Diisi", {
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