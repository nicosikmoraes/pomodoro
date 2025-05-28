<template>
    <div class="container-cronometro">
        <h1>{{ formatarTempo(time) }}</h1>
        <button
            type="button"
            @click="startTimer()"
            v-show="!activated"
            :style="{ color: btnColor }"
        >
            Start
        </button>
        <button type="button" @click="pauseTimer()" v-show="activated">Stop</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
    newTime: Number,
    newColor: String,
});

const time = ref(25 * 60);
const activated = ref(false);
const btnColor = ref('#BA4949');
let breakTimer = null;

function startTimer() {
    if (!activated.value) {
        activated.value = true;
        breakTimer = setInterval(() => {
            if (time.value > 0) {
                time.value--;
            } else {
                pause();
                alert('Fim do Pomodoro');
            }
        }, 1000);
    }
}

function pauseTimer() {
    if (activated.value) {
        activated.value = false;
        clearInterval(breakTimer);
    }
}

function changeTime() {
    time.value = props.newTime;
    btnColor.value = props.newColor;
    console.log('Change Time Função');
}

defineExpose({
    changeTime,
});

function formatarTempo(segundos) {
    const min = Math.floor(segundos / 60)
        .toString()
        .padStart(2, '0');
    const seg = (segundos % 60).toString().padStart(2, '0');
    return `${min}:${seg}`;
}
</script>

<style scoped>
.container-cronometro {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-top: 20px;
    width: 100%;
    height: 77%;
}

h1 {
    font-size: 120px;
}

button {
    background-color: white;
    border: 0px;
    color: #c15c5c;
    font-weight: bold;
    border-radius: 4px;
    box-shadow: rgb(235, 235, 235) 0px 6px 0px;
    font-size: 22px;
    height: 55px;
    padding: 0px 12px;
    width: 200px;
    cursor: pointer;
}

button:hover {
    background-color: rgb(230, 230, 230);
}
</style>
