<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>
    <a @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart ({{ totalQuantity }})</span>
    </a>
  </header>

  <router-view :inventory="inventory" :addToCart="addToCart" />

  <SidebarCart v-if="showSidebar" :cart="cart" :toggle="toggleSidebar" :inventory="inventory"
    :remove="removeFromCart" />
</template>

<script>
import SidebarCart from '@/components/SidebarCart.vue'
import food from './food.json'

export default {
  components: {
    SidebarCart
  },
  data () {
    return {
      showSidebar: false,
      inventory: food,
      cart: {}
    }
  },
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((total, quantity) => total + quantity, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) {
        this.cart[name] = 0
      }

      this.cart[name] += quantity
    },
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    removeFromCart (name) {
      delete this.cart[name]
    }
  }
}
</script>
