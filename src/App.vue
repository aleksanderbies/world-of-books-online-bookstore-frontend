<template>
  <div id="wrapper">
    <nav class="navbar is-dark">
      <div class="navbar-brand">
        <router-link to="/" tag="img" class="navbar-item routerlink" ><img src ="./assets/world_of_books_logo.png"></router-link>
        <a class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbar-menu" @click="showMobileMenu = !showMobileMenu">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>
      <div class="navbar-menu" id="navbar-menu" v-bind:class="{'is-active': showMobileMenu}">
        <div class="navbar-end">
          <router-link to="" class="navbar-item">Drama</router-link>
          <router-link to="" class="navbar-item">Fantasy</router-link>
          <router-link to="" class="navbar-item">Historical</router-link>
          <router-link to="" class="navbar-item">Romantic</router-link>
          <router-link to="" class="navbar-item">Sci-Fi</router-link>
          <div class="navbar-item">
            <div class="buttons">
              <router-link to="/log-in" class="button is-light">
              <span class="icon"><i class="fa-solid fa-arrow-right-to-bracket"></i></span>
              <span>Log in</span></router-link>
              <router-link to="/cart" class="button is-success"> 
                <span class="icon"><i class="fas fa-shopping-cart"></i></span>
                <span>Cart ({{ cartTotalLength }})</span>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </nav>
    <section class="section">
      <router-view/>
    </section>
    <footer class="footer">
      <p class="has-text-centered">
        Copyright &copy; 2022
      </p>
    </footer>
  </div>
</template>


<script>
import axios from 'axios'
export default {
  data() {
    return {
      showMobileMenu: false,
      cart: {
        items: []
      }
    }
  },
  beforeCreate() {
    this.$store.commit('initializeStore')
    const token = this.$store.state.token
    if (token) {
        axios.defaults.headers.common['Authorization'] = "Token " + token
    } else {
        axios.defaults.headers.common['Authorization'] = ""
    }
  },
  mounted() {
    this.cart = this.$store.state.cart
  },
  computed: {
      cartTotalLength() {
          let totalLength = 0
          for (let i = 0; i < this.cart.items.length; i++) {
              totalLength += this.cart.items[i].quantity
          }
          return totalLength
      }
  }
}
</script>

<style lang="scss">
@import '../node_modules/bulma';
</style>