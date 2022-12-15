<template>
  <div class="hero">
    <!-- Dekstop -->
    <div class="d-none d-md-block">
      <div class="row mt-4">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <b> Delicious Foods Menu, </b> <br />
                in Your Gadget
              </h2>
              <p>Find your Favorite Food & Drink</p>
              <router-link to="/foods" class="btn btn-lg btn-primary">Order</router-link>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/images/Hero.png" width="100%" />
        </div>
      </div>
    </div>

    <!-- Mobile -->
    <div class="d-sm-block d-md-none">
      <div class="row mt-4">
        <div class="col-md-6 mb-3">
          <img src="../assets/images/Hero.png" width="100%" />
        </div>
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <b> Delicious Foods Menu, </b> <br />
                in Your Gadget
              </h2>
              <p>Find your Favorite Food & Drink</p>
              <button class="btn btn-lg btn-primary">Order</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "comHero",
};
</script>

<style>
</style>