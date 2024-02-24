<template>
    <ul>
        <li>
            <h4 class="list-index">#</h4>
            <h4 class="list-checkbox"></h4>
            <h4 class="list-name">Name</h4>
            <h4 class="list-status">Status</h4>
            <h4 class="list-button">Edit</h4>
            <h4 class="list-button">Remove</h4>
        </li>
    </ul>
    <draggable v-model="texts" tag="ul" :animation="300">
        <template #item="{ element: text, index }">
            <li>
                <p class="list-index">{{ index+1 }}</p>
                <p class="list-checkbox"><input type="checkbox" v-model="text.status"></p>
                <input class="list-name" :id="'edit-input-'+index" type="text" v-if="text.editing" v-model="text.text" @keyup.enter="doneEdit(index)">
                <p class="list-name" v-else>{{ text.text }}</p>
                <p class="list-status done" v-if="text.status">Done</p>
                <p class="list-status not-started" v-else>Not started</p>
                <p class="list-button"><img src="../assets/pencil.png" @click="startEdit(index)"></p>
                <p class="list-button"><img src="../assets/bin.png" @click="remove(index)"></p>
            </li>
        </template>
    </draggable>
    <!-- <ul>
        <li>
            <h4 class="list-index">#</h4>
            <h4 class="list-checkbox"></h4>
            <h4 class="list-name">Name</h4>
            <h4 class="list-status">Status</h4>
            <h4 class="list-button">Edit</h4>
            <h4 class="list-button">Remove</h4>
        </li>
        <li v-for="(text, index) in texts">
            <p class="list-index">{{ index+1 }}</p>
            <p class="list-checkbox"><input type="checkbox" v-model="text.status"></p>
            <input class="list-name" :id="'edit-input-'+index" type="text" v-if="text.editing" v-model="text.text" @keyup.enter="doneEdit(index)">
            <p class="list-name" v-else>{{ text.text }}</p>
            <p class="list-status done" v-if="text.status">Done</p>
            <p class="list-status not-started" v-else>Not started</p>
            <p class="list-button"><img src="../assets/pencil.png" @click="startEdit(index)"></p>
            <p class="list-button"><img src="../assets/bin.png" @click="remove(index)"></p>
        </li>
    </ul> -->
</template>

<script>
import draggable from 'vuedraggable'

export default{
    components: { draggable },
    data(){
        return{
            texts: []
        }
    },
    methods:{
        add(text){
            this.texts.push({
                text: text,
                status: false,
                editing: false
            })
        },
        remove(index){
            let lis = document.querySelectorAll('ul>li')
            lis[index+1].classList = 'li-remove-animation'
            lis[index+1].style.opacity = '0'
            setTimeout(()=>{
                this.texts.splice(index, 1)
                lis.forEach((li)=>{
                    li.classList = ''
                    li.style.opacity = '1'
                })
            }, 300)
        },
        doneEdit(index){
            this.texts[index].editing = !this.texts[index].editing
        },
        startEdit(index){
            this.doneEdit(index)
            this.$nextTick(() => {
                document.querySelector(`#edit-input-${index}`).focus()
            })
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
        .list-index{
            flex: 0 0 5%;
        }
        .list-checkbox{
            flex: 0 0 5%;
            input{
                transform: scale(1.5);
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

</style>