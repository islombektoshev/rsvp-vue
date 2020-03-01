<template>
    <table class="counter">
        <tbody>
        <tr>
            <td>Attending:</td>
            <td>{{total - unConfirmed}}</td>
        </tr>
        <tr>
            <td>Unconfirmed:</td>
            <td>{{unConfirmed}}</td>
        </tr>
        <tr>
            <td>Total:</td>
            <td>{{total}}</td>
        </tr>
        </tbody>
    </table>
</template>

<script>
    export default {
        name: "Stats",
        props: {
            total: Number,
            unConfirmed: Number
        }
    }
</script>

<style scoped>

</style>
<table class="counter">
    <tbody>
    <tr>
        <td>Attending:</td>
        <td>2</td>
    </tr>
    <tr>
        <td>Unconfirmed:</td>
        <td>1</td>
    </tr>
    <tr>
        <td>Total:</td>
        <td>3</td>
    </tr>
    </tbody>
</table>