<script setup>
import { ref } from 'vue';
import { defineProps } from 'vue';

const props = defineProps(['notes']);

const showNote = ref(null);

const toggleNote = (note) => {
  showNote.value = showNote.value === note ? null : note;
};

const closeNote = () => {
  showNote.value = null;
};


const emits = defineEmits(['noteDeleted']);

const deleteNote = (id) => {
    emits('noteDeleted', id);
}
</script>

<template>
<div class="overflow-auto p-5">
    <div class="flex flex-col">
    <div v-if="notes.length > 0" v-for="note in notes" :key="note.id" class="border-[1px] border-b-0 last:border-b-[1px] border-collapse border-zinc-900">
      <div class="flex justify-between items-center pe-5">
        <h2 @click="() => toggleNote(note)" class="p-5 text-lg font-medium">{{ note.title }}</h2>
        <button @click="deleteNote(note.id)" class="p-3 w-5 h-5 flex justify-center items-center border-[1px] border-zinc-900">x</button>
      </div>
      <div v-if="showNote === note" class="absolute z-10 top-0 left-0 bg-white w-[100vw] h-[100vh]">
        <div class="max-w-md mx-auto p-5 pt-10 flex flex-col gap-4">
            <h2 class="text-4xl font-medium">{{ note.title }}</h2>
            <p>{{ note.content }}</p>
            <button class="fixed bottom-10 right-10 bg-black text-white p-5" @click="closeNote">Close</button>
        </div>
      </div>
    </div>
    <div v-else>
        NO NOtes
    </div>
  </div>
</div>
</template>
