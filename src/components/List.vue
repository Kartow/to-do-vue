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
        <li v-for="text, index in texts">
            <p class="list-index">{{ index+1 }}</p>
            <p class="list-checkbox"><input type="checkbox" v-model="text.status"></p>
            <p class="list-name">{{ text.text }}</p>
            <p class="list-status done" v-if="text.status">Done</p>
            <p class="list-status not-started" v-else>Not started</p>
            <p class="list-button"><img></p>
            <p class="list-button"><img src="../assets/bin.png" @click="remove(index)"></p>
        </li>
    </ul>
</template>

<script>
export default{
    props: ['texts'],
    methods:{
        remove(index){
            let lis = document.querySelectorAll('ul>li')
            lis[index+1].classList = 'li-remove-animation'
            lis[index+1].style.opacity = '0'
            setTimeout(()=>{
                this.$emit('remove', index)
                lis.forEach((li)=>{
                    li.classList = ''
                    li.style.opacity = '1'
                })
            }, 300)
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
        p, h4{
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