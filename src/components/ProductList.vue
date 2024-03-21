<template class="mt-5">
    <div>
        <!--Table of Products-->
        <h2>List of Available Products</h2>
        <table class="table ">
            <thead class="table-primary">
                <tr>
                    <th>Product Name</th>
                    <th>Product Price</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody class="table-secondary">
                <!--Loop for showing the list of products -->
                <tr v-for="(product, index) in productList" :key="index">
                    <td>{{product.name }}</td>
                    <td>Php {{ product.price.toFixed(2) }}</td>
                    <td><button type="button" class="btn-success" @click="addToCart(product)">Add To Cart</button></td>

                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
  export default {
    data() {
        return {
            // product list
            productList: [
                {name: 'Frozen French Fries (1kg)', price: 116 },
                {name: 'Frozen Pork Siomai (500 grams)', price: 85},
                {name: 'Frozen Cheesy Chicken Tenders (500 grams)', price: 90},
                {name: 'Ice Cream (Vanilla Flavor) 1L', price: 159},
                {name: 'Frozen Burger Patties (250 grams)', price: 55},
                {name: 'Frozen Hotdog (1 kilograms)', price: 148},
                {name: 'Calamares (500 grams)', price: 109},
                {name: 'Squid Balls (250 grams)', price: 45},
                {name: 'Fish Balls (1kg)', price: 85},
                {name: 'Kikiam (500 grams)', price: 70}
            ],
        }
    },
    methods: {
      addToCart(product) {
        // emitted event into the App.vue
        this.$emit('add-to-cart', { product, quantity: 1 });
      }
    }
  }
</script>

<style scoped>


</style>