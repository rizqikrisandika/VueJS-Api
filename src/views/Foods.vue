<template>
  <div>
    <Navbar/>
    <div class="container">
      <div class="row mt-5">
        <div class="col-12 col-sm-12 col-md-8 col-lg-8">
          <h2>Daftar <strong>Menu</strong></h2>
        </div>
        <div class="col-12 col-sm-12 col-md-4 col-lg-4">
          <div class="input-group mb-3">
            
            <input
              v-model="search"
              type="text"
              class="form-control"
              placeholder="Cari Makanan.."
              aria-label="Cari"
              aria-describedby="basic-addon1"
              @keyup="searchFoods"
            />
            <div class="input-group-prepend">
              <span class="input-group-text" id="basic-addon1">
                <b-icon-search></b-icon-search>
              </span>
            </div>
          </div>
        </div>
      </div>
      <div class="row mt-5">
        <div
          class="col-12 col-sm-12 col-md-4 col-lg-4 mb-4"
          v-for="product in products"
          :key="product.id"
        >
          <ProductCard :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import ProductCard from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "Foods",
  components: {
    Navbar,
    ProductCard,
  },
  data() {
    return {
      products: {},
      search: '',
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
    searchFoods() {
      axios
      .get("http://localhost:3000/products?q="+this.search)
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/products")
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>