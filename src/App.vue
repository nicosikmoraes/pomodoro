<template>
    <div class="container" :style="{ 'background-color': color }">
        <timerComponent @changeColor="getColor" />
    </div>
</template>

<script setup>
import { ref } from 'vue';
import timerComponent from './components/timerComponent.vue';

const color = ref('#BA4949');

function getColor(newColor) {
    color.value = newColor;
}
</script>

<style>
* {
    font-family: 'ArialRounded', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica,
        Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';
    font-size: 15px;
    text-rendering: optimizeLegibility;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;
}

.container {
    min-height: 100vh;
    max-height: 100vw;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    color: white;
}
</style>
