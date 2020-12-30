<template>
  <div class="row mt-2 flex-column-reverse flex-lg-row flex-md-row">
    <div class="col-12 col-sm-12 col-md-6 col-lg-6">
      <div class="d-flex h-100">
        <div class="justify-content-center align-self-center">
          <h2>
            <strong>MakanYuk!!! ...</strong><br />
            Banyak Menu Murah & Enak
          </h2>
          <p>Ayo segara dipesan menu kesukaan anda</p>
          <router-link class="btn btn-success" to="/foods">Pesan</router-link>
        </div>
      </div>
    </div>
    <div class="col-12 col-sm-12 col-md-6 col-lg-6">
      <img src="../assets/images/banner.svg" width="100%" alt="" />
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