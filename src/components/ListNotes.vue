<script setup lang="ts">
import type { Note } from "@/utils/types";

defineProps<{
  deleteNote: (id: string) => void;
  notes: Note[];
  updateNote: (id: string) => void;
  toggleModal: (note: Note) => void;
  toggleValue: boolean;
  toggleViewModal: (note: Note) => void;
}>();
</script>

<template>
  <div class="mt-5 bg-slate-500 p-4 rounded h-full">
    <div class="mb-4">
      <h2 class="text-2xl font-bold text-center">List Notes</h2>
    </div>
    <ul class="flex flex-col gap-4 max-h-96 overflow-y-scroll">
      <li
        class="flex flex-col bg-slate-400 p-4 py-8 rounded-lg space-y-2"
        v-for="n in notes"
        :key="n.id"
      >
        <div class="flex justify-between">
          <small
            >Created At:
            {{ new Date(n.created_at!).toLocaleString().split(",")[0] }}</small
          >
          <br />
          <small
            >Updated At:
            {{ new Date(n.updated_at!).toLocaleString().split(",")[0] }}</small
          >
        </div>
        <strong>
          <button
            class="text-xl font-bold underline"
            @click="toggleViewModal(n)"
          >
            {{ n.title.charAt(0).toUpperCase() + n.title.slice(1) }}
          </button>
        </strong>
        <textarea
          v-if="toggleValue"
          v-model="n.content"
          class="bg-slate-200 rounded p-1 w-full"
          rows="3"
        ></textarea>
        <p v-else class="text-ellipsis overflow-hidden whitespace-nowrap">
          {{ n.content.slice(0, 50) }}
        </p>

        <div class="flex justify-end space-x-2 mt-4">
          <button
            class="bg-yellow-500 rounded-2xl p-2 px-4 hover:bg-yellow-400 hover:cursor-pointer"
            @click="toggleModal(n)"
          >
            Update
          </button>
          <button
            class="bg-slate-700 rounded-2xl p-2 px-4 hover:bg-slate-600 hover:cursor-pointer"
            @click="deleteNote(n.id!)"
          >
            Delete
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
