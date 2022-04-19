<template>
  <div class="postUser">
    <img :src="imageData" @click="emitInfo" :class="[activeCard === item.id ? 'imgUserActive' : 'imgUser']"/>
    <div :class="[activeCard === item.id ? 'cardNameActive' : 'cardName']">{{item.name}}</div>
    <div :class="[activeCard === item.id ? 'cardNameComapnyAvtive' : 'cardNameComapny']">{{item.company.name}}</div>
  </div>
</template>

<script>

export default {
  name: "MyUser",
  props:{
    item: Object,
    activeCard: {
      type: Number,
      default: 1,
    },
  },
  data(){
    return{
      change: false,
      imageData: "https://i.pravatar.cc/150?img=" + this.item.id,
    }
  },
  methods:{
    emitInfo(){
      this.$emit('emitInfo', this.item.id)
    },
  },
}
</script>

<style scoped>

</style>