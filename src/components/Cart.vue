<template>
  <ul class="list-group">
    <li class="list-group-item">
      <span class="item-name">Name</span>
      <span class="item-price float-right">Price</span>
    </li>
    <hr />
    <li v-for="(item, index) in items" :key="index" class="list-group-item">
      <span class="item-name">{{ item.title }}</span>
      <span class="item-price ml-5">${{ item.price }}</span>
      <button
        class="btn btn-sm btn-danger float-right"
        @click="removeItem(index)"
      >
        X
      </button>
    </li>
    <hr />
    <li class="list-group-item">
      <span class="item-name">Total</span>
      <span class="item-price float-right">${{ totalPrice.toFixed(2) }}</span>
    </li>

    <li v-if="" class="list-group-item">
      <button @click="clearCart" class="btn btn-block btn-success">Checkout</button>
    </li>
  </ul>
</template>

<script>
export default {
  // props: ["items"],

  computed: {
    items(){
      return this.$store.getters.getCart
    },
    totalPrice() {
      //            let total = 0;
      //            this.items.forEach(item => {
      //                total+= parseFloat(item.price)
      //            });

      // const total = this.items.reduce(
      //   (total, item) => (total += parseFloat(item.price)),
      //   0
      // );
      // return total;

      return this.items.reduce(
        (total, item) => (total += parseFloat(item.price)),
        0
      );
    },
  },
  methods: {
    removeItem(index) {
      // this.$emit("removeItem", index);
      this.$store.commit("removeItem", index);
    },
    clearCart(){
      if(confirm('Are you sure, you want to delete this!!')){
        this.$store.commit('clearCart')
      }
      
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
