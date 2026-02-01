<script setup lang="ts">
import type { Note } from "@/utils/types";

defineProps<{
  updateNote: (id: string) => void;
  note: Note;
  toggleModal: (note: Note) => void;
}>();
</script>

<template>
  <form
    class="flex flex-col gap-4 mt-5 bg-slate-500 p-4 rounded h-2/3 md:h-1/2 md:w-1/3 w-full justify-between"
    @submit.prevent="updateNote(note.id!)"
  >
    <div class="h-1/5 space-y-1">
      <div class="flex justify-between">
        <h2 class="text-2xl font-bold text-center">Update Note</h2>
        <button
          class="text-red-500 hover:text-red-700"
          @click="toggleModal({ title: '', content: '' } as Note)"
        >
          X
        </button>
      </div>

      <p class="text-sm font-light">
        Update a simple note using the form below
      </p>
    </div>
    <div class="flex flex-col justify-between space-y-2 h-4/5">
      <div class="w-full h-full flex flex-col space-y-4">
        <input
          class="bg-slate-700 rounded-2xl p-2"
          type="text"
          placeholder="Title"
          v-model="note.title"
        />
        <textarea
          class="bg-slate-700 rounded-2xl p-2 h-3/4 resize-none"
          type="text"
          placeholder="New note"
          id="content"
          v-model="note.content"
        />
      </div>

      <button
        class="bg-slate-700 hover:bg-slate-600 rounded-2xl p-2 hover:cursor-pointer z-50"
        type="submit"
      >
        Update Note
      </button>
    </div>
  </form>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
