<script setup lang="ts">
import type { Haiku } from '@/models/Haiku'
import jsonUrl from '/Users/shemkl/test.json'

defineProps({
  haikus: {
    type: Object as () => { [key: string]: Haiku[] },
    required: true,
  },
})

function importJson() {
  try {
    //haikus.value[key].push()
    localStorage.setItem('haikus', JSON.stringify(jsonUrl))
  } catch (e) {
    console.log(e)
  }
}
</script>

<template>
  <div id="import-container">
    <label id="import-label" for="import-input" class="haiku-forms">URL:</label>
    <input id="import-input" placeholder="The end begins again." type="text" v-model="jsonUrl" />
  </div>
  <button @click.prevent="importJson">Import!</button>
</template>
