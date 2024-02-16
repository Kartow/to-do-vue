<template>
  <Inputarea @add="addToList"/>
  <List @remove="removeFromList" :texts="texts"/>
</template>

<script>
import Inputarea from './components/Inputarea.vue'
import List from './components/List.vue'

export default {
  name: 'App',
  components: { Inputarea, List },
  data(){
      return{
          texts: [],
          todosAmount: 0
      }
  },
  methods:{
    addToList(text){
      this.todosAmount++
      this.texts.push({
        text: text,
        status: false,
        index: this.todosAmount
      })
    },
    removeFromList(index){
      this.texts.splice(index, 1)
    }
  }
}
</script>

<style lang="scss">
$fontsize: 20px;
$mobilefontsize: 10px;
#app{
  width: 40vw;
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  font-size: $fontsize;
  @media (max-width: 1200px){
    width: 90vw;
  }
  @media (max-width: 600px){
    font-size: $mobilefontsize;
  }
}
</style>
