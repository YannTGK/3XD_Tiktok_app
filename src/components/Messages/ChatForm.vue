<script setup>
// ChatForm.vue
import { ref } from 'vue';
const emit = defineEmits(['sendMessage']);
let name = "Dyangoo";
let message = ref('');

function submitMessage() {
    emit('sendMessage', { user: name, text: message.value });
    message.value = "";  // Clear the input after sending
}
</script>

<template>
    <div class="form">
        <label for="name">{{ name }}:</label>
        <input type="text" v-model="message" placeholder="Type your message here...">
        <button @click="submitMessage">Send</button>
    </div>
</template>

<style scoped>
    .form {
        display: flex;
        gap: 10px;
        flex-direction: column;
    }
    input {
        flex: 1;
        padding: 8px 16px;
        font-size: 1rem;
    }
</style>