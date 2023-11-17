<script setup>
import Header from './components/Header.vue';
import NoteList from './components/NoteList.vue';
// import AddNoteBtn from './components/AddNoteBtn.vue';
import AddNote from './components/AddNote.vue';

import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();

const notes = ref([
  { id: 1, title: 'Note Title', content: 'note content is here' },
  { id: 2, title: 'Note Title', content: 'note content is here' },
  { id: 3, title: 'Note Title', content: 'note content is here' },
  { id: 4, title: 'Note Title', content: 'note content is here' },
  { id: 5, title: 'Note Title', content: 'note content is here' },
]);

const handleNoteSubmitted = (NoteData) => {
  notes.value.push({
    id: generateUniqueID(),
    title: NoteData.title,
    content: NoteData.content,
  })
  
  toast.success('Note Added');
}

const generateUniqueID = () => {
  return Math.floor(Math.random() * 100000);
}

</script>

<template>
  <div class="max-w-md mx-auto h-[100dvh]">
    <Header />
    <NoteList :notes="notes" />
    <!-- <AddNoteBtn /> -->
    <AddNote @-note-submitted="handleNoteSubmitted" />
  </div>
</template>