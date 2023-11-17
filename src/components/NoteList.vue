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
</script>

<template>
<div class="p-5">
    <div class="max-h-[50dvh] overflow-auto border-[1px] border-zinc-900 flex flex-col">
    <div v-for="note in notes" :key="note.id" class="border-b-[1px] last:border-b-0 border-zinc-900">
      <h2 @click="() => toggleNote(note)" class="p-5 text-lg font-medium">{{ note.title }}</h2>
      <div v-if="showNote === note" class="absolute z-10 top-0 left-0 bg-white w-[100vw] h-[100vh]">
        <div class="max-w-md mx-auto p-5 pt-10 flex flex-col gap-4">
            <h2 class="text-4xl font-medium">{{ note.title }}</h2>
            <p>{{ note.content }}</p>
            <button class="fixed bottom-10 right-10 bg-black text-white p-5" @click="closeNote">Close</button>
        </div>
      </div>
    </div>
  </div>
</div>
</template>
