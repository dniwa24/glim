<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-toolbar-title>Examination</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn color="primary" depressed dark @click="drawer = true">
        <v-icon>mdi-cart</v-icon>
        <v-badge color="green"  :content="notification" :value="notification"></v-badge>
      </v-btn>
      <!-- <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon> -->
    </v-app-bar>

    <v-navigation-drawer :width="350" v-model="drawer" absolute temporary right>
      <v-container class="d-flex" v-for="c in cart" :key="c.id">
        <v-row dense>
          <v-col cols="12">
            <v-card max-width="300">
            <v-card-title>
              <v-img :src="c.image"></v-img>
            </v-card-title>
            <v-card-subtitle>{{c.name}}</v-card-subtitle>
            <v-card-text>
              <p>Price: {{c.price * c.qty}}</p>
              <p>Quantity: {{c.qty}}</p>
            </v-card-text>
          </v-card>
          </v-col>
        </v-row>
        
      </v-container>
      <template v-slot:append>
        <div class="pa-2">
          <p>Total Price: {{totalPrice}}</p>
        </div>
      </template>
    </v-navigation-drawer>

    <v-main>
      <v-container>
        <v-row>
          <v-col cols="3" v-for="product in products" :key="product.id">
            <v-card
              max-width="344">
              
              <v-card-title>
                <v-img :src="product.image"></v-img>
              </v-card-title>
              <v-card-subtitle>{{product.name}}</v-card-subtitle>
              <v-card-text>Price: {{product.price}}</v-card-text>
              <v-card-actions>
                <v-btn class="primary" dark @click="addToCart(product)">Add to cart</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>


export default {
  name: 'App',

  data() {
    return {
      drawer: false,
      products: [
                {
                    id: 1,
                    image: 'https://picsum.photos/500/300?random=1',
                    name: "Product 1",
                    qty: 1,
                    price: 100
                },
                {
                    id: 2,
                    image: 'https://picsum.photos/500/300?random',
                    name: "Product 2",
                    qty: 1,
                    price: 200
                },
                {
                    id: 3,
                    image: 'https://picsum.photos/510/300?random=2',
                    name: "Product 3",
                    qty: 1,
                    price: 300
                },
                {
                    id: 4,
                    image: 'https://picsum.photos/510/300?random=3',
                    name: "Product 4",
                    qty: 1,
                    price: 400
                },
            ],
            cart: [],
            totalPrice: 0,
            notification: 0
    }
  },
  methods: {
    
    addToCart(product){
      const prod = this.cart.find((e) => {
        return e.id === product.id
      })
      if(prod){
        prod.qty += 1;
        this.totalPrice += product.price;
        this.notification++;

        return;
      } 
      this.cart.push(product);
      this.totalPrice += product.price;
      this.notification++;
      
    }
  }
};
</script>

<style scoped>
.sss{
  border: 1px solid red;
}
</style>