<template>
    <div class="product">
        <div class="product-image">
            <img v-bind:src="image" v-bind="altText">
        </div>
        <div class="product-info">
            <h1>{{title}}</h1>
            <p v-if="inStock">In Stock</p>                  
            <p v-else class="outOfStock">Out of Stock</p>
            <p v-show="onSale">{{title}} on sale</p> 

            <p>Shipping: {{ shipping }}</p>  
            <ul>
                <li v-for="list in details" v-bind:key="list">{{list}}</li>
            </ul>
            <ul>
                <li v-for="size in sizes" v-bind:Key="size">{{size}}</li>
            </ul>
            <div v-for="(varient, index ) in varients" 
                 v-bind:Key="varient.varientID"
                 class="color-box"
                 v-bind:style="{backgroundColor: varient.varientColor}"
                 @mouseover="updateImage(index)">
               
            </div>
            
            <button v-on:click="addTocart" :disabled="!inStock" :class="{disabledButton: !inStock}">Add to cart</button>
            <br>
             <button v-on:click="removeCart" :disabled="!inStock" :class="{disabledButton: !inStock}">Remove from cart</button>
           
            
        </div>
        <ProductTab />
       
        
    </div>
</template>



<script>
import greensocks from '../assets/vmSocks-green-onWhite.jpg';
import bluesocks from '../assets/vmSocks-blue-onWhite.jpg';
import ProductTab from './productTab.vue';

export default {
    name:'LandingPage',
    components:{
        ProductTab
      
    },
    props:{
               premiums:{
                    type: Boolean,
                    required: true
                },
                details:{
                    type: Array,
                    required: true
                }
         }
                
            ,
    data(){
        return{
            
            brand: "Vue Mastry",
            product: 'socks',
           selectedVarient: 0,
            altText: 'Apair of socks',
           
            
            varients : [
                {
                    varientID: 1,
                    varientColor: "green",
                    varientInmage: greensocks,
                    varientQuantity : 10,
                    onSale: true
                },
                 {
                    varientID: 2,
                    varientColor: "blue",
                     varientInmage: bluesocks,
                     varientQuantity: 15,
                     onSale: false
                },
            ],
            sizes: [36,38,40,42,44],
            
           
            }     
    },
    methods: {
            addTocart: function(){
               this.$emit('add-to-cart', this.varients[this.selectedVarient].varientID)
            },
            removeCart()
            {
               this.$emit('remove-Cart', this.varients[this.selectedVarient].varientID)
            },
            updateImage: function(index){
                this.selectedVarient = index;
              
            },
           
    },
    computed:{
        title(){
            return this.brand + ' ' + this.product
        },
        image(){
            return this.varients[this.selectedVarient].varientInmage
        },
        inStock(){
            return this.varients[this.selectedVarient].varientQuantity
        },
        onSale(){
            return this.varients[this.selectedVarient].onSale
        },
        shipping(){
            
            if(this.premiums){
                return "Free";
            }else{
                return 100 + " Rs";
            }
        }
    }
}
</script>