<script setup lang="ts">
defineProps<{
  createNote: () => void;
  newNote: { title: string; content: string };
}>();
</script>

<template>
  <form
    class="flex flex-col gap-4 mt-5 bg-slate-500 p-4 rounded h-full justify-between shadow-lg"
    @submit.prevent="createNote"
  >
    <div class="h-1/5 space-y-1">
      <h2 class="text-2xl font-bold text-center">Create Note</h2>
      <p class="text-sm font-light text-center">
        Create a simple note using the form below
      </p>
    </div>
    <div class="flex flex-col justify-between space-y-2 h-4/5">
      <div class="w-full h-full flex flex-col space-y-4">
        <input
          class="bg-slate-700 rounded-xl p-2"
          type="text"
          placeholder="Title"
          v-model="newNote.title"
        />
        <textarea
          class="bg-slate-700 rounded-xl p-2 h-3/4 resize-none"
          type="text"
          placeholder="New note"
          id="content"
          v-model="newNote.content"
        />
      </div>

      <button
        class="bg-slate-700 rounded-xl p-2 hover:bg-slate-600 transition-colors duration-200"
        type="submit"
      >
        Add Note
      </button>
    </div>
  </form>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
