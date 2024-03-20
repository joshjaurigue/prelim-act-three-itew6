<template>
  <div class="mt-5">
    <h2 class="text-center fw-bold">Shopping Cart</h2>
    <!--Checks if cart is empty or not-->
    <div v-if="cartItems.length === 0">
      <p class="text-center text-danger empty">Your cart is empty.</p>
    </div>
    <div v-else>
      <!--Format for the Shopping Cart-->
      <table class="table text-center">
        <thead class="table-info">
          <tr >
            <th>Product</th>
            <th>Price</th>
            <th>Quantity</th>
            <th>Subtotal</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <!--Loop for showing the cart-->
          <tr v-for="(item, index) in cartItems" :key="index">
            <td>{{ item.product.name }}</td>
            <td>Php {{ item.product.price.toFixed(2) }}</td>
            <td>
              <button class="btn-primary" @click="decreaseQuantity(index)">-</button>
              {{ item.quantity }}
              <button class="btn-primary"  @click="increaseQuantity(index)">+</button>
            </td>
            <td>Php {{ (item.product.price * item.quantity).toFixed(2) }}</td>
            <td><button class="btn-danger" @click="removeFromCart(index)">Remove</button></td>
          </tr>
        </tbody>
        <tr>
            <p class="total text-primary">Total: Php {{ totalPrice.toFixed(2) }}</p>
          </tr>
      </table>
   
    </div>
  </div>
  
</template>

<script>
export default {
  // props to be inherited by the parent class
  props: ['cartItems'],
  methods: {
    removeFromCart(index) {
      // emitted event for removing items in the cart
      this.$emit('remove-from-cart', index); 
    },
    increaseQuantity(index) {
       // emitted event for increasing the quantity of a product in the cart
      this.$emit('increase-quantity', index); 
    },
    decreaseQuantity(index) {
        // emitted event for decreasing the quantity of a product in the cart
      this.$emit('decrease-quantity', index); 
    },
  },
  computed: {
    // computed property intended for the total price of the product
    totalPrice() {
      return this.cartItems.reduce((total, item) => total + item.product.price  * item.quantity, 0);
    },
    
  }
};
</script>

<style scoped>
.total {
  font-weight: bold;
  font-size: larger;
  text-decoration: underline;
}
.empty {
  font-weight: bold;
}
</style>
