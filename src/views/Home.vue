<template>
  <div class="home">
    <div class="box1">
      <new-juese/>
      <new-juese/>
      <new-juese/>
      <new-juese/>
      <new-juese/>
      <new-juese/>
      <new-juese/>
      <new-juese/>
      
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import newJuese from '../components/newjuese.vue'

export default {
  components:{
      newJuese,
  },
  
  
}
</script>
<style scoped>
.box1{
  margin: 0 0 0 60px;
}
</style>