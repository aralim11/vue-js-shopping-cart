<template>
    <li class="list-group-item">
        <div class="row">
            <div class="col-5 col-sm-5 col-md-5 col-lg-5 zero">{{ name }}</div>
            <div class="col-3 col-sm-3 col-md-3 col-lg-3 zero"><span class="badge badge-warning" v-on:click="submitCartMinus(id)">-</span>&nbsp;{{qty}}&nbsp;<span class="badge badge-dark" v-on:click="submitCartPlus(id)">+</span></div>
            <div class="col-3 col-sm-3 col-md-3 col-lg-3 zero">${{ calculate(price * qty) }}</div>
            <div class="col-1 col-sm-1 col-md-1 col-lg-1 zero"><span class="badge badge-danger" v-on:click="submitRemoveCart(id)">x</span></div>
        </div>
    </li>
</template>

<script>
export default {
    props: ['id', 'name', 'price', 'qty'],
    inject: ['removeCart', 'cartPlus', 'cartMinus'],
    methods: {
        submitRemoveCart: function(id) {
            this.removeCart(id);
        },

        submitCartPlus: function(id) {
            this.cartPlus(id);
        },

        submitCartMinus: function(id) {
            this.cartMinus(id);
        },

        calculate: function(multi) {
            return multi.toFixed(2);
        }
    },
}
</script>

<style scoped>
    .badge {
        cursor: pointer;
    }

    .zero {
        margin: 0px;
        padding: 0px;
    }
</style>