<template>
    <div>
        <form class="review-form" v-on:submit.prevent="onSubmit">
            <p v-if="errors.length">
                <b>Please correct the following errors:</b>
                <ul>
                    <li v-for="error in errors" v-bind:key="error">{{error}}</li>
                </ul>
            </p>
            <p>
                <label for="name">Name:</label>
                <input id="name" v-model="name" placeholder="name"/>
               
            </p>
            <p>
                <label for="review">Review:</label>
                <textarea id="review" v-model="review" placeholder="review" ></textarea>
            </p>
            <p>
                <label for="rating">Rating:</label>
                <select id="rating" v-model.number="rating">
                    <option>5</option>
                    <option>4</option>
                    <option>3</option>
                    <option>2</option>
                    <option>1</option>
                    
                </select>
            </p>
            <p>
                <label>Would you recomend this product</label>
                <input type="radio" v-model="recommend" value="Yes">Yes
                <input type="radio" v-model="recommend" value="No">No
            </p>
            <p>
                <input type="submit" value="submit">
            </p>
        </form>
    </div>
     
</template>

<script>
export default {
    name:'ProductReview',
    data(){
        return{
            name: null,
            review: null,
            rating: null,
            recommend: null,
            errors: []
            
        }
    },
    methods:{
        onSubmit(){
            if(this.name && this.review && this.rating && this.recommend){
                    let ProductReview ={
                    name: this.name,
                    review: this.review,
                    rating: this.rating,
                    recommend: this.recommend
                }
                this.$emit('reviewSubmitted', ProductReview)
                this.name = null,
                this.review = null,
                this.rating = null,
                this.recommend = null
            }else{
                if(!this.name) this.errors.push("Name is required")
                if(!this.review) this.errors.push("Review is required")
                if(!this.rating) this.errors.push("Rating is required")
                 if(!this.recommend) this.errors.push("Recommendation is required")
            }
           

        }

    }
}
</script>