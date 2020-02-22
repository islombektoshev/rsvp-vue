<template>
    <div>
        <form @submit="addPerson">
            <input type="text" name="name" v-model="name">
        </form>
        <h1>{{"People"}}</h1>
        <ul style="display: flex; justify-content: center">
            <li v-for="(p,i) in people" :key="i">
                <People :name="p.name" :id="i" @delete-people="removePerson"></People>
            </li>
        </ul>
    </div>
</template>

<script>
    import Person from "./Person";
    import People from "./People";

    export default {
        name: 'HelloWorld',
        components: {People},
        props: {
            msg: String
        },
        data: function () {
            return {
                people: [],
                name:""
            };
        },
        methods: {
            addPerson(e){
                console.log(this);
                e.preventDefault();
                let p = new Person(1, e.target.name.value);
                console.log(p);
                this.people.push(p);
                this.name="";
            },
            removePerson(i){
                this.people.splice(i,1);
            },
        },

    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
