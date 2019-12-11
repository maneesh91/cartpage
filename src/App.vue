<template>
  <div id="app">
    <NavBar />
    <div class="cart">
                <p>Cart {{cart.length}}</p>
    </div>
    <LandingPage v-bind:premiums="premium" :details="details" @add-to-cart="updateCart" @remove-Cart ="RemoveCart"></LandingPage>
    
   
  </div>
</template>

<script>
import NavBar from './components/navbar.vue'
import LandingPage from './components/landingpage.vue'
import('./design/style.css')


export default {
  name: 'App',
  components: {
    NavBar,
    LandingPage
  },
  data(){
    return{
      premium: true,
      details : ["80% cotton", "20% polyyester", "Gender-neutral"],
      cart: [],
    }
  },
  methods:{
    updateCart(id){
      this.cart.push(id)
    },
    RemoveCart(id){
      for(var i = this.cart.length-1; i >= 0; i--){
        if(this.cart[i] === id){
          this.cart.splice(i,1)
        }
      }
    }
  }
}
</script>


