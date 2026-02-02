<script setup>
const props = defineProps({
    userId: {
        type: String,
        default: ''
    },
})
</script>

<template>
    <div class="user-card">
        <h2>dWebsite available!</h2>
        <p>This user has tied their ENS name to a website hosted on decentralized infrastructure</p>
        <a class="button" :href="`https://${userId}.link`">View dWebsite</a>
    </div>
</template>

<style scoped>
.user-card {
    /* Nuxt/Vue components often look better with a dark background 
     if using cyan/white text */
    background-color: #1a1a1a;
    border: 1px solid #333;
    border-radius: 12px;
    padding: 1.5rem;
    width: 355px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
    font-family: InterDisplay, Inter, sans-serif;
    /* Ensures the bio and everything else stays centered if desired */
    text-align: center;
}

.header {
    display: flex;
    flex-direction: column;
    /* Stack image and info vertically */
    align-items: center;
    /* Center them horizontally */
}

.avatar {
    width: 80px;
    /* Sightly larger looks better when centered */
    height: 80px;
    border-radius: 50%;
    object-fit: cover;
    border: 2px solid cyan;
    /* Optional: adds a ring effect */
    margin-bottom: 10px;
}

.info {
    display: flex;
    flex-direction: column;
    align-items: center;
}

h2 {
    margin-top: 0;
}

a.button {
    background-color: #00ffff;
    color: black;
    padding: 5px 10px;
    text-decoration: none;
    border: none;
    font-family: InterDisplay, Inter, sans-serif;
    font-size: 16px;
    margin: 10px;
    border-radius: 10px;
}

a.button:hover {
    background-color: #6f00ff;
    color: white;
}

a.button:active {
    background-color: #0000ff;
    color: white;
}
</style>