<template>
    <div class="container-task">
        <p>Tasks</p>
        <hr />

        <div v-for="(tasks, index) in task" :key="index">
            <div class="list">
                <button id="btn-icon" @click="tasks.done = !tasks.done" :class="{ riscadoIcon: tasks.done, normalIcon: !tasks.done }">&#10004;</button>
                <h3 :class="{ riscado: tasks.done }">
                    {{ tasks.task }}
                </h3>
            </div>
        </div>

        <button type="button" class="btn-modal" @click="showModal = true"><div id="btn-modal-text">add task</div></button>

        <modalTasks v-if="showModal" @close="showModal = false" @passTask="getTask" />
    </div>
</template>

<script setup>
import modalTasks from './modalTasks.vue';
import { ref } from 'vue';

const icon = ref('&#10004;');
const showModal = ref(false);
const task = ref([]);
const done = ref(false);
const indexTask = ref(null);

function getTask(newTask) {
    const taskObeject = {
        task: newTask,
        done: false,
    };
    task.value.push(taskObeject);
    console.log(task.value[0], indexTask.value);
}
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
    border-left: 5px solid black;
    justify-content: flex-start;
    align-items: center;
    padding: 18px 20px;
    gap: 10px;
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
