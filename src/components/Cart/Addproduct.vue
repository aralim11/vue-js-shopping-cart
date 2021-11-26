<template>
    <div class="row mt-10">
        <div class="col-md-12">
            <base-card>
                <div class="col-md-6 offset-sm-3">
                    <form @submit.prevent="addProduct">
                        <div class="form-row">
                            <div class="form-group col-md-6">
                                <label for="product_name">Product Name <span class="required">*</span></label>
                                <input type="text" class="form-control" id="product_name" ref="product_name" placeholder="Enter Product Name">
                            </div>
                            <div class="form-group col-md-6">
                                <label for="price">Price <span class="required">*</span></label>
                                <input type="number" class="form-control" id="price" ref="price" placeholder="Enter Product Price">
                            </div>
                        </div>

                        <div class="form-row">
                            <div class="form-group col-md-6">
                                <label for="quantity">Quantity <span class="required">*</span></label>
                                <input type="number" class="form-control" id="quantity" ref="quantity" placeholder="Enter Product Quantity">
                            </div>
                        </div>
                        
                        <button type="submit" class="btn btn-primary">Save</button>
                        <span v-if="isRequired" class="required"><strong> &nbsp;&nbsp;All Field Is Required!! </strong></span>
                    </form>
                </div>
            </base-card>
        </div>
    </div>
</template>

<script>
export default {
    inject: ['storeProduct'],
    data: function(){
        return {
            isRequired: false,
        }
    },
    methods: {
        addProduct: function() {
            const product_name = this.$refs.product_name.value;
            const price = this.$refs.price.value;
            const quantity = this.$refs.quantity.value;

            if (product_name.trim() === '' && price.trim() === '' && quantity.trim() === '') {
                this.isRequired = true;
                return;
            }

            this.storeProduct(product_name, price, quantity);
        }
    },
}
</script>

<style scoped>
    .required{
        color: red;
        font-weight: 700;
    }
</style>