<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const userId = route.params.id

// 1. Create a reactive variable to hold the data
const ensData = ref(null)
const ensDataStatusCode = ref(null)

// 2. Run the fetch when the component "mounts" to the page
onMounted(async () => {
  try {
    const ensResponse = await fetch(`https://enstate.rs/u/${userId}`)
    // 3. You MUST await the .json() call too
    var data = await ensResponse.json()
    
    if (data.records) {
      if (data.records.avatar) {
        if (data.records.avatar.startsWith("ipfs://")) {
          const cid = data.records.avatar.slice(7)
          data.records.avatar = `https://ipfs.filebase.io/ipfs/${cid}`
        } 
      }
    }

    // 4. Assign the data to your ref's .value
    ensData.value = data
    ensDataStatusCode.value = ensResponse.status
  } catch (error) {
    console.error("Fetch failed:", error)
  }
})

useSeoMeta({
    title: userId,
    titleTemplate:"%s | Simple ENS Viewer",
    ogTitle: `${userId} | Simple ENS Viewer`,
    ogUrl:"https://ensr.littlebitstudios.com",
    twitterSite:"littlebit670",
    ogType:"website",
    ogDescription:"A Nuxt-based website that shows quick information from ENS profiles",
    twitterCard:"summary",
})
</script>

<template>
  <div v-if="ensDataStatusCode==404">
    <div v-if="userId.startsWith('0x')" style="display:flex; flex-direction:column; align-items: center; max-width: 100%;">
        <p style="width: 300px">It appears that the Ethereum address you gave has no ENS name.</p>
        <AddressCard chainName="Ethereum" :address="userId" icon-url="https://cryptologos.cc/logos/versions/ethereum-eth-logo-diamond-purple.svg" />
    </div>
    <div v-else>
      <p>It appears that that ENS name does not exist.</p>
    </div>
  </div>
  <div v-else-if="ensData" style="display:flex; flex-direction:column; align-items: center; max-width: 100%;">
    <ProfileCard style="margin-bottom:15px; margin-top:15px;" :display-name="ensData.records.name || ensData.name" :user-id="`${ensData.name}`" :profile-pic-url="ensData.records.avatar" :description="ensData.records.description" />
    <AddressCard chainName="Ethereum" :address="ensData.address" icon-url="https://cryptologos.cc/logos/versions/ethereum-eth-logo-diamond-purple.svg" />
    <div v-if="ensData.name.endsWith('.base.eth')" style="max-width:330px; margin-bottom:15px">
        <small>That's a Basename! It's recommended to send to these names on the Base chain.</small>
    </div>
    <div v-else-if="ensData.name.endsWith('.brnr.eth')" style="max-width:340px; margin-bottom:15px">
        <small>That's a Burner card user! Burner cards only support Ethereum, Base, Arbitrum, and Optimism chains.</small>
    </div>
    <div v-else style="max-width:330px; margin-bottom:15px">
        <small>The Ethereum address can be used for other EVM chains like Base and Polygon.</small>
    </div>
    <span v-if="ensData.chains.sol">
        <AddressCard chainName="Solana" :address="ensData.chains.sol" icon-url="https://cryptologos.cc/logos/solana-sol-logo.svg" />
    </span>
    <span v-if="ensData.chains.btc">
        <AddressCard chainName="Bitcoin" :address="ensData.chains.btc" icon-url="https://cryptologos.cc/logos/bitcoin-btc-logo.svg" />
    </span>
    <span v-if="ensData.chains.cardano">
        <AddressCard chainName="Cardano" :address="ensData.chains.cardano" icon-url="https://cardano.org/img/brand-assets/cardano-starburst-white.svg" />
    </span>
  </div>
  <p v-else>Loading ENS data...</p>
  <footer style="margin-top: 15px;">
      <p>Created by <a href="https://littlebit670.link">LittleBit</a> | <a href="https://github.com/littlebitstudios/simple-ens-resolver">View project on GitHub</a></p>
      <p>Uses a public ENS API: <a href="https://enstate.rs">enstate.rs</a></p>
  </footer>
</template>