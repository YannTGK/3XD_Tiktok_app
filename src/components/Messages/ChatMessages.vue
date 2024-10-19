<script setup>
import { reactive, onMounted } from 'vue';

// Define props using Vue's built-in prop system
const props = defineProps({
    messages: {
        type: Array,         // Validate that the prop is an array
        default: () => [],   // Provide a default empty array
    }
});

// Fetch messages from the backend when the component is mounted
const fetchedMessages = reactive([]);

onMounted(() => {
    fetch('https://threexd-messages-api-cevy.onrender.com/api/v1/messages')
        .then(res => res.json())
        .then(data => {
            // Ensure that fetched messages are pushed at the end of the array
            fetchedMessages.push(...data.data.messages);
        })
        .catch(error => {
            console.error('Error fetching messages:', error);
        });
});
</script>

<template>
    <div class="comments">
        <!-- Display both messages passed via props and fetched messages -->
        <ul>
            <!-- Render the combined messages in the order they were received -->
            <li v-for="(message, index) in [...fetchedMessages, ...messages]" :key="index">
                <strong>{{ message.user }}</strong>
                <p>{{ message.text }}</p>
            </li>
        </ul>
    </div>
</template>

<style scoped>
.comments {
    margin-top: 16px;
    padding: 16px;
    border: 1px solid #ccc;
    border-radius: 16px;
    height: 600px;
    overflow-y: scroll;
}
.comments ul {
    list-style-type: none;
    padding: 0;
}
.comments li {
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #fff;
}
</style>