<template>
    <div id="inputarea">
        <input type="text" v-model="text" placeholder="Write here" @keyup.enter="add">
        <img @click="add" src="../assets/send_black.png">
    </div>
</template>

<script>
export default{
    data(){
        return{
            text: ''
        }
    },
    methods:{
        add(){
            this.$emit('add', this.text)
            this.text = ''
        }
    }
}
</script>

<style lang="scss">
$fontsize: 20px;
$mobilefontsize: 12px;
$transition: .2s all ease-in-out;

#inputarea{
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 5px;
    height: 50px;
    width: 100%;
    input{
        border: none;
        border-bottom: 1px solid #ccc;
        background: none;
        width: 90%;
        height: 90%;
        font-size: $fontsize;
        transition: $transition;
        &:focus, &:hover{
            outline: none;
            border-bottom: 1px solid #888;
        }
        @media (max-width: 600px){
            font-size: $mobilefontsize;
        }
    }
    img{
        height: 90%;
        cursor: pointer;
        transition: $transition;
        &:hover{
            transform: translateX(3px);
        }
    }
    }
    
</style>