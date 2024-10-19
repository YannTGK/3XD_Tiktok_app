<script setup>
import { ref } from 'vue';
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';

const messages = ref([]);

function addMessage(message) {
    // Send message to backend
    fetch('https://threexd-messages-api-cevy.onrender.com/api/v1/messages', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(message)
    })
    .then(response => response.json())
    .then(data => {
        // After successful push to DB, add the message to the local state
        messages.value.push(data.data.message);
    })
    .catch(error => {
        console.error('Error sending message:', error);
    });
}   
</script>

<template>
    <ChatMessages :messages="messages" />
    <ChatForm @sendMessage="addMessage" />
</template>

<style scoped>
</style>
