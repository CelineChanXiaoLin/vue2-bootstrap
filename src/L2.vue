<template>
  <div id="app">
  <h1 class="greenFont">Conditional Rendering</h1>

  <p v-if="showText">This is true!</p>
  <p v-else>false</p>

  <b-btn @click="showText =!showText">Click me change txt</b-btn>

  <p v-if="showNumber==1">1</p>
  <p v-else-if="showTNumber==2">2</p>
  <p v-else>3</p>

  <h3>Array</h3>
  <div v-for="i,index in products" :key="i.name" :index="index">
  <p :style="'color:'+i.fontColor">{{index+1}}. Name:{{i.name}}</p>
  <p>{{i.quantity}}</p>
  <img :src="i.image">Image Source:{{i.image}}
  <p>Price: RM{{products[index].price}}</p>
</div>
  
<p>{{message}}</p>
<p>{{reversedMessage}}</p>
<p>{{allCapsMessage}}</p>

<p>{{totalPrice}}</p>


</div>
</template>

<script>

export default {
  name: "App",
  components: {},
  data() {
    return {
      counter:0,
      message:"hello",
      showText:true,

      showNumber:10,

    products: [
        {
          name: "Apple",
          quantity: 0,
          price: 10,
          stock: 0,
          image: "apple.jpg",
          url: "https://www.google.com/",
          fontColor:"green"
        },
        {
          name: "Orange",
          quantity: 3,
          price: 12,
          stock: 0,
          image: "orange.jpg",
          url: "https://www.facebook.com/",
          fontColor:"green"

        },
        {
          name: "Strawberry",
          quantity: 2,
          price: 9,
          stock: 0,
          image: "orange.jpg",
          url: "https://www.discord.com/",
          fontColor:"green"
        },
        {
          name: "Strawberry 2",
          quantity: 5,
          price: 7,
          stock: 0,
          image: "strawberry.jpeg",
          fontColor:"green"
        },
        {
          name: "Orange 2",
          quantity: 7,
          price: 13,
          stock: 0,
          image: "orange.jpg",
          fontColor:"green"
        },
        {
          name: "Apple 2",
          quantity: 9,
          price: 11,
          stock: 0,
          image: "apple.jpg",
          fontColor:"green"
        },
      ], 
   
    }
  },
  created() {
     
    },
  methods: {
  
    
  },
  computed: {
  

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
