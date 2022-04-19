<template>
  <div class="curentPost">
      <div class="twoBlockPosts" v-if="newExclusivePosts.length > 0">
        <div class="absoluteImg">
          <img src="@/assets/images/Group18.svg" alt="" style="right: 0%; position: relative">
        </div>
      <div style="display: flex; justify-content: flex-end; align-items: center; width: 100%">
        <img src="@/assets/images/icon.svg" alt="" class="postsPeople">
        <div class="headPosts">3 актуальных поста {{array[id-1].name}}</div>
      </div>
      <MySeparatePosts v-for="post in newExclusivePosts" :post="post" :key="post.id"/>
    </div>
  </div>
</template>

<script>

import MySeparatePosts from "@/components/MySeparatePosts";
import axios from "axios";

export default {
  name: "CurrentPostsPeople",
  components: {
    MySeparatePosts,
  },
  data(){
    return{
      peoplePosts: [],
      newExclusivePosts: [],
    }
  },
  props: {
    array: Array,
    id:{
      type: Number,
      default: 1,
      required: true,
    },
    quantityPosts:{
      type: Number,
      default: 3,
    }
  },
  async mounted() {
    await axios.get(`https://jsonplaceholder.typicode.com/posts?userId=${this.id}`)
          .then(response => {
              this.peoplePosts = response.data
              console.log('OK')
          })
          .catch(e => {
            console.log(e + 'ошибка')
          })
  },
  watch: {
      id(valueID){
       axios.get(`https://jsonplaceholder.typicode.com/posts?userId=${valueID}`)
          .then(response => {
            this.peoplePosts = response.data
            console.log('OK')
          })
          .catch(e => {
            console.log(e + 'ошибка')
          })
    },

    async peoplePosts(){
      let arr = []
      let bolen = true
      for (let i = 0; i <= this.peoplePosts.length * 2; i++) {
        let number = Math.floor(Math.random() * (9 - 0) + 0);

        for (let j = 0; j < arr.length; j++) {

          if(arr[j] === number){
            bolen = false
            return
          }
        }

        if(bolen){
          arr.push(this.peoplePosts[number])
        }
        if(arr.length === this.quantityPosts){
          break
        }
      }
      this.newExclusivePosts = arr
    }
  }
}
</script>

<style scoped>

</style>