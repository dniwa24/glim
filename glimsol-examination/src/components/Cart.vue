<template>
    <div>   
        <div v-for="product in products" :key="product.id">
            <p>{{product.name}}</p>
            <p>{{product.qty}}</p>
            <p>{{product.price}}</p>
            <v-btn class="primary" dark @click="addToCart(product.id, product.name, product.qty, product.price)">Add to cart</v-btn>
            <hr>
        </div>

        <div v-for="c in cart" :key="c.productName">
            <p>{{c.productName}}</p>
            <p>{{c.productQty}}</p>
            <p>{{c.productPrice}}</p>
        </div>

    </div>
</template>

<script>
export default {
    data() {
        return {
            cart: [],
            products: [
                {
                    id: 1,
                    name: "Product 1",
                    qty: 1,
                    price: 100
                },
                {
                    id: 2,
                    name: "Product 2",
                    qty: 1,
                    price: 200
                },
                {
                    id: 3,
                    name: "Product 3",
                    qty: 1,
                    price: 300
                },
                {
                    id: 4,
                    name: "Product 4",
                    qty: 1,
                    price: 400
                },
            ]
        }
    },
    methods: {
        addToCart(id, name, qty, price){
            const productData = {
                productId: id,
                productName: name,
                productQty: qty,
                productPrice: price
            }
            const isExist = this.cart.find((product) => {
                return product.productId === productData.productId
            })
            if(isExist){
                productData.productQty++;
                console.log(productData.productQty);}
            else
                this.cart.push(productData)
            // this.cart.push(productData)
            console.log(this.cart)
        }
    }
}
</script>

<style>

</style>