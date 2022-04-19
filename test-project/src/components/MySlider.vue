<template>
  <div>
    <div class="absoluteImg2">
      <img src="@/assets/images/Group18.svg" alt="" style="right: -30%; position: relative">
    </div>
    <div class="block__button">
      <my-button-left @click="buttonPrev"></my-button-left>
      <my-button-rigth @click="buttonNext"></my-button-rigth>
    </div>
    <div class="SelfBlockSlider">
      <div :style="transformMain" class="Self">
        <div style="width: 5px; opacity: 0" ref="scrollAreaStart"></div>
        <my-user v-for="item in array" @emitInfo="emitInfo" :activeCard="activeCard" :item="item" :key="item.id"></my-user>
        <div style="width: 5px; opacity: 0" ref="scrollAreaEnd"></div>
      </div>
    </div>
  </div>
</template>

<script>
import MyButtonLeft from "@/components/UIComponents/MyButtonLeft";
import MyButtonRigth from "@/components/UIComponents/MyButtonRigth";
import MyUser from "@/components/MyUser";

export default {
  name: "MySlider",
  components:{
    MyButtonLeft,
    MyButtonRigth,
    MyUser,
  },
  data(){
    return{
      activeCard: 1,
      widthWindow: 1200,
      array: this.posts,
      endPosition: this.posts.length,
      startSlide: true,
      endSlide: true,
      valuePosition: 0,
      transformMain: {
        transform: 'translateX(0%)',
        animationName: 'slideinNext1',
      }
    }
  },
  methods:{
    emitInfo(item){
      this.$emit('emitInfo', item);
      this.activeCard = item
    },
    buttonPrev(){
        if(this.startSlide) {
          if (this.widthWindow > 1200) {
            this.valuePosition += 25
          } else if (this.widthWindow < 1200 && this.widthWindow > 600) {
            this.valuePosition += 53
          } else if (this.widthWindow <= 600) {
            this.valuePosition += 105
          }
        }
        this.endSlide = true
      },
    buttonNext(){
      if(this.endSlide){
        if(this.widthWindow > 1200){
          this.valuePosition -= 25
        }else if(this.widthWindow < 1200 && this.widthWindow > 600){
          this.valuePosition -= 53
        }else if(this.widthWindow <= 600){
          this.valuePosition -= 105
        }
      }
      this.startSlide = true
    },
    onResize() {
      this.widthWindow = window.innerWidth
    }
  },
  watch:{
    valuePosition(newLet, oldLet){
      if(newLet > oldLet){
        this.transformMain.transform = `translateX(${newLet}%)`
        this.transformMain.animationName = `slideinNext2`
      }else{
        this.transformMain.transform = `translateX(${newLet}%)`
        this.transformMain.animationName = `slideinPrevie1`
      }
    }
  },
  inject: ['posts'],
  created() {
    window.addEventListener('resize', this.onResize);
    this.onResize();
  },
  mounted() {
    let self = this
    const options = {
      rootMargin: '0px',
      threshold: 0.1
    }
    const callbackEnd = function(entries) {
      if(entries[0].isIntersecting){
        self.endSlide = false
      }
    };

    const callbackStart = function(entries) {
      if(entries[0].isIntersecting){
        self.startSlide = false
      }
    };

    const observerEnd = new IntersectionObserver(callbackEnd, options);
    const observerStart = new IntersectionObserver(callbackStart, options);
    observerEnd.observe(this.$refs.scrollAreaEnd);
    observerStart.observe(this.$refs.scrollAreaStart);
  }
}
</script>

<style scoped>

</style>