<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link> |
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link> |
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>
    <div @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <!-- الرقم جانب عربة التسوق (عدد المنتجات) -->
      <span>Cart ({{ totalQuantity }})</span>
    </div>
  </header>
  <!-- <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav> -->
  <router-view :inventory="inventory" :addToCart="addToCart" />
  <SidebarComponent
        v-if="showSidebar"
        :toggle="toggleSidebar"
        :cart="cart"
        :inventory="inventory"
        :remove="removeItem"
        />
</template>

<script>
import SidebarComponent from '@/components/SidebarComponent.vue'
import food from './food.json'

export default {
  components: {
    SidebarComponent
  },
  data () {
    return {
      showSidebar: false,
      inventory: food,
      cart: {}
    }
  },

  //
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr
      }, 0)
    }
  },
  //
  methods: {
    addToCart (name, quantity) {
      console.log(name)
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
      // تصفير مربع إدخال كمية المنتج
      console.log(this.cart)
    },
    //
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    //
    removeItem (name) {
      delete this.cart[name]
    }
  }
}
</script>

<style></style>
<!--
  scoped
  هي لتطبيق التنسيق هنا فقط
-->
<style scoped></style>
