<script setup>
import { ref, onMounted } from 'vue'

import FlipboxBuilder from './components/FlipboxBuilder.vue'
import FlipboxPreview from './components/FlipboxPreview.vue'

const frontContent = ref('')
const backContent = ref('')

const savedMessage = ref('')

const STORAGE_KEY = 'flipbox-builder-data'


// LOAD SAVED FLIPBOX
onMounted(() => {
  const savedData = localStorage.getItem(STORAGE_KEY)

  if (!savedData) {
    return
  }

  try {
    const parsedData = JSON.parse(savedData)

    frontContent.value = parsedData.front || ''
    backContent.value = parsedData.back || ''
  } catch (error) {
    console.error('Could not load saved flipbox.', error)
  }
})


// SAVE FLIPBOX
function saveFlipbox() {
  const flipboxData = {
    front: frontContent.value,
    back: backContent.value,
  }

  localStorage.setItem(
    STORAGE_KEY,
    JSON.stringify(flipboxData)
  )

  savedMessage.value = 'Flipbox saved successfully.'

  setTimeout(() => {
    savedMessage.value = ''
  }, 2500)
}
</script>


<template>
  <main class="app-container">

    <h1>Flipbox Builder</h1>

    <div class="workspace">

      <!-- BUILDER -->

      <FlipboxBuilder
        :front="frontContent"
        :back="backContent"

        @update:front="frontContent = $event"
        @update:back="backContent = $event"

        @save="saveFlipbox"
      />


      <!-- LIVE PREVIEW -->

      <FlipboxPreview
        :front="frontContent"
        :back="backContent"
      />

    </div>


    <!-- SAVE CONFIRMATION -->

    <p
      v-if="savedMessage"
      class="save-message"
      role="status"
      aria-live="polite"
    >
      ✓ {{ savedMessage }}
    </p>

  </main>
</template>