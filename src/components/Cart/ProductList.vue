<template>
    <div class="col-12 col-sm-6 col-md-6 col-lg-4 mt-10">
        <div class="card" :class="qtyCheck">
            <img class="card-img" v-bind:src="image" alt="Vans">
            <div class="card-body">
                <h6 class="card-title">{{ name }}</h6>
                <div class="buy d-flex justify-content-between align-items-center mt-16-m">
                    <div class="price text-success">
                        <h5 class="mt-4">${{ price }} - {{ qty }}</h5>
                    </div>
                    <button class="btn btn-danger mt-3" v-on:click="submitCart(id)"><i class="fas fa-shopping-cart"></i>Shop</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['id', 'name', 'price', 'image', 'qty'],
    inject: ['storeCart'],
    methods: {
        submitCart: function(id) {
            this.storeCart(id);
        }
    },

    computed: {
        qtyCheck: function() {

            if(this.qty === 0){
                return 'emptQty';
            }

           return null; 
        }
    }
}
</script>

<style scoped>
 .emptQty {
     border: 2px solid red;
 }
</style>