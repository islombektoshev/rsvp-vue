<template>
  <li :class="{responded:person.isConfirmed}">
    <input v-if="isEditing" type="text" v-model="person.name">
    <span v-else>{{person.name}}</span>
    <label>
      <input type="checkbox" v-model="person.isConfirmed"> Confirmed
    </label>
    <button @click="isEditing=!isEditing">{{isEditing?"save":"edit"}}</button>
    <button>remove</button>
  </li>
</template>

<script>
    export default {
        name: "Card",
        props: {
            person: {
                name: String,
                isConfirmed: Boolean,
            },
            index: Number,
        },
        data: function () {
            return {
                isEditing: false,
            };
        },
    }
</script>

<style scoped>

</style>