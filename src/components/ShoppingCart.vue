<template>
  <div class="cart">
    <p class="cart-title">Shopping Cart</p>
    <p class="cart-empty" v-if="total == 0">Your Shopping Cart is Empty!</p>
    <div class="items" v-else>
      <div class="item clearfix" v-for="item in items">
        <img :src="'/dist/' + item.image" class="item-image">
        <div class="item-details">
          <p class="item-title">{{item.title}}</p>
          <p class="item-price">
            <span>x{{item.qty}}</span>
            <span class="right">$ {{item.qty * item.price}}</span>
          </p>
        </div>
      </div>
    </div>
    <div class="cart-total">
      <span>Total</span>
      <span class="right">$ {{total}}</span>
    </div>
  </div>
</template>
<script>
  import State from '../shoppingCartState'
  import _ from 'lodash'

  export default {
    data() {
      return {
        items: State.data.cart
      }
    },
    computed: {
      total () {
        return _.sumBy(this.items, function(item) {
          return (item.price * item.qty)
        })
      }
    }
  }
</script>
<style>
  .cart {
    margin-left: 1em;
  }
  .cart-title {
    margin: 0.5em 0 0 0;
    font-weight: bold;
    text-transform: uppercase;
    text-align: center;
    padding: 0.75em;
    background: #35495E;
    color: #fff;
  }

  .cart-empty {
    text-align: center;
    margin: 4em 0 0 0;
    min-height: 300px;
  }
  .cart-total {
    background: #F1F1F1;
    margin: 0;
    padding: 0.75em;
  }

  .items {
    min-height: 300px;
  }

  .item {
    padding: 0.75em 0.5em;
    border-top: 1px solid #ddd;
  }

  .right {
    float: right;
  }

  .item-image {
    float: left;
    width: 20%;
  }
  .item-details {
    float: left;
    width: 80%;
    padding-left: 0.75em;
  }
  .item-title {
    margin: 0;
    font-weight: bold;
  }
  .item-price {
    margin: 0;
    font-size: 0.9em;
  }
</style>