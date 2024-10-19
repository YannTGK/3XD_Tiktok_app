<script setup>
    let name = 'Dyangoo';
    const props = defineProps({
        title: String });
</script>

<template>
    <div class="video__detail">
        <img src="../../assets/dyangoo.png" alt="profile picture">
        <p class="username">{{ name }}</p>
    </div>
            <h2>{{ title }}</h2>
</template>

<style scoped>
.video__detail {
    display: flex;
    gap: 10px;
    align-items: center;
}
img {
    width: 50px;
    height: 50px;
    border-radius: 50%;
}
</style>
