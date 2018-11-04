<template>
  <div class="cart">
    <h1>Shopping Cart</h1>
    <p v-show="!products.length"><i>Please add some products to cart.</i></p>
    <ul>
      <li v-for="product in products" :key="product.id">
        {{product.title}} - {{product.price}} - {{product.quantity}}
      </li>
    </ul>
    <p>Total:{{total|currency}}</p>
    <button @click="checkout(products)">
        Checkout
    </button>
    <p v-show="checkoutStatus">
      Checkout{{checkoutStatus}}
    </p>
  </div>
</template>

<script>
  import {mapState,mapGetters,mapActions} from 'vuex'
  export default{
    computed:{
      ...mapGetters('cart',{
        products:'cartProducts',
        total:'cartTotal'
      }),
      ...mapState('cart',{
        checkoutStatus:state=>state.checkoutStatus
      })
    },
    methods:{
        // ...mapActions(['checkout'])
      checkout (products) {
        this.$store.dispatch('cart/checkout', products)
      }
    }
  }
</script>

<style lang="">
  
</style>