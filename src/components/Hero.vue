<template>
  <div class="row mt-2 flex-column-reverse flex-lg-row flex-md-row">
    <div class="col-12 col-sm-12 col-md-6 col-lg-6">
      <div class="d-flex h-100">
        <div class="justify-content-center align-self-center">
          <h2>
            <strong>Delicious Food Menu,</strong><br />
            in Your Gadget
          </h2>
          <p>Ayo segera pilih dan pesan makanan favorit Anda</p>
          <router-link class="btn btn-success" to="/foods"><b-icon-arrow-right></b-icon-arrow-right> Pesan</router-link>
        </div>
      </div>
    </div>
    <div class="col-12 col-sm-12 col-md-6 col-lg-6">
      <img src="../assets/images/hero.png" width="100%" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Hero",
};
</script>

<style>
</style>