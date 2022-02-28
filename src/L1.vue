<template>
  <div id="app">
      <h2 class="greenFont">My first ever Vue Tutorial</h2>

      <h4 class="blueFont">{{ message }}</h4>

      Name:<input type="text" v-model="name"/> <br> 
      Addr:<input type="text" v-model="addr"/> <br> 
      Email:<input type="text" v-model="email"/> <br> 
      Tel:<input type="text" v-model="tel"/>  <br><br>

      <h2>Name : {{ name }}</h2>
      <h3>Addr :{{ addr }}</h3>
      <h3>Email: {{ email }}</h3>
      <h3>Tel: {{ tel }}</h3>

    <button class="greenFont" @click="increase"> +1</button>
    <button class="redFont" @click="decrease"> -1</button>
    <br>
    <button class="greenFont" @click="increase5"> +5</button>
    <button class="redFont" @click="decrease5"> -5</button>

    <h2> {{counter}}</h2>
    <br>
    <img v-bind:src="image1">
    <img :src="image2">
    <img :src="image3">
    <br>
    <button v-if="!user" @click="logIn">logIn</button>
    <button v-if="user" @click="logOut">LogOut</button>
    <button @click="getStats">getStats</button>

    <ul id="gas-stats"></ul>
  


</div>
</template>

<script>
import Moralis from 'moralis'
export default {
  name: "App",
  components: {},
  data() {
    return {
      message: "Please enter your details below",
      name: "",
      addr: "",
      email: "",
      tel: "",
      image1: "apple.jpg",
      image2: "orange.jpg",
      image3: "strawberry.jpg",
      url1: "https://apple.com",
      url2: "https://orange.com",
      url3: "https://abc.com",
      web1: "Fruit Company",
      web2: "Orange Company",
      web3: "Another Fruit Company",
      counter: 0, 
      user:null
    }
  },
  created() {
      Moralis.initialize("N57ODjzkI15fX5kSZjmM0YHXbtLGSLOCrekbhgiD");
      Moralis.serverURL = "https://hpzry1kums8f.usemoralis.com:2053/server";
      Moralis.start();
    },
  methods: {
    increase() {
      this.counter = this.counter + 1;
    },
    decrease() {
      this.counter = this.counter - 1;
    },
    increase5() {
      this.counter = this.counter + 5;
    },
    decrease5() {
      this.counter = this.counter - 5;
    },
    //new lesson
    async logIn() {
      this.user = Moralis.User.current();
      if (!this.user) {
        this.user = await Moralis.authenticate();
      }
      console.log("logged in user:", this.user);
    },
    async logOut() {
      await Moralis.User.logOut();
      this.user = null
      console.log("logged out");
    },
    getStats() {
      const user = Moralis.User.current();
      if (user) {
          this.getUserTransactions(user);
        }
          this.getAverageGasPrices();
      },
    async getUserTransactions(user){
        // create query
        const query = new Moralis.Query("EthTransactions");
        query.equalTo("from_address", user.get("ethAddress"));

        // run querys
        const results = await query.find();
        console.log("user transactions:", results);
      },
      // CLOUD FUNCTION
      async getAverageGasPrices(){
        const results = await Moralis.Cloud.run("getAvgGas");
        console.log("average user gas prices:", results);
        
      }
    
  },
  computed: {},
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
