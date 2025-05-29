<template>
    <div class="container-timer" :style="{ 'background-color': color }">
        <div class="container-buttons">
            <button type="button" id="btn-pomodoro" class="btn" @click="pomodoro()" :class="{ 'btn-active1': selected === 'pomodoro' }">Pomodoro</button>

            <button type="button" id="btn-short" class="btn" @click="short()" :class="{ 'btn-active2': selected === 'short' }">Short Break</button>
            <button type="button" id="btn-long" class="btn" @click="long()" :class="{ 'btn-active3': selected === 'long' }">Long Break</button>
        </div>
        <cronometroComponent
            :newTime="newTime"
            :newColor="newColor"
            ref="changeTimeFunction"
            @changePagePomodoro="pomodoro"
            @changePageShort="short"
            @changePageLong="long"
        />
    </div>
</template>

<script setup>
import { ref } from 'vue';
import cronometroComponent from './cronometroComponent.vue';

const emit = defineEmits(['changeColor']);
const changeTimeFunction = ref(null);

const newTime = ref(25 * 60);
const newColor = ref('#BA4949');
const mainColor = ref('');
const color = ref('#C15C5C');
const selected = ref('pomodoro');

function changeColor() {
    emit('changeColor', mainColor.value);
    changeTimeFunction.value.changeTime(newTime.value, newColor.value);
}

function pomodoro() {
    (selected.value = 'pomodoro'), (color.value = '#C15C5C'), (mainColor.value = '#BA4949'), (newTime.value = 25 * 60), (newColor.value = '#BA4949');
    changeColor();
    console.log('Pomodoro', newTime.value);
}

function short() {
    (selected.value = 'short'), (color.value = '#4c9196'), (mainColor.value = '#38858a'), (newTime.value = 5 * 60), (newColor.value = '#38858a');
    changeColor();
    console.log('Short', newTime.value);
}

function long() {
    (selected.value = 'long'), (color.value = '#4d7fa2'), (mainColor.value = '#397097'), (newTime.value = 15 * 60), (newColor.value = '#397097');
    changeColor();
    console.log('Long', newTime.value);
}
</script>

<style scoped>
.container-timer {
    width: 535px;
    height: 350px;
    border-radius: 6px;
    margin-top: 6vh;
    transition: 0.2s;
}

.container-buttons {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin-top: 20px;
    gap: 10px;
    transition: 0.2s;
}

.btn {
    border: 0px;
    color: white;
    font-size: 16px;
    padding: 4px 12px;
    width: 110px;
    height: 30px;
    border-radius: 6px;
    cursor: pointer;
    background-color: transparent;
    transition: 0.2s;
}

.btn-active1 {
    font-weight: bold;
    background-color: #a44e4e;
}

.btn-active2 {
    font-weight: bold;
    background-color: #417b80;
}

.btn-active3 {
    font-weight: bold;
    background-color: #426c8a;
}
</style>
