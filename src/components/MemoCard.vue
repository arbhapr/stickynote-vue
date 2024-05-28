<template>
    <div class="card" :style="{ backgroundColor: memo.backgroundColor }">
        <p class="card-content">
            {{ memo.memo }}
        </p>
        <div class="card-footer">
            <p class="card-date">
                {{ memo.date }}
            </p>
            <button @click="$emit('deleteMemo', memo.id)" class="card-button">x</button>
        </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
    memo: Object
})
</script>

<style>
.card {
    width: 255px;
    height: 255px;
    padding: 10px;
    margin-bottom: 20px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    color: #333;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.card-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.card-button {
    background-color: transparent;
    border: none;
    font-size: 20px;
    cursor: pointer;
    color: #e74c3c;
}
</style>