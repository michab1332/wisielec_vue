<script setup lang="ts">
const handleReset = () => {
    location.reload();
}
</script>

<template>
    <div class="navbar">
        <h3 class="navbar__title">
            Wisielec
        </h3>
        <p @click="handleReset" class="navbar__resetButton">RESET</p>
    </div>
</template>

<style scoped>
.navbar {
    background-color: #262626;
    display: flex;
    justify-content: space-between;
    color: #fff;
    align-items: center;
    height: 10vh;
    padding: 0 3rem;
}

.navbar__resetButton {
    cursor: pointer;
    transition: transform .3s ease;
}

.navbar__resetButton:hover {
    transform: scale(1.1);
}
</style>