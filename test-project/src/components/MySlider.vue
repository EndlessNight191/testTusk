<template>
  <div>
    <div class="block__button">
      <my-button-left @click="buttonPrev"></my-button-left>
      <my-button-rigth @click="buttonNext"></my-button-rigth>
    </div>
    <div class="SelfBlockSlider">
      <div :style="transformMain" class="Self">
        <my-user v-for="item in array" @emitInfo="emitInfo" :activeCard="activeCard" :item="item" :position="existingPosition" :key="item.id"></my-user>
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
      existingPosition: 0,
      valuePosition: 0,
      transformMain: {
        transform: 'translateX(0%)',
        animationName: '',
      }
    }
  },
  methods:{
    emitInfo(item){
      this.$emit('emitInfo', item);
      this.activeCard = item
    },
    buttonPrev(){
      if(this.widthWindow > 1200){
        if(this.existingPosition === 0){
          this.existingPosition = 6
          this.valuePosition = this.valuePosition - 150
        }else{
          this.existingPosition--
          this.valuePosition = this.valuePosition + 25
        }
      }else if(this.widthWindow < 780 && this.widthWindow > 600){
        if(this.existingPosition === 0){
          this.existingPosition = 7
          this.valuePosition = this.valuePosition - 320
        }else{
          this.existingPosition--
          this.valuePosition = this.valuePosition + 55
        }
      }else if(this.widthWindow <= 600){
        if(this.existingPosition === 0){
          this.existingPosition = 9
          this.valuePosition = this.valuePosition - 975
        }else{
          this.existingPosition--
          this.valuePosition = this.valuePosition + 110
        }
      }
    },
    buttonNext(){
      if(this.widthWindow > 1200){
        if(this.existingPosition === 6){
          this.existingPosition = 0
          this.valuePosition = this.valuePosition + 150
        }else{
          this.existingPosition++
          this.valuePosition = this.valuePosition - 25
        }
      }else if(this.widthWindow < 780 && this.widthWindow > 600){
        if(this.existingPosition === 7){
          this.existingPosition = 0
          this.valuePosition = this.valuePosition + 320
        }else{
          this.existingPosition++
          this.valuePosition = this.valuePosition - 55
        }
      }else if(this.widthWindow <= 600){
        if(this.existingPosition === 9){
          this.existingPosition = 0
          this.valuePosition = this.valuePosition + 975
        }else{
          this.existingPosition++
          this.valuePosition = this.valuePosition - 110
        }
      }
    },
    onResize() {
      this.widthWindow = window.innerWidth
    }
  },
  watch:{
    existingPosition(newLet, oldLet){
      let sum = ''

      if(this.widthWindow < 780 && this.widthWindow > 600){
        sum = 1
      }else if(this.widthWindow <= 600){
        sum = 2
      }

      if(newLet > oldLet){
        this.transformMain.transform = `translateX(${this.valuePosition}%)`
        this.transformMain.animationName = `slideinNext${sum}`
      }else{
        this.transformMain.transform = `translateX(${this.valuePosition}%)`
        this.transformMain.animationName = `slideinPrevie${sum}`
      }
    }
  },
  inject: ['posts'],
  created() {
    window.addEventListener('resize', this.onResize);
    this.onResize();
  },
}
</script>

<style scoped>

</style>