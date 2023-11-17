<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const title = ref('');
const content = ref('');

const emits = defineEmits(['NoteSubmitted']);
const toast = useToast();

const onSubmit = () => {
    if(!title.value || !content.value) {
        toast.error("Note without Note are not Accepted!");
        return;
    }

    const NoteData = {
        title: title.value,
        content: content.value,
    }
    
    emits('NoteSubmitted', NoteData);

    title.value = '';
    content.value = '';
}
</script>

<template>
    <div class="fixed bottom-0 w-full max-w-md p-5">
        <form class="w-full" @submit.prevent="onSubmit">
            <input v-model="title" id="title" class="w-full border-[1px] border-zinc-900 outline-none mb-2 p-2" type="text" placeholder="Title">
            <textarea v-model="content" id="content" class="min-h-[20dvh] w-full border-[1px] border-zinc-900 outline-none mb-2 p-2" placeholder="Type you note"></textarea>
            <button class="bg-black text-white px-5 py-2">Add Note</button>
        </form>
    </div>
</template>