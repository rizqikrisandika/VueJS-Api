<template>
  <div class="keranjang">
    <Navbar :updateKeranjang="keranjangs" />
    <div class="container mt-5">
      <h2><strong>Keranjang Saya</strong></h2>
      <table class="table">
        <thead>
          <tr>
            <th scope="col">No</th>
            <th scope="col">Gambar</th>
            <th scope="col">Makanan</th>
            <th scope="col">Keterangan</th>
            <th scope="col">Jumlah</th>
            <th scope="col">Harga</th>
            <th scope="col">Total Harga</th>
            <th scope="col">Hapus</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
            <th scope="row">{{ index + 1 }}</th>
            <td>
              <img
                :src="'../assets/images/' + keranjang.products.gambar"
                alt=""
                width="240px"
                class="img-fluid"
              />
            </td>
            <td>{{ keranjang.products.nama }}</td>
            <td>{{ keranjang.keterangan ? keranjang.keterangan : "-" }}</td>
            <td>{{ keranjang.jumlah_pemesanan }}</td>
            <td>Rp. {{ keranjang.products.harga }}</td>
            <td>
              Rp. {{ keranjang.products.harga * keranjang.jumlah_pemesanan }}
            </td>
            <td class="text-center text-danger">
              <b-icon-trash
                @click="hapusKeranjang(keranjang.id)"
              ></b-icon-trash>
            </td>
          </tr>
          <tr>
            <td colspan="6" align="right">
              <strong>Total Harga</strong>
            </td>
            <td>
              <strong>Rp. {{ totalHarga }}</strong>
            </td>
            <td></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "Keranjang",
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
          this.$toast.error("Sukses hapus Keranjang", {
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
        return items + data.products.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
};
</script>

<style>
</style>