<script setup>
  import { ref } from 'vue'

  const nameToView = ref('')

  const navigate = () => {
    if (nameToView.value) {
      navigateTo(`./u/${nameToView.value}`)
    }
  }
</script>

<template>
    <h1>Simple ENS Viewer</h1>
    <p>
      Wallet not accepting a particular ENS name?<br/>Try using it here to get their address(es).<br/>
    </p>
    <div>
      <input @keyup.enter="navigate" type="text" v-model="nameToView" id="nameToView" name="nameToView">
      <button @click="navigate" id="goButton">Go</button>
    </div>
    <small>You can also see if an Ethereum address has an<br/>ENS name connected to it by pasting it here.</small>
    <footer style="margin-top: 15px;">
      Created by <a href="https://littlebit670.link">LittleBit</a><br/>
      Uses a public ENS API: <a href="https://enstate.rs">enstate.rs</a>
    </footer>
</template>
