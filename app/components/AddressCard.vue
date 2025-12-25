<script setup>
import { ref } from 'vue'

const props = defineProps({
    chainName: String, // e.g., "Ethereum" or "Solana"
    address: String,   // The actual wallet address
    iconUrl: String    // Optional: URL for the chain logo
})

const copied = ref(false)

const copyToClipboard = async () => {
    try {
        await navigator.clipboard.writeText(props.address)
        copied.value = true

        // Reset the "Copied!" message after 2 seconds
        setTimeout(() => {
            copied.value = false
        }, 2000)
    } catch (err) {
        console.error('Failed to copy: ', err)
    }
}

// Helper to truncate long addresses: 0x123...abcd
const truncatedAddress = computed(() => {
    if (!props.address) return ''
    return `${props.address.slice(0, 6)}...${props.address.slice(-4)}`
})
</script>

<template>
    <div class="address-card">
        <div class="chain-info">
            <img v-if="iconUrl" :src="iconUrl" class="chain-icon" alt="Chain Icon" />
            <span class="chain-name">{{ chainName }}</span>
        </div>

        <div class="address-container">
            <code class="address-text" :title="address">{{ truncatedAddress }}</code>

            <button @click="copyToClipboard" class="copy-btn" :class="{ 'is-copied': copied }">
                {{ copied ? 'Copied!' : 'Copy' }}
            </button>
        </div>
    </div>
</template>

<style scoped>
@import url('https://fonts.cdnfonts.com/css/jetbrains-mono');

.address-card {
    background: #222;
    border: 1px solid #444;
    border-radius: 8px;
    padding: 12px 16px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 370px;
    margin: 8px 0;
}

.chain-info {
    display: flex;
    align-items: center;
    gap: 8px;
}

.chain-icon {
    width: 32px;
    height: 32px;
    margin-right: 5px;
}

.chain-name {
    color: white;
    font-weight: 600;
    font-size: 0.9rem;
}

.address-container {
    display: flex;
    align-items: center;
    gap: 12px;
}

.address-text {
    color: cyan;
    background: #111;
    padding: 4px 8px;
    border-radius: 4px;
    font-family: "JetBrains Mono", monospace;
    font-size: 0.85rem;
}

.copy-btn {
    background: transparent;
    border: 1px solid cyan;
    color: cyan;
    padding: 4px 10px;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.75rem;
    transition: all 0.2s;
    min-width: 65px;
}

.copy-btn:hover {
    background: rgba(0, 255, 255, 0.1);
}

.copy-btn.is-copied {
    background: cyan;
    color: black;
}
</style>