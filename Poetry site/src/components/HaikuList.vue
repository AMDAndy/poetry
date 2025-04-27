<script setup lang="ts">
import type { Haiku } from '@/models/Haiku'

defineProps({
  haikus: {
    type: Object as () => { [key: string]: Haiku[] },
    required: true,
  },
})

const emit = defineEmits(['delete-haiku', 'delete-author'])

function sendDeleteHaiku(key: string, index: number) {
  emit('delete-haiku', key, index)
}

function sendDeleteAuthor(key: string | number, index: number) {
  emit('delete-author', key, index)
}
</script>

<template>
  <div id="haiku-list">
    <li v-for="(myHaikus, author, authorIndex) in haikus" :key="author">
      <strong>{{ author }}</strong>
      <button @click="sendDeleteAuthor(author, authorIndex)">Delete author</button>
      <ul>
        <li v-for="(haiku, haikuIndex) in myHaikus" :key="haiku.prompt">
          <button @click="sendDeleteHaiku(haiku.author, haikuIndex)">Delete haiku</button>
          <br />
          <p>{{ haiku.prompt }}</p>
          <p>
            {{ haiku.firstLine }}
            <br />
            {{ haiku.secondLine }}
            <br />
            {{ haiku.thirdLine }}
            <br />
          </p>
        </li>
      </ul>
    </li>
  </div>
</template>
