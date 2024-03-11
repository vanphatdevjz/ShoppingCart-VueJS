<template>
  <div class="card text-left" style="width: 18rem">
    <img class="card-img-top" :src="productItem.image" alt="" />
    <div class="card-body">
      <h4 class="card-title">{{ productItem.name }}</h4>
      <h5 class="card-text text-danger font-weight-bold">
        {{ productItem.price }}
      </h5>
    </div>
    <div class="mb-2">
      <button class="btn btn-danger ml-2" @click="handleBuy(productItem)">
        Mua
      </button>
      <button class="btn btn-info ml-2" @click="handleOpenModalDetail">
        Chi Tiết
      </button>
    </div>
  </div>
  <teleport to="#app">
    <app-modal :isOpen="isOpenModalDetail" :handleCloseModal="handleCloseModalDetail">
      <product-detail :productDetail="productItem"/>
    </app-modal>
  </teleport>
</template>

<script>
import ProductDetail from "./ProductDetail.vue";
export default {
  components: { ProductDetail },
  data() {
    return {
      isOpenModalDetail: false,
    };
  },
  props: {
    productItem: {
      type: Object,
    },
  },
  methods: {
    handleBuy(productItem) {
      this.$emit("handle-buy", productItem);
      //console.log(productItem);
    },
    handleOpenModalDetail() {
      this.isOpenModalDetail = true;
    },
    handleCloseModalDetail() {
      this.isOpenModalDetail = false;
    },
  },
};
</script>

<style></style>
