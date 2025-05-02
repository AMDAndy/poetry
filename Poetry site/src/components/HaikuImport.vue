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
      const fileContents = JSON.parse(contents) as Haiku[]
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
  <div>
    <div id="import-dialog">
      <label class="file-select">
        <input type="file" @change="handleFileChange" />
      </label>
    </div>
    <div id="btn-import">
      <button @click.prevent="$emit('addHaiku')">Import!</button>
      <button @click.prevent="$emit('cancel')">Cancel</button>
    </div>
  </div>
</template>

<style>
#btn-import {
  display: flex;
  justify-content: space-around;
}
</style>
