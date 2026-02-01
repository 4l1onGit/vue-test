<script setup lang="ts">
import { ref, onMounted } from "vue";
import { api } from "./utils/api";
import CreateNote from "./components/CreateNote.vue";
import ListNotes from "./components/ListNotes.vue";
import type { Note } from "./utils/types";
import EditNoteModal from "./components/EditNoteModal.vue";
import ViewNote from "./components/ViewNote.vue";

const notes = ref([] as Note[]);
const toggle = ref(false);
const toggleView = ref(false);
const newNote = ref({
  title: "",
  content: "",
} as Note);

const updatedNote = ref({
  title: "",
  content: "",
} as Note);

const viewNote = ref({
  title: "",
  content: "",
} as Note);

const toggleModal = (note: Note) => {
  updatedNote.value = {
    id: note.id,
    title: note.title,
    content: note.content,
  } as Note;
  toggle.value = !toggle.value;
};

const toggleViewModal = (note: Note) => {
  viewNote.value = {
    id: note.id,
    title: note.title,
    content: note.content,
  } as Note;
  toggleView.value = !toggleView.value;
};

async function loadNotes() {
  try {
    const res = await api.get("/notes");
    notes.value = res.data;
  } catch (error) {
    notes.value = [];
    console.error("Error loading notes:", error);
  }
}

async function createNote() {
  await api.post("/notes", newNote.value);
  newNote.value = {
    title: "",
    content: "",
  } as Note;
  await loadNotes();
}

async function updateNote(id: string) {
  await api.put(`/notes/${id}`, {
    title: updatedNote.value.title,
    content: updatedNote.value.content,
  });
  updatedNote.value = {
    title: "",
    content: "",
  } as Note;
  toggle.value = false;
  await loadNotes();
}

async function deleteNote(id: string) {
  await api
    .delete(`/notes/${id}`)
    .then(() => {
      console.log(`Note with id ${id} deleted successfully.`);
    })
    .catch((error) => {
      console.error(`Error deleting note with id ${id}:`, error);
    });
  await loadNotes();
}

onMounted(loadNotes);
</script>

<template>
  <div
    class="bg-slate-900 w-full h-full min-h-screen text-white flex flex-col justify-center items-center"
    id="app"
  >
    <h1 class="text-4xl font-bold mt-10">Notes</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-10 w-full max-w-4xl p-10">
      <CreateNote :createNote="createNote" :newNote="newNote" />
      <ListNotes
        :toggleViewModal="toggleViewModal"
        :deleteNote="deleteNote"
        :notes="notes"
        :updateNote="updateNote"
        :toggleModal="toggleModal"
        :toggleValue="toggle"
      />
    </div>
    <div
      class="w-full h-full z-100 bg-black/10 backdrop-blur-sm fixed top-0 left-0 flex justify-center items-center p-4"
      v-if="toggle"
    >
      <EditNoteModal
        :updateNote="updateNote"
        :note="updatedNote"
        :toggleModal="toggleModal"
      />
    </div>
    <div
      class="w-full h-full z-100 bg-black/10 backdrop-blur-sm fixed top-0 left-0 flex justify-center items-center p-4"
      v-if="toggleView"
    >
      <ViewNote :note="viewNote" :toggleViewModal="toggleViewModal" />
    </div>
  </div>
</template>
