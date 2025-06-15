<template>
  <div class="min-h-screen bg-gray-100 flex flex-col items-center p-6">
    <h1 class="text-3xl font-bold mb-4">Yapılacaklar Listesi</h1>

    <div class="flex mb-6 w-full max-w-md">
      <input
        v-model="newTask"
        @keyup.enter="addTask"
        type="text"
        placeholder="Yeni görev ekle..."
        class="flex-grow p-2 rounded-l border border-gray-300"
      />
      <button
        @click="addTask"
        class="bg-blue-500 text-white px-4 py-2 rounded-r hover:bg-blue-600"
      >
        Ekle
      </button>
    </div>

    <p v-if="tasks.length === 0" class="text-gray-600">Henüz bir görev eklenmedi.</p>

    <ul v-else class="w-full max-w-md space-y-2">
      <li
        v-for="(task, index) in tasks"
        :key="index"
        class="flex justify-between items-center p-2 bg-white rounded shadow"
      >
        <span :class="{ 'line-through text-gray-400': task.done }">{{ task.text }}</span>
        <div class="space-x-2">
          <button
            @click="toggleDone(index)"
            class="text-sm text-green-600 hover:underline"
          >
            {{ task.done ? 'Geri Al' : 'Tamamla' }}
          </button>
          <button
            @click="removeTask(index)"
            class="text-sm text-red-600 hover:underline"
          >
            Sil
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ text: this.newTask, done: false });
        this.newTask = '';
      }
    },
    toggleDone(index) {
      this.tasks[index].done = !this.tasks[index].done;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style>
body {
  font-family: sans-serif;
}
</style>