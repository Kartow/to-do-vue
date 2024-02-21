<template>
  <Inputarea @add="addToList"/>
  <List @remove="removeFromList" @startEdit="startEdit" @doneEdit="editItem" :texts="texts"/>
</template>

<script>
import Inputarea from './components/Inputarea.vue'
import List from './components/List.vue'

export default {
  name: 'App',
  components: { Inputarea, List },
  data(){
      return{
          texts: []
      }
  },
  methods:{
    addToList(text){
      this.texts.push({
        text: text,
        status: false,
        editing: false
      })
    },
    removeFromList(index){
      this.texts.splice(index, 1)
    },
    editItem(index){
      this.texts[index].editing = !this.texts[index].editing
    },
    startEdit(index){
      this.editItem(index)
      this.$nextTick(() => {
        document.querySelector(`#edit-input-${index}`).focus()
      })
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
