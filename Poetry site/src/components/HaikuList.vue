<script setup lang="ts">
import type { Haiku } from '@/models/Haiku'

defineProps({
  haikus: {
    type: Object as () => { [key: string]: Haiku[] },
    required: true,
  },
})
</script>

<template>
  <div id="haiku-list">
    <li v-for="(myHaikus, key) in haikus" :key="key">
      <strong>{{ key }}</strong>
      <ul>
        <li v-for="haiku in myHaikus" :key="haiku.prompt">
          <p>{{ haiku.prompt }}</p>
          <p>{{ haiku.firstLine }}<br />{{ haiku.secondLine }}<br />{{ haiku.thirdLine }}<br /></p>
        </li>
      </ul>
    </li>
  </div>
</template>
