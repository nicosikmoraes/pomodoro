<template>
    <!-- Essa div é do fundo do modal -->
    <div class="modal-backdrop" @click.self="$emit('close')">
        <div class="modal-content">
            <input type="text" placeholder="What are you working on?" class="input-modal" v-model="taskMessage" />

            <div class="pomodoros-counter">
                <p>Est pomodoros</p>
                <div class="input-pomodoros">
                    <input id="value-pomodoros" type="number" value="1" />
                </div>
            </div>
        </div>

        <div class="modal-footer">
            <button type="button" class="btn-modal-close" @click="$emit('close')">Cancel</button>
            <button type="button" class="btn-modal-save" @click="getTask(), $emit('close')">Save</button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['passTask']);

const taskMessage = ref('');

function getTask() {
    passTask();
    taskMessage.value = '';
}

function passTask() {
    emit('passTask', taskMessage.value);
}
</script>

<style scoped>
.modal-content {
    padding: 10px 20px 0px;
    width: 100%;
    background-color: white;
    border-radius: 8px;
    border-bottom-left-radius: 0px;
    border-bottom-right-radius: 0px;
    margin-top: 12px;
    text-align: left;
    box-shadow: rgba(0, 0, 0, 0.15) 0px 10px 20px, rgba(0, 0, 0, 0.1) 0px 3px 6px;
    animation: 0.1s ease-in-out 0s 1 normal none running expand;
}

.modal-footer {
    padding: 14px 20px;
    text-align: right;
    border-bottom-left-radius: 8px;
    border-bottom-right-radius: 8px;
    background-color: rgb(239, 239, 239);
    display: flex;
    justify-content: flex-end;
    align-items: center;
    gap: 10px;
}

.input-modal {
    border-radius: 4px;
    font-size: 22px;
    font-style: italic;
    padding: 10px 0px;
    box-shadow: none;
    border: none;
    color: rgb(85, 85, 85);
    width: 100%;
    box-sizing: border-box;
    font-weight: bold;
}

input::placeholder {
    opacity: 0.5;
}

.input-modal:focus,
#value-pomodoros:focus {
    outline: none;
}

.pomodoros-counter {
    margin-top: 10px;
}

p {
    color: rgb(85, 85, 85);
    font-weight: bold;
    font-size: 16px;
}

#value-pomodoros {
    border-radius: 6px;
    background-color: rgb(239, 239, 239);
    font-size: 16px;
    padding: 10px;
    box-shadow: none;
    color: rgb(85, 85, 85);
    width: 75px;
    box-sizing: border-box;
    font-weight: bold;
    margin-top: 10px;
    border: none;
    margin-bottom: 20px;
}

.btn-modal-close {
    border-radius: 4px;
    background-color: transparent;
    color: rgb(136, 136, 136);
    border: none;
    box-shadow: none;
    width: 70px;
    padding: 8px 12px;
    cursor: pointer;
    text-align: center;
    opacity: 0.9;
    font-weight: bold;
}

.btn-modal-close:hover {
    opacity: 1;
    font-weight: bold;
}

.btn-modal-save {
    text-align: center;
    border-radius: 4px;
    cursor: pointer;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 2px 2px;
    color: white;
    opacity: 0.9;
    font-size: 14px;
    padding: 8px 12px;
    width: 70px;
    background-color: rgb(34, 34, 34);
    border: 2px solid rgb(34, 34, 34);
}

.btn-modal-save:hover {
    opacity: 1;
}
</style>
