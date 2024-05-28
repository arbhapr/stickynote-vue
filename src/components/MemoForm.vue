<template>
    <div class="form-overlay">
        <div class="form-modal">
            <button class="form-close-btn" @click="closeForm">&times;</button>
            <p v-if="errorMessage" class="form-error">
                {{ errorMessage }}
            </p>
            <textarea v-model="memo" cols="30" rows="10" placeholder="Write your memo here..."></textarea>
            <button class="form-save-btn" @click="saveMemo">
                Save
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
    newMemo: {
        type: String,
        required: true,
    },
})

const emit = defineEmits(['addMemo', 'closeForm'])
const memo = ref(props.newMemo)
const errorMessage = ref('')

function saveMemo() {
    if (!memo.value.trim()) {
        errorMessage.value = 'Please enter a memo'
        return
    }
    const newMemo = {
        id: Date.now(),
        memo: memo.value,
        date: new Date().toLocaleDateString("id-ID"),
        backgroundColor: getRandomColor(),
    }
    emit('addMemo', newMemo)
    memo.value = ''
    errorMessage.value = ''
}

function closeForm() {
    emit('closeForm')
}

function getRandomColor() {
    const letters = '0123456789ABCDEF'
    let color = '#'
    for (let i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)]
    }
    return color
}
</script>

<style>
.form-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
}

.form-modal {
    width: 450px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
}

.form-save-btn {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: #495a7d;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    margin-top: 15px;
    color: white;
}

.form-close-btn {
    position: absolute;
    top: 5px;
    right: 10px;
    width: 30px;
    height: 30px;
    background-color: transparent;
    border: none;
    font-size: 25px;
    cursor: pointer;
}

.form-error {
    color: red;
    margin-bottom: 10px;
}

textarea {
    width: 100%;
    font-size: 16px;
    border-radius: 5px;
    border: 1px solid #ccc;
    resize: none;
}
</style>