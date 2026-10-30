<script setup>
import { ref } from 'vue'

const tasks = ref([])

const inputTask = ref('')

const addTask = (title) => {

  const newTask = {
    id: new Date().getTime(),
    title: title,
    status: false
  }

  tasks.value.push(newTask)

  inputTask.value = ''
}

const deleteTask = (id) => {

  const task = tasks.value.find(item => item.id === id)

  if (!task) {
    alert("Task tidak ditemukan!")
    return
  }

  const confirmation = confirm("Apakah anda yakin")

  if (confirmation) {
    tasks.value = tasks.value.filter(item => item.id !== id)
  }

  tasks.value = tasks.value.filter(item => item.id !== id)
}
</script>

<template>
  <section class="app-screen">
    <div class="retro-window">
      <div class="title-bar">
        <span class="title-text">TASKIFY VUE</span>
        <div class="title-buttons">
          <span class="title-btn"></span>
          <span class="title-btn"></span>
          <span class="title-btn close"></span>
        </div>
      </div>

      <form @submit.prevent="addTask(inputTask)" action="" class="input-row">
        <input
          v-model="inputTask"
          type="text"
          placeholder="Masukkan tugas baru"
          aria-label="Tugas baru"
          class="input-field"
        />
        <button type="submit" class="btn btn-primary">
          <span class="btn-label">tambah</span>
        </button>
      </form>

      <ul class="task-list" v-auto-animate>
        <li v-for="task in tasks" :key="task.id" class="task-item">
          <div>
            <input v-model="task.status" type="checkbox" class="checkbox" />
            <span class="task-title" :class="task.status ? 'line-through' : ''">
              {{ task.title }}
            </span>
          </div>
          <button @click="deleteTask(task.id)" class="btn btn-delete">
            <span class="btn-label">Hapus</span>
          </button>
        </li>
      </ul>

    </div>
  </section>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Arial+Black&family=Arial+Condensed:wght@700&family=Arial:ital,wght@0,400;0,700;1,400&display=swap');

:root {
  --bg: #c8bda8;
  --win-bg: #e8e0d0;
  --title-bar: #174b46;
  --bevel-light: #fff8e8;
  --bevel-dark: #8b8578;
  --bevel-deep: #3f3b35;
  --primary: #226c63;
  --primary-dark: #123d3a;
  --info: #3d72a5;
  --danger: #8f2f2c;
  --text: #2d302d;
  --text-muted: #77756d;
}

.app-screen {
  min-height: 100vh;
  box-sizing: border-box;
  background: #c8bda8;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
  font-family: 'Arial', 'Helvetica', sans-serif;
  color: var(--text);
}

.retro-window {
  width: 100%;
  max-width: 520px;
  background: var(--win-bg);
  border: 2px solid var(--bevel-light);
  outline: 2px solid var(--bevel-deep);
  box-shadow: 5px 5px 0 #756d5e;
  padding: 8px;
}

.title-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: var(--title-bar);
  color: #fff8e8;
  padding: 9px 12px;
  border-bottom: 2px solid #0b2d2b;
  font-family: 'Arial Black', 'Arial Condensed', sans-serif;
  font-size: 17px;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.title-btn {
  width: 13px;
  height: 13px;
  border: 2px solid #f7f0df;
  background: #746f63;
  display: inline-block;
  margin-left: 6px;
  box-shadow: inset 1px 1px 0 #fff;
}

.title-btn.close {
  background: var(--danger);
}

.input-row {
  display: flex;
  gap: 8px;
  margin-top: 12px;
}

.input-field {
  flex: 1;
  min-width: 0;
  padding: 8px 10px;
  border: 2px solid #8b8578;
  background: #f8f3e8;
  box-shadow: inset 1px 1px 0 #c8c0b0;
  border-radius: 0;
  font-family: 'Arial', sans-serif;
  font-size: 14px;
  color: var(--text);
}

.input-field::placeholder { color: var(--text-muted); }
.input-field:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: inset 1px 1px 0 #c8c0b0, 0 0 0 1px var(--primary);
}

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(#f7f1e2, #c9c0ae);
  border: 2px solid #8b8578;
  border-top-color: #fff8e8;
  border-left-color: #fff8e8;
  box-shadow: 2px 2px 0 var(--bevel-deep);
  border-radius: 0;
  padding: 7px 14px;
  font-family: 'Arial', sans-serif;
  font-size: 13px;
  font-weight: bold;
  color: black;
  cursor: pointer;
  white-space: nowrap;
}

.btn:hover { background: linear-gradient(#fff8e8, #d8cfbd); }
.btn:active {
  border-top-color: #8b8578;
  border-left-color: #8b8578;
  box-shadow: inset 2px 2px 0 #736c60;
}

.btn-primary {
  background: var(--primary);
  border-color: var(--primary-dark);
  box-shadow: 2px 2px 0 var(--primary-dark);
  color: #fff8e8;
}
.btn-primary:hover { background: #2b7c71; }
.btn-primary:active { background: var(--primary-dark); }

.btn-delete {
  background: #f2dfd5;
  border-color: var(--danger);
  box-shadow: 2px 2px 0 #642320;
  color: black;
  color: var(--danger);
}
.btn-delete:hover { background: #f7eae1; }
.btn-delete:active { background: #d8b9ad; }

.btn-label { font-weight: bold; }

.task-list {
  list-style: none;
  margin: 13px 0 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 7px;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
  color: white;
  background: #226c63;
  border: 2px solid #8b8578;
  border-top-color: #fff8e8;
  border-left-color: #fff8e8;
  box-shadow: 2px 2px 0 var(--bevel-deep);
  border-radius: 0;
  padding: 9px 10px;
}

.task-item > div { display: flex; align-items: center; gap: 9px; min-width: 0; }

.checkbox {
  width: 16px;
  height: 16px;
  accent-color: var(--primary);
  cursor: pointer;
}

.task-title {
  font-size: 14px;
  color: var(--text);
  word-break: break-word;
}

.task-title.line-through {
  color: var(--text-muted);
  text-decoration: line-through;
}

@media (max-width: 520px) {
  .app-screen { padding: 16px; }
  .input-row { flex-direction: column; }
  .btn-primary { width: 100%; }
}
</style>
