<script setup>
import { watch, onBeforeUnmount } from 'vue'
import { useEditor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'

const props = defineProps({
  modelValue: {
    type: String,
    default: '',
  },
  label: {
    type: String,
    default: 'Content',
  },
})

const emit = defineEmits(['update:modelValue'])

const editor = useEditor({
  content: props.modelValue || '<p></p>',

  extensions: [
    StarterKit,
  ],

  editorProps: {
    attributes: {
      class: 'editor-content',
      'aria-label': props.label,
    },
  },

  onUpdate: ({ editor }) => {
    // Send HTML so Bold, Italic and Lists are preserved.
    emit('update:modelValue', editor.getHTML())
  },
})

watch(
  () => props.modelValue,
  (newValue) => {
    if (!editor.value) return

    const newContent = newValue || '<p></p>'

    if (editor.value.getHTML() !== newContent) {
      editor.value.commands.setContent(newContent, false)
    }
  }
)

onBeforeUnmount(() => {
  editor.value?.destroy()
})
</script>

<template>
  <div class="rich-editor">
    <div
      v-if="editor"
      class="toolbar"
      role="toolbar"
      :aria-label="`${label} formatting toolbar`"
    >
      <!-- BOLD -->
      <button
        type="button"
        :class="{ active: editor.isActive('bold') }"
        :aria-pressed="editor.isActive('bold')"
        aria-label="Bold"
        @click="editor.chain().focus().toggleBold().run()"
      >
        <strong>B</strong>
      </button>

      <!-- ITALIC -->
      <button
        type="button"
        :class="{ active: editor.isActive('italic') }"
        :aria-pressed="editor.isActive('italic')"
        aria-label="Italic"
        @click="editor.chain().focus().toggleItalic().run()"
      >
        <em>I</em>
      </button>

      <!-- BULLET LIST -->
      <button
        type="button"
        :class="{ active: editor.isActive('bulletList') }"
        :aria-pressed="editor.isActive('bulletList')"
        aria-label="Bulleted list"
        @click="editor.chain().focus().toggleBulletList().run()"
      >
        • List
      </button>

      <!-- UNDO -->
      <button
        type="button"
        aria-label="Undo"
        :disabled="!editor.can().chain().focus().undo().run()"
        @click="editor.chain().focus().undo().run()"
      >
        ↶ Undo
      </button>

      <!-- REDO -->
      <button
        type="button"
        aria-label="Redo"
        :disabled="!editor.can().chain().focus().redo().run()"
        @click="editor.chain().focus().redo().run()"
      >
        ↷ Redo
      </button>
    </div>

    <EditorContent
      :editor="editor"
      class="editor-box"
    />
  </div>
</template>