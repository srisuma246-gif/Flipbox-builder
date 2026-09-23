<script setup>
import RichTextEditor from './RichTextEditor.vue'

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

const emit = defineEmits([
  'update:front',
  'update:back',
  'save',
])
</script>

<template>
  <section class="builder">
    <h2>Builder</h2>

    <!-- FRONT -->
    <div class="editor-section">
      <h3>Front</h3>

      <RichTextEditor
        label="Front content"
        :model-value="front"
        @update:model-value="emit('update:front', $event)"
      />
    </div>

    <!-- BACK -->
    <div class="editor-section">
      <h3>Back</h3>

      <RichTextEditor
        label="Back content"
        :model-value="back"
        @update:model-value="emit('update:back', $event)"
      />
    </div>

    <button
      type="button"
      class="save-button"
      @click="emit('save')"
    >
      Save Flipbox
    </button>
  </section>
</template>