<template>
    <div class="container">
        <the-header></the-header>
        <the-top-menu></the-top-menu>
        <component :is='selectedTab'></component>
    </div>
</template>

<script>
import TheHeader from '../Layouts/TheHeader.vue';
import TheTopMenu from '../Layouts/TheTopMenu.vue';
import AddProduct from './Addproduct.vue';
import StoredProduct from './StoredProduct.vue';

export default {
    components: {
        'the-header': TheHeader,
        'the-top-menu': TheTopMenu,
        'add-product': AddProduct,
        'stored-product': StoredProduct,
    },

    data() {
        return {
            selectedTab: 'stored-product',
            products: [
                {
                    id: 1,
                    name: "Mushroom - Shitake",
                    price: 5.20,
                    image: "http://dummyimage.com/500x300.jpg/dddddd/000000",
                    qty: 12,
                },
                {
                    id: 2,
                    name: "Tea Leaves - Oolong",
                    price: 8.70,
                    image: "http://dummyimage.com/500x300.jpg/dddddd/000000",
                    qty: "20",
                },
                {
                    id: 3,
                    name: "Yams Fresh",
                    price: 7.51,
                    image: "http://dummyimage.com/500x300.bmp/dddddd/000000",
                    qty: 7,
                },
                {
                    id: 4,
                    name: "Wine - Soave Folonari",
                    price: 8.29,
                    image: "http://dummyimage.com/500x300.jpg/dddddd/000000",
                    qty: 20,
                },
            ],
            carts: []
        }
    },

    provide() {
        return {
            setSelectedTab: this.setSelectedTab,
            products: this.products,
            storeProduct: this.storeProduct,
            storeCart: this.storeCart,
            carts: this.carts,
            removeCart: this.removeCart,
            cartPlus: this.cartPlus,
            cartMinus: this.cartMinus,
        }
    },

    methods: {
        setSelectedTab: function(tab) {
            this.selectedTab = tab;
        },

        storeProduct: function(product_name, price, quantity) {

            const product = {
                id: Math.random().toString().replace("0.", ""),
                name: product_name,
                price: price,
                qty: quantity,
                image: "http://dummyimage.com/500x300.jpg/dddddd/000000",
            }

            this.products.unshift(product);
            this.selectedTab = 'stored-product';
        },

        storeCart: function(id) {
            const productExist = this.products.findIndex(res => {return res.id === id});
           
            if (this.products[productExist].qty > 0) {
                const cartExist = this.carts.filter(res => {return res.id === id});
            
                if (cartExist.length === 0) {
                    const result = this.products.filter(res => {return res.id === id});

                    for (var key in result) {
                        const value = result[key];
                        const product = {
                            id: value.id,
                            name: value.name,
                            price: value.price,
                            qty: 1,
                        }

                    this.carts.push(product);
                    }
                } else {
                    const result = this.carts.findIndex(res => {return res.id === id});
                    
                    this.carts[result].qty =  this.carts[result].qty + 1;
                }

                this.products[productExist].qty = this.products[productExist].qty - 1;
            }
        },

        cartPlus: function(id) {
            this.storeCart(id);
        },

        cartMinus: function(id) {
            const result = this.carts.findIndex(res => {return res.id === id}); 
            this.carts[result].qty =  this.carts[result].qty - 1;

            const productResult = this.products.findIndex(res => {return res.id === id});
            this.products[productResult].qty =  this.products[productResult].qty + 1;

            if(this.carts[result].qty === 0){
                this.removeCart(id);
            }
        },

        removeCart: function(id) {
            const cartListindex = this.carts.findIndex(res => res.id === id);

            const productResult = this.products.findIndex(res => {return res.id === id});
            this.products[productResult].qty =  this.products[productResult].qty + this.carts[cartListindex].qty;

            this.carts.splice(cartListindex, 1);
        }
    },
}
</script>