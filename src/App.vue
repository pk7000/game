<template>
<div id="app">
    <game />
</div>
</template>

<script>
import game from './components/game.vue'

export default {
    name: 'App',
    components: {
        game
    }
}
</script>

<style>
#app {
    font-family: 'Patrick Hand', cursive;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
