<script setup lang="ts">
import type { Haiku } from '@/models/Haiku'
import { ref } from 'vue'

defineProps({
  haikus: {
    type: Object as () => { [key: string]: Haiku[] },
    required: true,
  },
})
const file = ref<File | null>(null)
const fileContents = ref<string | null>(null)

const readFileContents = async () => {
  if (file.value) {
    try {
      const contents = await file.value.text()
      const fileContents = JSON.parse(contents)
      emit('importJson', fileContents)
    } catch (error) {
      console.error('Error reading file:', error)
    }
  }
  fileContents.value = null
}

const emit = defineEmits(['importJson', 'addHaiku', 'cancel'])

const handleFileChange = (event: Event) => {
  const target: HTMLInputElement = event.target as HTMLInputElement
  if (target.files) {
    file.value = target.files[0]
    readFileContents()
  }
}
</script>

<template>
  <div id="import-container">
    <label class="file-select">
      <input type="file" @change="handleFileChange" />
    </label>
  </div>
  <button @click.prevent="$emit('addHaiku')">Import!</button>
  <button @click.prevent="$emit('cancel')">Cancel</button>
</template>
