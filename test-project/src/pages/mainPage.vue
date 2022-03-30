<template>
  <div style="max-width: 90%; margin: 0px auto; overflow: hidden">
    <img src="@/assets/images/Group18.svg" alt="" class="absoluteImg">
    <div class="absoluteImg2">
      <img src="@/assets/images/Group18.svg" alt="" style="right: -30%; position: relative">
    </div>
    <my-header/>
    <my-slider v-if="array.length > 1" @emitInfo="emitInfo"/>
    <CurrentPostsPeople :array="array" :id="idPeople" style="margin-bottom: 125px"/>
  </div>
</template>

<script>
import myHeader from '@/components/myHeader';
import MySlider from "@/components/MySlider";
import CurrentPostsPeople from "@/components/CurrentPostsPeople";
import axios from 'axios';
import { computed } from 'vue'

export default {
  name: "mainPage",
  components: {
    myHeader,
    MySlider,
    CurrentPostsPeople,
  },
  data(){
    return{
      array: [],
      idPeople: 1,
    }
  },
  methods:{
    emitInfo(item){
      console.log(item)
      this.idPeople = item
    }
  },
  provide() {
    return {
      posts: computed(() => this.array),
    }
  },
  async created() {
    await axios.get('https://jsonplaceholder.typicode.com/users')
          .then(response => {
            this.array = response.data
          })
          .catch(e => {
            this.array.push(e)
          })
  }
}
</script>

<style scoped>

</style>