<template>
  <div class="container">
    <div class="row">
      <div class="col-md-7">
        <div class="row">
          <div class="col-md-6" :key="product.id" v-for="product in products">
            <product :isInCart="isInCart(product)" v-on:add-to-cart="addToCart(product)" :product="product" />
          </div>
        </div>
      </div>
      <div class="col-md-5 my-5">
        <Cart v-on:pay="pay()" v-on:remove-from-cart="removeFromCart($event)" :items="cart"/>
      </div>
    </div>
  </div>
</template>

<script>
import products from "./products.json";
import Product from "./components/Product.vue";
import Cart from "./components/Cart.vue"

export default {
  name: "app",
  data() {
    return {
      products,
      cart: []
    };
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
    },
    isInCart(product) {
      const item = this.cart.find(item => item.id === product.id)

      if(item) {
        return true
      }
      return false
    },
    removeFromCart(product) {
      this.cart = this.cart.filter(item => item.id !== product.id)
    },
    pay() {
      this.cart = []
      alert('Your order is completed!')
    }
  },
  components: {
    Product,
    Cart
  }
};
</script>

<style>
body {
  background-color: rgb(212, 212, 212);
}
</style>
