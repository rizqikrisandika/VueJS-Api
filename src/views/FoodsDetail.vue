<template>
  <div class="container">
    <div class="row">
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
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "FoodsDetail",
  data() {
    return {
      product: [],
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
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