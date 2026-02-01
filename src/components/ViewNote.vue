<script setup lang="ts">
import type { Note } from "@/utils/types";

defineProps<{
  note: Note;
  toggleViewModal: (note: Note) => void;
}>();
</script>

<template>
  <div
    class="flex flex-col gap-4 mt-5 bg-slate-500 p-4 rounded h-1/3 md:h-1/3 md:w-1/3 w-full justify-between"
  >
    <div class="h-full space-y-1 overflow-hidden">
      <div class="flex justify-between">
        <h2 class="text-2xl font-bold text-center">
          {{ note.title.charAt(0).toUpperCase() + note.title.slice(1) }}
        </h2>
        <button
          class="text-red-500 hover:text-red-700"
          @click="toggleViewModal({ title: '', content: '' } as Note)"
        >
          X
        </button>
      </div>
      <p class="h-full text-md overflow-y-scroll" id="content">
        {{ note.content }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
