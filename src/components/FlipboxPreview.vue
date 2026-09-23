<script setup>
import { ref } from 'vue'

defineProps({
  front: {
    type: String,
    default: '',
  },

  back: {
    type: String,
    default: '',
  },
})

const showingFront = ref(true)

function flipCard() {
  showingFront.value = !showingFront.value
}
</script>

<template>
  <section class="preview-section">
    <h2>Preview</h2>

    <div
      class="flipbox"
      role="button"
      tabindex="0"

      :aria-label="
        showingFront
          ? 'Showing front of flipbox. Activate to show back.'
          : 'Showing back of flipbox. Activate to show front.'
      "

      @click="flipCard"
      @keydown.enter.prevent="flipCard"
      @keydown.space.prevent="flipCard"
    >
      <div
        class="flipbox-inner"
        :class="{ flipped: !showingFront }"
      >

        <!-- FRONT SIDE -->
        <div class="flipbox-face flipbox-front">
          <span class="side-title">
            FRONT
          </span>

          <div
            v-if="front"
            class="preview-content"
            v-html="front"
          ></div>

          <p
            v-else
            class="empty-message"
          >
            Add front content in the builder.
          </p>

          <span class="flip-help">
            Click to flip
          </span>
        </div>


        <!-- BACK SIDE -->
        <div class="flipbox-face flipbox-back">
          <span class="side-title">
            BACK
          </span>

          <div
            v-if="back"
            class="preview-content"
            v-html="back"
          ></div>

          <p
            v-else
            class="empty-message"
          >
            Add back content in the builder.
          </p>

          <span class="flip-help">
            Click to flip
          </span>
        </div>

      </div>
    </div>


    <!-- ACCESSIBLE STATUS -->
    <p
      class="side-status"
      aria-live="polite"
    >
      Showing:
      <strong>
        {{ showingFront ? 'Front' : 'Back' }}
      </strong>
    </p>

  </section>
</template>