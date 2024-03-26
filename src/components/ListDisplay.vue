<script>
    export default {
        name: "ListDisplay",
        components: {},
        props: {
            list: Array
        },
        data: function () {
            return {
            }
        },
        mounted () {
        },
        methods: {
        },
    }
</script>

<template>
    <h1 v-for="listItem in list">{{ listItem }}</h1>
</template>

<style scoped>
    .container {
        width: 100%;
        min-height: 100%;
        border: 1px solid lightgrey;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 20px;
        position: relative
    }

    .AddItemModal {
        max-width: 1200px;
        background-color: white;
    }
    .AddItemModalContainer {
        width: 100%;
        height: 100%;
        background-color: rgba(0,0,0,0.2);
        position: absolute;
        top: 0;
        left: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 40px;
    }
    .newItemTextBox {
    width: 90%;
    max-width: 500px;
    padding: 10px;
    outline: none;
  }
</style>