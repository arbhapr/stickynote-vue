<template>
  <main>
    <div class="container">
      <header>
        <h1 class="header-title">Memo</h1>
        <button class="header-btn" @click="showForm = true">+</button>
      </header>
      <MemoList
        :memos="memos"
        @deleteMemo="deleteMemo"
      />
    </div>
    <MemoForm
      v-if="showForm"
      :newMemo="newMemo"
      @addMemo="addMemo"
      @closeForm="showForm = false"
    />
  </main>
</template>

<script setup>
import { ref } from 'vue'
import MemoForm from './components/MemoForm.vue'
import MemoList from './components/MemoList.vue'

const showForm = ref(false)
const newMemo = ref('')
const memos = ref([])

function addMemo(memo) {
  memos.value.push(memo)
  newMemo.value = ''
  showForm.value = false
}

function deleteMemo(id) {
  memos.value = memos.value.filter(memo => memo.id !== id)
}

</script>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
  font-family: Arial, Helvetica, sans-serif;
}

.container {
  max-width: 900px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header-title {
  font-size: 48px;
  font-weight: bold;
  margin-bottom: 25px;
  color: #49517d;
}

.header-btn {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  border-radius: 100%;
  background-color: #49517d;
  color: white;
}
</style>
