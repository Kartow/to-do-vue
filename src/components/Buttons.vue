<template>
    <div id="buttons">
        <button @click="downloadTodos">Download to-dos</button>
        <button @click="importTodos">Import to-dos</button>
    </div>
</template>

<script>
export default{
    methods:{
        downloadTodos(){
            this.$emit('downloadTodos')
        },
        importTodos(){
            this.$emit('importTodos')
        }
    }
}
</script>

<style lang="scss">
$fontsize: 20px;
$mobilefontsize: 12px;
$transition: .2s all ease-in-out;

#buttons{
    display: flex;
    justify-content: center;
    gap: 40px;
    margin-bottom: 10px;
    button{
        border: none;
        background: none;
        border-bottom: 1px solid #ccc;
        font-size: $fontsize;
        transition: $transition;
        cursor: pointer;
        padding: 5px 0;
        &:hover{
            border-bottom: 1px solid #888;
        }
        @media (max-width: 600px){
            font-size: $mobilefontsize;
        }
    }
}
</style>