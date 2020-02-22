<template>
    <div>
        <span>Id: </span><span>{{id}}</span><br>
        <span>Name: </span> <span>{{name}}</span>
        <p><span>Age: </span><span>{{age}}</span></p>
        <button @click="age+=1">+</button> : <button @click="age-=1">-</button>
        <button @click="$emit('delete-people',id)">X</button>
    </div>
</template>

<script>
    export default {
        props: {
            name: String,
            id: Number
        },
        name: "People",
        data: function () {
            console.log("on data");
            return {
                age: Math.round(Math.random() * 50)
            };
        }
    }
</script>

<style scoped>
    div{
        border: black 3px solid;
        padding: 10px;
        border-radius: 5px;
        margin: 10px;
        background: antiquewhite;

    }
</style>