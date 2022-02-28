<template>
  <div id="app">
  <b-row>
  <b-col cols="4" v-for="product in products" v-bind:key="product._id">

  <b-card :title="product.name" :img-src="product.image" img-alt="Image" img-top tag="article" style="max-width: 20rem;" class="mb-2">
  
     <b-card-text>{{product.price}}</b-card-text>
    
      <b-button variant="success" v-on:click="Plus5(product)">+5</b-button>
      <b-button variant="success" v-on:click="Plus1(product)">+</b-button>
      {{product.quantity}}
      <b-button variant="danger" v-on:click="Minus1(product)">-</b-button>
      <b-button variant="danger" v-on:click="Minus5(product)">-5</b-button>
      Subtotal:RM {{product.quantity*product.price}}
</b-card>
  </b-col>
  </b-row>
  ============Price Total======================
  <div v-for="product in products" :key="product">
  <p v-if="product.quantity>0">
    {{product.name}}
   </p>
   </div> 
   Subtotal: {{calSubtotal}}
    <select v-model="shippingfee">
    <option v-for="flavor in areaOptions" :value="flavor.fees" :key="flavor._id"  :selected="option == '5'">{{flavor.text}}</option>
  </select>
  Shipping Fees: {{shippingfee}}<br>
  Grand Total: {{calTotal}}


  </div>
</template>

<script>

export default {
  name: "App",
  components: {},
  data() {
    return {
      name: "",
      mobile: "",
      email: "",
      quantity: 0,
      totalSales: 0,
      discountPct: 0,
      pickupArea: 0,
      shippingfee:5,
      areaOptions: [
        { value: "0", text: "Mont Kiara", fees:5 },
        { value: "1", text: "Cheras", fees:4},
        { value: "2", text: "Puchong", fees:3 },
        { value: "3", text: "Kepong", fees:2 },
        { value: "4", text: "Others", fees:1 },
      ],
      products: [
        {
          name: "Apple",
          quantity: 0,
          price: 10,
          stock: 0,
          image: "apple.jpg",
        },
        {
          name: "Orange",
          quantity: 0,
          price: 12,
          stock: 0,
          image: "orange.jpg",
        },
        {
          name: "Strawberry",
          quantity: 0,
          price: 9,
          stock: 0,
          image: "strawberry.jpg",
        },
        {
          name: "Strawberry 2",
          quantity: 0,
          price: 7,
          stock: 0,
          image: "strawberry.jpg",
        },
        {
          name: "Orange 2",
          quantity: 0,
          price: 13,
          stock: 0,
          image: "orange.jpg",
        },
        {
          name: "Apple 2",
          quantity: 0,
          price: 11,
          stock: 0,
          image: "apple.jpg",
        },
      ],
    };
  },
  created() {
     
    },
  methods: {
  Plus5(product) {
      product.quantity+=5;
    },
    Plus1(product){
      product.quantity+=1;
    },
    Minus5(product){
      
      if(product.quantity-5>=0){
        product.quantity-=5;
      }
    },
    Minus1(product){
      
      if(!product.quantity-1<0){
        product.quantity-=1;
      }
    },
    
    
    
  },
  computed: {
  calSubtotal() {
    var Subtotal=0;
    for(let i=0;i<this.products.length;i++){
      Subtotal+=this.products[i].quantity*this.products[i].price;

    }
    
    return Subtotal;
  },
  calTotal(){
    var grandTotal=0;
    for(let i=0;i<this.products.length;i++){
      grandTotal+=this.products[i].quantity*this.products[i].price;

    }

    grandTotal+=this.shippingfee;
    return grandTotal;

  }
  

  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}


.blueFont {
  color: blue;
  
}

.greenFont {
  color: green;
  font-size: 30px;
}

.redFont {
  color: red;
  font-size: 30px;
}

.redbg {
  background: red;
}
</style>
