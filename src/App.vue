<script setup>
import { ref, computed } from 'vue'
import draggableComponent from 'vuedraggable'

const name = ref('')
const items = ref([])        // source list
// Create 4 target lists instead of just one
const target1 = ref([])     
const target2 = ref([])     
const target3 = ref([])     
const target4 = ref([])     

const MAX = 20
function addItem() {
  const v = name.value.trim()
  if (!v || items.value.length >= MAX) return
  items.value.push({ id: Date.now(), text: v })
  name.value = ''
}
function removeItem(i) { items.value.splice(i, 1) }
const remaining = computed(() => MAX - items.value.length)

// Export function
function exportLists() {
  const data = {
    sourceList: items.value,
    target1: target1.value,
    target2: target2.value,
    target3: target3.value,
    target4: target4.value
  }
  
  const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'text/plain' })
  const url = window.URL.createObjectURL(blob)
  const link = document.createElement('a')
  link.href = url
  link.download = 'maneuvers-lists.txt'
  link.click()
  window.URL.revokeObjectURL(url)
}

// Import function
function importLists() {
  const input = document.createElement('input')
  input.type = 'file'
  input.accept = '.txt'
  
  input.onchange = e => {
    const file = e.target.files[0]
    const reader = new FileReader()
    
    reader.onload = readerEvent => {
      try {
        const content = JSON.parse(readerEvent.target.result)
        items.value = content.sourceList || []
        target1.value = content.target1 || []
        target2.value = content.target2 || []
        target3.value = content.target3 || []
        target4.value = content.target4 || []
      } catch (err) {
        alert('Error reading file: Please make sure it\'s a valid lists file')
      }
    }
    
    reader.readAsText(file)
  }
  
  input.click()
}
</script>

<template>
  <main>
    <h1 class="eleven">Crusader Granted Maneuvers Tool</h1>

    <div class="cards">
     
      <div class="card">
        <div class="field">
          <button class="botonnohoverleft" @click="importLists">Import</button>
          <button class="botonnohoverright" @click="exportLists">Export</button>
          
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
  :group="{ name: 'names', pull: true, put: true }"
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

      <!-- Four target cards -->
      <div class="card">
        <h2 class="card-title">Card 1</h2>
        <draggableComponent
          v-model="target1"
          item-key="id"
          tag="ul"
          class="card-list"
          :group="{ name: 'names', pull: true, put: true }"
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
            <li v-if="!target1.length" class="card-item empty-hint">Drop items here →</li>
          </template>
        </draggableComponent>
      </div>

      <div class="card">
        <h2 class="card-title">Card 2</h2>
        <draggableComponent
          v-model="target2"
          item-key="id"
          tag="ul"
          class="card-list"
          :group="{ name: 'names', pull: true, put: true }"
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
            <li v-if="!target2.length" class="card-item empty-hint">Drop items here →</li>
          </template>
        </draggableComponent>
      </div>

      <div class="card">
        <h2 class="card-title">Card 3</h2>
        <draggableComponent
          v-model="target3"
          item-key="id"
          tag="ul"
          class="card-list"
          :group="{ name: 'names', pull: true, put: true }"
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
            <li v-if="!target3.length" class="card-item empty-hint">Drop items here →</li>
          </template>
        </draggableComponent>
      </div>

      <div class="card">
        <h2 class="card-title">Card 4</h2>
        <draggableComponent
          v-model="target4"
          item-key="id"
          tag="ul"
          class="card-list"
          :group="{ name: 'names', pull: true, put: true }"
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
            <li v-if="!target4.length" class="card-item empty-hint">Drop items here →</li>
          </template>
        </draggableComponent>
      </div>
    </div>
  </main>
</template>



<style  lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400..900;1,400..900&display=swap');
</style>
