<template>
  <header>
    <the-header
      :cartList="cartList"
      @handle-delete-cart="handleDelete"
      @handle-up-or-down-amount-cart="handleUpOrDownAmount"
    />
  </header>
  <main class="container">
    <product-list @handle-buy="handleBuy" />
  </main>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import ProductList from "./components/ProductList.vue";
export default {
  name: "App",
  components: {
    TheHeader,
    ProductList,
  },

  data() {
    return {
      cartList: [],
    };
  },
  props: {
    cardList: Array,
  },
  methods: {
    handleBuy(productItem) {
      const index = this.cartList.findIndex(
        (cart) => cart.id === productItem.id
      );
      if (index !== -1) {
        this.cartList[index].amount += 1;
      } else {
        const newproductItem = { ...productItem, amount: 1 };
        this.cartList = [...this.cartList, newproductItem];
      }
      //console.log(this.cartList)

      // this.cartList.push(newCartList);
      //this.cartList.push(productItem);
      // console.log(this.cartList);
    },
    handleDelete(cart) {
      this.cartList = this.cartList.filter(
        (cartItem) => cartItem.id !== cart.id
      );
    },
    handleUpOrDownAmount(params) {
      const { status, cart } = params;
      const index = this.cartList.findIndex(
        (cartItem) => cartItem.id === cart.id
      );
      if (index !== -1) {
        if (status) {
          if ( this.cartList[index].amount < this.cartList[index].quantityInStock) {
            this.cartList[index].amount += 1;
          } else {
            alert("Không được tăng nữa");
          }
        } else {
          if (this.cartList[index].amount > 1) {
            this.cartList[index].amount -= 1;
          } else {
            alert("Không được giảm nữa");
          }
        }
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
