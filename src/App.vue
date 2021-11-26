<template>
  <the-cart></the-cart>
</template>

<script>
import TheCart from './components/Cart/TheCart.vue';

export default {
  components: {
    'the-cart': TheCart,
  }
}
</script>

<style>
  body{
    background-color: #E2E3E5;
  }

  .mt-10 {
    margin-top: 10px;
  }
</style>