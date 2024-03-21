<template>
    <h1 class="text-center p-5">Welcome to My Frozen Goods Store!</h1>

    <!--Vue components for the product list and shopping cart-->
    <ProductList @add-to-cart="addToCart"  />
    <ShoppingCart :cartItems="cartItems" @remove-from-cart="removeFromCart" @increase-quantity="increaseQuantity" @decrease-quantity="decreaseQuantity"/>
</template>

<script>
// imported components
import ProductList from './components/ProductList.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  name: 'App',
  components: {
    ProductList,
    ShoppingCart,
  },
  data() {
    return {
      
      // array intended for the items in the cart
      cartItems: [],

      // boolean intended for alerting users if minimum quantity is reached
      showMinimumQuantityAlert: false
    };
  },
  methods: {
    // add to cart function for adding items to the cart
    addToCart({ product, quantity }) { 

      // constant variable intended to check if the product being added is already existing in the cart
      const existingProductIndex = this.cartItems.findIndex(item => item.product.name === product.name);
      
      if (existingProductIndex !== -1) {
        // if product exists, it will just add quantity of 1
        this.cartItems[existingProductIndex].quantity += quantity;
      } else {
        // otherwise, another product will be added into the cart
        this.cartItems.push({ product: { ...product }, quantity });
      }

      alert(product.name + " was added to the cart successfully!");
    },
    // function that removes items in the cart
    removeFromCart(index) {
      alert("Product removed successfully from your cart.");
      // removes the selected product from the cart
      this.cartItems.splice(index, 1);
    },
    // function intended to increase the quantity of an item in the cart
    increaseQuantity(index) {
      if (this.cartItems[index].quantity === 10) {
        // checks if product has reached the allowed maximum quantity
        alert("You have reached the maximum quantity allowed for this product.");
      } else {
        // otherwise, the quantity will be added to the product
        this.cartItems[index].quantity++;
      }
    },
    // function intended to decrease the quantity of an item in the cart
    decreaseQuantity(index) {
      if (this.cartItems[index].quantity > 1) {
        // checks if product has not yet reached the required mininum quantity of a product, if true, the quantity will be decreased 
        this.cartItems[index].quantity--;
      } else if (this.cartItems[index].quantity === 1 && !this. showMinimumQuantityAlert) {
      // otherwise, an alert will be shown
      this.showMinimumQuantityAlert = true;
      alert("You have reached the minimum quantity required for the product.");
    }
  }
 }
}
</script>

<style>

</style>
