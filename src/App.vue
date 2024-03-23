<template>
  <div id="logo">
    <img src="./assets/logo.png">
  </div>
  <Inputarea @add="addToList"/>
  <List ref="List" @wrongFile="wrongFile"/>
  <Buttons @downloadTodos="downloadTodos" @importTodos="importTodos"/>
  <div class="overlay"></div>
  <div class="popup">
    <p class=close @click="closePopup">x</p>
    <h1>An error occured while importing to-do's</h1>
    <p>Check if you have uploaded the right file</p>
  </div>
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
    importTodos(file){
      this.$refs.List.importTodos(file)
    },
    wrongFile(){
      document.querySelector('.popup').style.display = 'block'
      document.querySelector('.overlay').style.display = 'block'
    },
    closePopup(){
      document.querySelector('.popup').style.display = 'none'
      document.querySelector('.overlay').style.display = 'none'
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Mukta:wght@200;300;400;500;600;700;800&display=swap');
  
$fontsize: 20px;
$mobilefontsize: 10px;
$transition: .2s all ease-in-out;

body{
  display: flex;
  flex-direction: column;
  align-items: center ;
}
#app{
  width: 40vw;
  position: absolute;
  padding-top: 50px;
  font-size: $fontsize;
  font-family: 'Mukta', sans-serif;
  input{
    font-family: 'Mukta', sans-serif;
  }
  .popup{
    display: none;
    background: rgba(255,255,255,.9);
    padding: 2%;
    width: 50%;
    position: fixed;
    top: 10%;
    left: 50%;
    transform: translateX(-50%);
    line-height: 50px;
    .close{
      position: absolute;
      top: 0;
      right: 2%;
      margin: 0;
      user-select: none;
      cursor: pointer;
      font-size: 3rem;
      transition: $transition;
      &:hover{
        text-shadow: rgba(0,0,0,.3) 0 0 10px;
      }
    }
  }
  .overlay{
    display: none;
    width: 100vw;
    height: 100vh;
    background: rgba(0,0,0,.7);
    position: fixed;
    top: 0;
    left: 0;
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
