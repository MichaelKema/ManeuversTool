<script setup>
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/core";

const greetMsg = ref("");
const name = ref("");

async function greet() {
  // Learn more about Tauri commands at https://tauri.app/develop/calling-rust/
  greetMsg.value = await invoke("greet", { name: name.value });
}
</script>

<template>
  <main>
    <h1 class="eleven">Crusader Granted Maneuvers Tool</h1>

    
    <div class="card-wrapper">
      <div class="card"></div>
      <input type="text" class="input" placeholder="Input text" />
    </div>
  </main>
</template>



<style  lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400..900;1,400..900&display=swap');
</style>
