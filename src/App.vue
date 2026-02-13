<script setup>

import { ref, watch, onMounted, computed } from 'vue'

// ① 状態（state）
const task = ref('')
const tasks = ref([])
const inputRef = ref(null)
const filter = ref('all')
const isDark = ref(false)

// 未完了だけを取り出しその数を数える
const remainingCount = computed(() => {
  return tasks.value.filter(t => !t.done).length
})

// ② 派生データ（computed）
const filteredTasks = computed(() => {
  let result = tasks.value

  if (filter.value === 'active') {
    result = tasks.value.filter(t => !t.done)
  }

  if (filter.value === 'completed') {
    result = tasks.value.filter(t => t.done)
  }

  // 未完了を上、完了を下に並べる
  return [...result].sort((a, b) => a.done - b.done)
})

// ③ 操作（functions）
const addTask = async () => {
  if (!task.value.trim()) return

  tasks.value.unshift({
    id: Date.now(),
    text: task.value,
    done: false
  })

  task.value = ''
  inputRef.value.focus()
}

const removeTask = (id) => {
  tasks.value = tasks.value.filter(t => t.id !== id)
}

//全削除
const clearAll = () => {
  if (confirm('本当に全て削除しますか？')) {
  tasks.value = []
  }
}

const clearCompleted = () => {
  if (confirm('完了したタスクを削除しますか？')) {
    tasks.value = tasks.value.filter(t => !t.done)
  }
}

// ④ 監視・ライフサイクル
watch(tasks, (newTasks) => {
  localStorage.setItem('tasks', JSON.stringify(newTasks))
}, { deep: true })

watch(isDark, (val) => {
  localStorage.setItem('darkMode', val)
})

onMounted(() => {
  const savedTasks = localStorage.getItem('tasks')
  if (savedTasks) {
    tasks.value = JSON.parse(savedTasks)
  }
const savedDark = localStorage.getItem('darkMode')
if (savedDark !== null) {
  isDark.value = savedDark === 'true'
}
})


</script>

<template>
  <div :class="{ dark: isDark }">
    <h1>TODOアプリ</h1>
    <button @click="isDark = !isDark">
     {{ isDark ? '☀ ライト' : '🌙 ダーク' }}
    </button>

    <input
      ref="inputRef"
      v-model="task"
      @keyup.enter="addTask"
    />
    <button @click="addTask">追加</button>

    <!-- ここにフィルターボタン -->
    <div class="filters">
      <button :class="{ active: filter === 'all' }" @click="filter = 'all'">すべて</button>
      <button :class="{ active: filter === 'active' }" @click="filter = 'active'">未完了</button>
      <button :class="{ active: filter === 'completed' }" @click="filter = 'completed'">完了</button>
    </div>  
    <div>
      <p>残り {{ remainingCount }} 件</p>
       <button @click="clearCompleted">完了だけ削除</button>
      <button @click="clearAll">全削除</button>
    </div>
    <ul>
      <transition-group name="fade" tag="ul">
  　　　<li v-for="t in filteredTasks" :key="t.id">
    　　　<input type="checkbox" v-model="t.done" />
    　　　<span :style="{ textDecoration: t.done ? 'line-through' : 'none' }">
      　　　{{ t.text }}
    　　　</span>
    　　　<button @click="removeTask(t.id)">削除</button>
 　　　 </li>
　　　</transition-group>
    </ul>
  </div>
</template>

<style>
body {
  background: #f5f6f8;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}

div {
  max-width: 420px;
  margin: 60px auto;
  background: white;
  padding: 30px;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  font-weight: 600;
}

input[type="text"],
input:not([type]) {
  width: 70%;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #ddd;
  margin-right: 8px;
}

button {
  padding: 8px 14px;
  border-radius: 8px;
  border: none;
  background: #3b82f6;
  color: white;
  cursor: pointer;
  transition: 0.2s;
}

button:hover {
  opacity: 0.85;
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 20px;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 0;
  border-bottom: 1px solid #eee;
}

li:last-child {
  border-bottom: none;
}

span {
  flex: 1;
  margin-left: 10px;
}

input[type="checkbox"] {
  transform: scale(1.2);
}

span[style*="line-through"] {
  color: #999;
}

li button {
  background: #ef4444;
}

.filters {
  display: flex;
  gap: 8px;
  margin-top: 15px;
}

.filters button {
  background: #e5e7eb;
  color: #333;
}

.filters button.active {
  background: #3b82f6;
  color: white;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.dark {
  background: #1f2937;
  color: #f9fafb;
}

.dark div {
  background: #111827;
  box-shadow: none;
}

.dark button {
  background: #374151;
  color: white;
}

.dark .filters button {
  background: #374151;
}

.dark .filters button.active {
  background: #2563eb;
}

.dark li {
  border-bottom: 1px solid #374151;
}

</style>
