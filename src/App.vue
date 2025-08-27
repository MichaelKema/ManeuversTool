<script setup>
import { ref, computed } from 'vue'
import draggableComponent from 'vuedraggable'
import draggable from 'vuedraggable'

const name = ref('')
const items = ref([])        // left list
const selected = ref([])     // right list

const MAX = 20
function addItem() {
  const v = name.value.trim()
  if (!v || items.value.length >= MAX) return
  items.value.push({ id: Date.now(), text: v })
  name.value = ''
}
function removeItem(i) { items.value.splice(i, 1) }
const remaining = computed(() => MAX - items.value.length)
</script>

<template>
  <main>
    <h1 class="eleven">Crusader Granted Maneuvers Tool</h1>

    <div class="cards">
      <!-- LEFT card (source) -->
      <div class="card">
        <div class="field">
          <input
            class="input"
            type="text"
            v-model="name"
            placeholder="Input text"
            @keydown.enter.prevent="addItem"
            :disabled="items.length >= 20"
          />
          <button
            class="boton-elegante on-input"
            @click="addItem"
            :disabled="items.length >= 20"
            aria-label="confirm"
          >
            ✔
          </button>
        </div>

<draggableComponent
  v-model="items"
  item-key="id"
  tag="ul"
  class="card-list"
  :sort="false"
  :group="{ name: 'names', pull: true, put: false }"
  :animation="150"
  :force-fallback="true"
  :fallback-on-body="true"
  ghost-class="ghost"
  chosen-class="chosen"
>
  <template #item="{ element, index }">
    <li class="card-item">
      <span class="card-item-text">{{ index + 1 }}. {{ element.text }}</span>
      <button class="item-remove" @click="removeItem(index)" aria-label="remove">×</button>
    </li>
  </template>
</draggableComponent>
      </div>

      <!-- RIGHT card (target) -->
      <div class="card">
<draggableComponent
  v-model="selected"
  item-key="id"
  tag="ul"
  class="card-list"
  :group="{ name: 'names', pull: false, put: true }"
  :animation="150"
  :force-fallback="true"
  :fallback-on-body="true"
  ghost-class="ghost"
  chosen-class="chosen"
>
  <template #item="{ element, index }">
    <li class="card-item">
      <span class="card-item-text">{{ index + 1 }}. {{ element.text }}</span>
    </li>
  </template>

  <template #footer>
    <li v-if="!selected.length" class="card-item empty-hint">Drop items here →</li>
  </template>
</draggableComponent>
      </div>
    </div>
  </main>
</template>



<style  lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400..900;1,400..900&display=swap');
</style>
