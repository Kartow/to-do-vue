<template>
    <div>
        <h1>{{ title }}</h1>
        <div id="okno">
            <h1>{{ text }}</h1>
        </div>
    </div>
</template>

<script>
export default{
    props: ['text'],
    data(){
        return{
            title: 'Tytuł'
        }
    }
}
</script>

<style lang="scss" scoped>
$divbg: lightblue;
$titlecolor: darkblue;
$textfontsize: 10px;

h1{
    font-size: 20px;
}

#okno{
    background: $divbg;
    h1{
        color: $titlecolor;
        font-size: $textfontsize;
    }
}
</style>