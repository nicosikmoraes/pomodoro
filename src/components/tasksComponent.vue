<template>
    <div class="container-task">
        <p>Tasks</p>
        <hr />

        <div v-for="(tasks, index) in task" :key="index">
            <div class="list" @click="tasks.select = !tasks.select" :class="{ selectedTask: tasks.select }">
                <button
                    id="btn-icon"
                    @click="(tasks.done = !tasks.done), (tasks.select = !tasks.select)"
                    :class="{ riscadoIcon: tasks.done, normalIcon: !tasks.done }"
                >
                    <i class="bi bi-check"></i>
                </button>

                <h3 :class="{ riscado: tasks.done }">{{ tasks.task }}</h3>

                <div class="pomodoros-made">
                    <h2>{{ madePomodoros }}/{{ tasks.pomodorosTotal }}</h2>
                    <i id="delete-icon" class="bi bi-trash" @click="deleteTask(tasks.id)"></i>
                </div>
            </div>
        </div>

        <button type="button" class="btn-modal" @click="showModal = true" :style="{ 'background-color': color }">
            <div id="btn-modal-text">add task</div>
        </button>

        <modalTasks v-if="showModal" @close="showModal = false" @passTask="getTask" />
    </div>
</template>

<script setup>
import modalTasks from './modalTasks.vue';
import { ref } from 'vue';
import { defineExpose } from 'vue';

const showModal = ref(false);
const task = ref([]);
const color = ref('#BA4949');
const idTask = ref(0);
const madePomodoros = ref(0);

function getTask(newTask, pomodoros) {
    const taskObeject = {
        task: newTask,
        done: false,
        id: idTask.value++,
        pomodorosTotal: pomodoros,
        select: false,
    };
    task.value.push(taskObeject);
}

function deleteTask(id) {
    task.value = task.value.filter((task) => task.id !== id);
}

function changeColor(newColor) {
    color.value = newColor;
}

function changePomodoros(pomodorosMade) {
    madePomodoros.value = pomodorosMade;
    console.log('Pomodoros made', madePomodoros.value);
}

defineExpose({
    changeColor,
    changePomodoros,
});
</script>

<style scoped>
.container-task {
    width: 530px;
    margin-top: 35px;
}

.list {
    background-color: white;
    margin-top: 12px;
    display: flex;
    color: rgb(85, 85, 85);
    width: 100%;
    border-radius: 4px;
    font-size: 16px;
    box-sizing: border-box;
    justify-content: flex-start;
    align-items: center;
    padding: 18px 20px;
    gap: 10px;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 4px;
}

.list:hover {
    border-left: 5px solid rgb(177, 177, 177);
}

.selectedTask {
    border-left: 5px solid black;
    transform: translateY(2px);
    box-shadow: none;
}

.riscado {
    text-decoration: line-through;
    color: rgb(85, 85, 85);
    opacity: 0.5;
}

.normalIcon {
    background-color: rgb(230, 230, 230);
}

.riscadoIcon {
    background-color: #ab4343;
}

#btn-icon {
    font-size: 25px;
    color: white;
    width: 32px;
    height: 32px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 100px;
    cursor: pointer;
    border: none;
}

p {
    font-size: 20px;
    font-weight: bold;
    margin-bottom: 15px;
}

h3 {
    font-size: 18px;
    font-weight: bold;
}

h2 {
    font-size: 20px;
    opacity: 0.8;
}

i {
    font-size: 28px;
}

.pomodoros-made {
    margin-left: auto;
    display: flex;
    gap: 26px;
    align-items: center;
}

#delete-icon {
    font-size: 23px;
    margin-left: auto;
    cursor: pointer;
}

.btn-modal {
    box-sizing: border-box;
    background-color: #ab4343;
    border: 2px dashed rgba(255, 255, 255, 0.4);
    width: 100%;
    height: 64px;
    border-radius: 8px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    opacity: 0.8;
    margin-top: 12px;
    color: white;
    transition: 0.3s;
}

#btn-modal-text {
    opacity: 0.8;
    font-size: 20px;
    font-weight: bold;
    transition: 0.3s;
}

.btn-modal:hover #btn-modal-text {
    opacity: 1;
}
</style>
