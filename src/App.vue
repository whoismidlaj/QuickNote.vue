<script setup>
import Header from './components/Header.vue';
import NoteList from './components/NoteList.vue';
// import AddNoteBtn from './components/AddNoteBtn.vue';
import AddNote from './components/AddNote.vue';

import { ref, onMounted } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();

const notes = ref([]);

onMounted(() => {
  const savedNotes = JSON.parse(localStorage.getItem('notes'));
  if(savedNotes) {
    notes.value = savedNotes;
  }
});

const saveNotesToLocalStorage = () => {
  localStorage.setItem('notes', JSON.stringify(notes.value));
}


const handleNoteSubmitted = (NoteData) => {
  notes.value.push({
    id: generateUniqueID(),
    title: NoteData.title,
    content: NoteData.content,
  })
  
  toast.success('Note Added');
  saveNotesToLocalStorage();
}

const handleTransactionDeleted = (id) => {
  notes.value = notes.value.filter((note) => note.id !== id);
  toast.success('Note Deleted');
  saveNotesToLocalStorage();
}

const generateUniqueID = () => {
  return Math.floor(Math.random() * 100000);
}

</script>

<template>
  <div class="max-w-md mx-auto h-[100dvh]">
    <Header />
    <div class="flex flex-col h-[90dvh]">
    <NoteList class="flex-1" @note-deleted="handleTransactionDeleted" :notes="notes" />
    <!-- <AddNoteBtn /> -->
    <AddNote @-note-submitted="handleNoteSubmitted" />
  </div>
  </div>
</template>