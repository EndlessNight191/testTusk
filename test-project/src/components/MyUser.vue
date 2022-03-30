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
    position: Number,
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
/*  async created() {
    const config = {
        responseType: 'arraybuffer'
    };

    axios.get(`https://i.pravatar.cc/150?img=${this.item.id}`, config)
    .then(response => {
      let img = btoa(response.data);
      console.log(img)
      this.imageData = 'data:image/jpeg;base64,' + img;
      console.log(this.imageData)
    })
  }*/
}
</script>

<style scoped>

</style>