<template>
    <div class="container-cronometro">
        <h1>{{ formatarTempo(time) }}</h1>
        <div class="container-btn">
            <div class="bnt-event">
                <button type="button" @click="startTimer()" v-show="!activated" :style="{ color: btnColor }">Start</button>

                <button type="button" @click="pauseTimer()" v-show="activated" :style="{ color: btnColor }">Stop</button>
            </div>

            <button id="btn-end" type="button" @click="endTime()" :style="{ color: btnColor }">End</button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['changePagePomodoro', 'changePageShort', 'changePageLong', 'pomodoros']);

const time = ref(25 * 60);
const activated = ref(false);
const btnColor = ref('#BA4949');
const countPause = ref(0);
const madePomodoros = ref(0);
let breakTimer = null;

function startTimer() {
    if (!activated.value) {
        activated.value = true;
        breakTimer = setInterval(() => {
            if (time.value > 0) {
                time.value--;
            } else {
                pauseTimer();
                changePage();
                console.log('ChangePage');
            }
        }, 1000);
    }
}

function pauseTimer() {
    if (activated.value) {
        activated.value = false;
        clearInterval(breakTimer);
        console.log('Pause');
    }
}

function endTime() {
    time.value = 0;
}

function changeTime(newTime, newColor) {
    time.value = newTime;
    btnColor.value = newColor;
    pauseTimer();
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

function changePage() {
    console.log('changePage Função');
    if (time.value === 0 && btnColor.value === '#BA4949' && countPause.value < 3) {
        madePomodoros.value++;
        emit('changePageShort');
        emit('pomodoros', madePomodoros.value);
        countPause.value++;
    } else if (time.value === 0 && btnColor.value === '#BA4949' && countPause.value >= 3) {
        madePomodoros.value++;
        emit('changePageLong');
        emit('pomodoros', madePomodoros.value);
        countPause.value = 0;
    } else if (time.value === 0) {
        emit('changePagePomodoro');
    }
    console.log(countPause.value);
}
</script>

<style scoped>
.container-cronometro {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-top: 5px;
    width: 100%;
    height: 77%;
}

.container-btn {
    margin-top: 10px;
    display: flex;
    gap: 15px;
}

h1 {
    font-size: 120px;
}

#btn-end {
    background-color: white;
    border: 0px;
    color: #c15c5c;
    font-weight: bold;
    border-radius: 4px;
    box-shadow: rgb(235, 235, 235) 0px 6px 0px;
    font-size: 22px;
    width: 100px;
    transition: 0.5s;
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
    transition: 0.5s;
}

button:hover,
#btn-end:hover {
    background-color: rgb(230, 230, 230);
}
</style>
