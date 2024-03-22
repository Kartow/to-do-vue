<template>
  <div id="logo">
    <img src="./assets/logo.png">
  </div>
  <Inputarea @add="addToList"/>
  <List ref="List"/>
  <Buttons @downloadTodos="downloadTodos" @importTodos="importTodos"/>
</template>

<script>
import Inputarea from './components/Inputarea.vue'
import List from './components/List.vue'
import Buttons from './components/Buttons.vue'

export default {
  name: 'App',
  components: { Inputarea, List, Buttons },
  methods:{
    addToList(text){
      this.$refs.List.add(text)
    },
    downloadTodos(){
      this.$refs.List.downloadTodos()
    },
    importTodos(){
      this.$refs.List.importTodos()
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
  #logo{
    width: 100%;
    display: flex;
    justify-content: center;
    img{
      width: 20%;
    }
  }
  @media (max-width: 1200px){
    width: 80vw;
  }
  @media (max-width: 600px){
    font-size: $mobilefontsize;
  }
}
</style>
