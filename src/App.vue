<template>
    <div id="app">
        <Book msg="Counter App" :saved="this.saved" />
    </div>
</template>

<script>
import Book from "./components/Book.vue";

export default {
    name: "App",
    data() {
        return {
            saved: [],
        };
    },
    components: {
        Book,
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
