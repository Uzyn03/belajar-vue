<script setup>
import { ref } from "vue";

const showForm = ref(false);
const newMemo = ref("");
const memos = ref([]);

function addMemo() {
  memos.value.push({
    id: Date.now(),
    memo: newMemo.value,
    date: new Date().toLocaleDateString("en-us"),
    backgroundColor: getRandomColor(),
  });

  newMemo.value = "";
  showForm.value = false;
}

function getRandomColor() {
  return `#${Math.floor(Math.random() * 16777215).toString(16)}`;
}
</script>

<template>
  <main>
    <div class="container">
      <header>
        <h1 class="header-title">Memo</h1>
        <button @click="showForm = true" class="header-button">+</button>
      </header>
      <div class="card-container">
        <div v-for="(memo, index) in memos" class="card" :key="index" :style="{ backgroundColor: memo.backgroundColor}">
          <p class="card-content">{{ memo.memo }}</p>
          <p class="card-date">{{ memo.date }}</p>
        </div>
      </div>
    </div>

    <div v-if="showForm" class="form-overlay">
      <div class="form-modal">
        <button @click="showForm = false" class="form-close-btn">
          &times;
        </button>
        <textarea
          v-model="newMemo"
          name="memo"
          id="memo"
          cols="30"
          rows="10"
        ></textarea>
        <button @click="addMemo" class="form-save-btn">Save</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
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
  /* background-color: aqua; */
}

.header-title {
  font-size: 50px;
  color: #047857;
  margin-bottom: 25px;
}

.header-button {
  border: none;
  cursor: pointer;
  border-radius: 100%;
  background-color: #047857;
  color: #fff;
  width: 50px;
  height: 50px;
  padding: 10px;
}

.card-container {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.card {
  background-color: #67e8f9;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px;
  margin-bottom: 20px;
  width: 225px;
  height: 225px;
  border-radius: 5%;
}

.form-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 10;
  background-color: rgba(0, 0, 0, 0.77);
  display: flex;
  justify-content: center;
  align-items: center;
}

.form-modal {
  width: 420px;
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
  background-color: #047857;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  margin-top: 15px;
  color: white;
}

.form-close-btn {
  position: absolute;
  top: 5px;
  right: 5px;
  width: 30px;
  height: 30px;
  background-color: transparent;
  border: none;
  font-size: 30px;
  cursor: pointer;
}
</style>
