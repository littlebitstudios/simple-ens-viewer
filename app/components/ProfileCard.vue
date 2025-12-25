<script setup>
const props = defineProps({
    displayName: {
        type: String,
        default: ''
    },
    userId: {
        type: String,
        default: ''
    },
    profilePicUrl: {
        type: String,
        default: ''
    },
    description: {
        type: String,
        default: ''
    }
})
</script>

<template>
    <div class="user-card">
        <div class="header">
            <img :src="profilePicUrl || '/no-avatar.png'" :alt="displayName" class="avatar" />
            <div class="info">
                <h3>{{ displayName.split(".")[0] }}</h3>
                <span class="user-id">{{ userId }}</span>
            </div>
        </div>

        <p v-if="description" class="bio">{{ description }}</p>
        <a class="button" v-if="userId.endsWith('.base.eth')" :href="`https://base.org/names/${userId.split('.')[0]}`">View on Basenames</a>
        <a class="button" v-else-if="userId.endsWith('.eth')" :href="`https://app.ens.domains/${userId}`">View on ENS Web App</a>
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
    padding-bottom: 1rem;
    width: 355px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
    font-family: sans-serif;
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

h3 {
    font-family: InterVariable, Inter, sans-serif;
    margin: 0;
    font-size: 1.2rem;
    color: white;
}

.user-id {
    font-family: InterVariable, Inter, sans-serif;
    color: cyan;
    font-size: 0.85rem;
    font-weight: 500;
    margin-top:3px
}

.bio {
    font-family: InterVariable, Inter, sans-serif;
    font-size: 0.9rem;
    line-height: 1.5;
    color: #ccc;
    /* Slightly off-white for better readability */
    margin-top: 1.25rem;
}

a.button {
    background-color: #00ffff;
    color: black;
    padding: 5px 10px;
    text-decoration: none;
    border: none;
    font-family: InterVariable, Inter, sans-serif;
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