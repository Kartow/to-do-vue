<template>
    <ul>
        <li>
            <h4 class="list-checkbox">☑️</h4>
            <h4 class="list-name">Name</h4>
            <h4 class="list-status">Status</h4>
            <h4 class="list-button">Edit</h4>
            <h4 class="list-button">Remove</h4>
        </li>
    </ul>
    <draggable v-model="texts" tag="ul" :animation="300" :disabled="isEditing">
        <template #item="{ element: text, index }">
            <li>
                <p class="list-checkbox"><input type="checkbox" v-model="text.status"></p>
                <input class="list-name" :id="'edit-input-'+index" type="text" v-if="text.editing" v-model="text.text" @keyup.enter="doneEdit(index)" @focusout="doneEdit(index)">
                <p class="list-name" v-else>{{ text.text }}</p>
                <p class="list-status done" v-if="text.status">Done</p>
                <p class="list-status not-started" v-else>Not started</p>
                <p class="list-button"><img src="../assets/pencil.png" :class="{ loweropacity: text.editing }" @click="startEdit(index)"></p>
                <p class="list-button"><img src="../assets/bin.png" @click="remove(index)"></p>
            </li>
        </template>
    </draggable>
</template>

<script>
import draggable from 'vuedraggable'

export default{
    components: { draggable },
    data(){
        return{
            texts: [],
            isEditing: false
        }
    },
    mounted(){
        this.mountLocalStorageData()
    },
    watch:{
        texts: {
            handler: function(){
                this.updateLocalStorage()
            },
            deep: true
        }
    },
    methods:{
        mountLocalStorageData(){
            const data = JSON.parse(localStorage.getItem('texts'))
            if (data){
                this.texts = data
            }
        },
        updateLocalStorage(){
            localStorage.setItem('texts', JSON.stringify(this.texts))
        },
        getData(){
            let data = JSON.parse(localStorage.getItem('texts'))
            if(data){
                return data
            }
            return false
        },
        add(text){
            let data = this.getData()
            data = (data != false) ? data : []
            data.push({
                text: text,
                status: false,
                editing: false
            })
            data = JSON.stringify(data)
            localStorage.setItem('texts', data)
            this.mountLocalStorageData()
        },
        remove(index){
            let lis = document.querySelectorAll('ul>li')
            lis[index+1].classList = 'li-remove-animation'
            lis[index+1].style.opacity = '0'
            setTimeout(()=>{
                this.texts.splice(index, 1)
                this.updateLocalStorage()
                lis.forEach((li)=>{
                    li.classList = ''
                    li.style.opacity = '1'
                })
            }, 300)
        },
        doneEdit(index){
            this.texts[index].editing = false
            let editingCount = false
            this.texts.forEach((text) => {
                if (text.editing){
                    editingCount = true
                }
            })
            if(editingCount){
                this.isEditing = true
            } else {
                this.isEditing = false
            }
            this.updateLocalStorage()
        },
        startEdit(index){
            if(this.texts[index].editing){
                this.doneEdit(index)
            } else {
                this.texts.forEach((text) => {
                    text.editing = false
                })
                this.texts[index].editing = true
                this.$nextTick(() => {
                    document.querySelector(`#edit-input-${index}`).focus()
                })
                this.isEditing = true
            }
        },
        downloadTodos(){
            const blob = new Blob([JSON.stringify(this.texts)], { type: 'application/json' })
            const url = URL.createObjectURL(blob)
            const a = document.createElement('a')
            a.href = url
            a.download = 'todos.json'
            a.click()
            a.remove()
            console.log(blob)
        },
        importTodos(file){
            const reader = new FileReader()
            reader.readAsText(file, "UTF-8")
            reader.onload = evt => {
                if(file.type === "application/json"){
                    console.log(evt.target.result)
                    this.texts = JSON.parse(evt.target.result)
                } else {
                    this.$emit('wrongFile')
                }
            }
            reader.onerror = evt => {
                this.$emit('wrongFile')
            }
        }
    }
}
</script>

<style lang="scss" scoped>
$fontsize: 20px;

@keyframes remove {
    0% {opacity: 1;}
    100% {opacity: 0;}
}

ul{
    width: 100%;
    list-style-type: none;
    padding: 0;
    li{
        display: flex;
        text-align: center;
        vertical-align: middle;
        width: 100%;
        min-height: 60px;
        justify-content: space-between;
        border-bottom: 1px solid #ccc;
        opacity: 1;
        p, h4, input[type=text]{
            word-break: break-all;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            img{
                height: 30px;
                cursor: pointer;
            }
        }
        input[type=text]{
            border: none;
            font-size: 1rem;
            text-align: center;
            font-size: $fontsize;
            padding: 0;
            width: 0;
        }
        .list-checkbox{
            flex: 0 0 10%;
            input{
                transform: scale(2);
            }
        }
        .list-name{
            flex: 0 0 40%;
        }
        .list-status{
            flex: 0 0 20%;
        }
        .list-button{
            flex: 0 0 15%;
        }
        .done{
            color: forestgreen;
        }
        .not-started{
            color: crimson;
        }
    }
}

.li-remove-animation{
    animation: remove .3s ease-out;
}

.loweropacity{
    opacity: .3;
}

</style>