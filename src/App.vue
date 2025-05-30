<template>
    <div class="container" :style="{ 'background-color': color }">
        <timerComponent @changeColor="getColor" @pomodoros="getPomodoros" />
        <tasksComponent ref="taskComponent" />
    </div>
</template>

<script setup>
import { ref } from 'vue';
import timerComponent from './components/timerComponent.vue';
import tasksComponent from './components/tasksComponent.vue';

const color = ref('#BA4949');
const taskComponent = ref(null);

function getColor(newColor) {
    color.value = newColor;
    taskComponent.value.changeColor(color.value);
}

function getPomodoros() {
    taskComponent.value.changePomodoros();
}
</script>

<style>
* {
    font-family: 'ArialRounded', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
        'Segoe UI Symbol';
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
    transition: 0.2s;
    padding: 40px;
}
</style>
