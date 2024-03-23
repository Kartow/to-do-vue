<template>
    <div id="buttons">
        <button @click="downloadTodos">Download to-dos</button>
        <button @click="importTodos">Import to-dos</button>
        <input type="file" id="file-input" hidden>
    </div>
</template>

<script>
export default{
    methods:{
        downloadTodos(){
            this.$emit('downloadTodos')
        },
        importTodos(){
            const input = document.getElementById('file-input')
            input.click()
            input.addEventListener("change", () => {
                this.$emit('importTodos', input.files[0])
            })
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