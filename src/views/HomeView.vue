<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">
          Welcome to "World of Books"!
        </p>
        <p class="subtitle">
          The best online bookstore!
        </p>
      </div>
    </section>
    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Latest books</h2>
      </div>
      <ProductBox 
        v-for="product in latestProducts"
        v-bind:key="product.id"
        v-bind:product="product" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'

import ProductBox from '@/components/ProductBox';

export default {
  name: 'HomeView',
  data() {
    return{
      latestProducts: []
    }
  },
  components: {
    ProductBox
  }, 
  mounted(){
    this.getLatestProducts();
    document.title = "Home | World of Books";
  }, 
  methods: {
    async getLatestProducts(){

      this.$store.commit('setIsLoading', true);

      await axios.get('/api/v1/latest-products/')
        .then(response =>{
          this.latestProducts = response.data;
        })
        .catch(error => {
          console.log(error);
        });

        this.$store.commit('setIsLoading', false);
    }
  }
}
</script>

<style scoped>
  .title{
    font-size: 60px;
  }
  .subtitle{
    font-weight: 600px;
    font-size: 30px;
    text-shadow: 0 0 5px rgba(0,0,0,0.9);
  }

  .hero-body{
    background: linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)),url("../assets/books-background.jpg") top center;
  }
</style>