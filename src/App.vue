<template>
  <Inputarea @add="addToList"/>
  <List ref="List"/>
</template>

<script>
import Inputarea from './components/Inputarea.vue'
import List from './components/List.vue'

export default {
  name: 'App',
  components: { Inputarea, List },
  methods:{
    addToList(text){
      this.$refs.List.add(text)
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Mukta:wght@200;300;400;500;600;700;800&display=swap');

$fontsize: 20px;
$mobilefontsize: 10px;
#app{
  width: 40vw;
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  font-size: $fontsize;
  font-family: 'Mukta', sans-serif;
  input{
    font-family: 'Mukta', sans-serif;
  }
  @media (max-width: 1200px){
    width: 90vw;
  }
  @media (max-width: 600px){
    font-size: $mobilefontsize;
  }
}
</style>
