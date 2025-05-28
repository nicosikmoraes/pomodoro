<template>
    <div class="container-timer" :style="{ 'background-color': color }">
        <div class="container-buttons">
            <button
                type="button"
                id="btn-pomodoro"
                class="btn"
                :class="{ 'btn-active1': selected === 'pomodoro' }"
                @click="
                    (selected = 'pomodoro'),
                        (color = '#C15C5C'),
                        (mainColor = '#BA4949'),
                        (newTime = 25 * 60),
                        (newColor = '#BA4949');
                    changeColor();
                    changeColor();
                "
            >
                Pomodoro
            </button>

            <button
                type="button"
                id="btn-short"
                class="btn"
                :class="{ 'btn-active2': selected === 'short' }"
                @click="
                    (selected = 'short'),
                        (color = '#4c9196'),
                        (mainColor = '#38858a'),
                        (newTime = 5 * 60),
                        (newColor = '#38858a');
                    changeColor();
                    changeColor();
                "
            >
                Short Break
            </button>
            <button
                type="button"
                id="btn-long"
                class="btn"
                :class="{ 'btn-active3': selected === 'long' }"
                @click="
                    (selected = 'long'),
                        (color = '#4d7fa2'),
                        (mainColor = '#397097'),
                        (newTime = 15 * 60),
                        (newColor = '#397097');
                    changeColor();
                    changeColor();
                "
            >
                Long Break
            </button>
        </div>
        <cronometroComponent :newTime="newTime" :newColor="newColor" ref="changeTimeFunction" />
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
    changeTimeFunction.value?.changeTime();
}
</script>

<style>
.container-timer {
    width: 450px;
    height: 350px;
    border-radius: 6px;
    margin-top: 13vh;
}

.container-buttons {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin-top: 20px;
    gap: 10px;
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
