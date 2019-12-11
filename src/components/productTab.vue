<template>
    <div>
        <span 
        class="tab"
         v-for="tab in tabs" 
        :class="{activeTab: selecttedTab === tab }"
        :key="tab"
        @click="selecttedTab = tab" >{{tab}}</span>

         <div>
             <div v-show="selecttedTab === 'Reviews'">
                <h2>reviews</h2>
                <p v-if="!reviews.length">There is no reviews yet.</p>
                <ul v-else>
                    <li v-for="review in reviews" v-bind:key="review">
                        <p>{{review.name}}</p>
                        <p>{{review.review}}</p>
                        <p>{{review.rating}}</p>
                        <p>{{review.recommend}}</p>
                    </li>
                </ul>
            </div>
            <ProductReview v-show="selecttedTab === 'Make a Review'" v-on:reviewSubmitted="addReview"/>
        </div>
    </div>
    
</template>
<script>
import ProductReview from './productReview.vue'
export default {
    name:'ProductTab',
    components: {
        ProductReview
    },
    
    data(){
        return{
            tabs:['Reviews', 'Make a Review'],
            selecttedTab: 'Reviews',
            reviews:[]
        }
    },
    methods:{
         addReview(ProductReview){
              this.reviews.push(ProductReview)
            }
    }
}
</script>