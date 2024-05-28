<template>
    <div class="card-container">
        <MemoCard v-for="memo in memos" :key="memo.id" :memo="memo" @deleteMemo="handleDeleteMemo" />
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';
import MemoCard from './MemoCard.vue'

const emit = defineEmits(['deleteMemo'])
const props = defineProps({
    memos: [],
})

function handleDeleteMemo(memoId) {
    emit('deleteMemo', memoId)
}
</script>

<style scoped>
.card-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}
</style>