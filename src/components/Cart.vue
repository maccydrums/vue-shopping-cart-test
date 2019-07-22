<template>
  <div class="card">
    <div class="card-body">
    <ul class="list-group">
      <li class="list-group-item" :key="item.id" v-for="item in items">
        {{ item.title }} <br/>$ {{ item.price }} + shipping
        <button
          @click="$emit('remove-from-cart', item)"
          class="btn badge-danger float-right"
        >Remove from cart</button>
      </li>
    </ul>
    <div class="p-3 mt-5">
      <h4 class="text-center">Total: $ {{ total }}</h4>
    </div>
    <button :disabled="items.length === 0" @click="$emit('pay')" class="btn btn-info form-control center">Pay Now</button>
  </div>
  </div>
</template>

<script>
export default {
  props: ["items"],
  computed: {
    total() {
      return this.items.reduce((acc, item) => acc + Number(item.price), 0)
    }
  }
}
</script>