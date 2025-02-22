<script setup lang="ts">
import { ref } from 'vue'

let author: string = ''
let prompt: string = ''
let haiku: string = ''

const containsHaikus = ref(false)
const haikus = ref([{}])

function clearFields(): void {
  author = ''
  prompt = ''
  haiku = ''
}

function addHaiku(): void {
  haikus.value.push({ author: author, prompt: prompt, haiku: haiku })
  clearFields()
  containsHaikus.value = true
}
</script>

<template>
  <main>
    <div class="what-to-do">
      <p>Place here a sentence.</p>
      <p>Gently we all grow through life.</p>
      <p>The end begins again.</p>
    </div>
    <div class="haiku-forms">
      Author:
      <input type="text" v-model="author" required />
    </div>
    <div id="prompt" for="prompt" class="haiku-forms">
      Prompt:
      <input id="prompt-input" type="text" v-model="prompt" required />
    </div>
    <div class="haiku-forms">
      Haiku:
      <input type="text" v-model="haiku" required />
      <button id="click-add" @click="addHaiku">Click me</button>
    </div>
    <div id="haiku-list">
      <ul v-if="containsHaikus">
        <li v-for="(item, key) in haikus" :key="key">{{ item }}</li>
      </ul>
      <p v-else>nipples</p>
    </div>
  </main>
</template>

<style>
#haiku-list {
  text-align: center;
  max-width: fit-content;
  margin: auto;
}
.what-to-do > p {
  height: 0;
  padding-bottom: 0.7rem;
}

#click-add {
  margin-top: 1rem;
}

.what-to-do {
  text-align: center;
}

.what-to-do,
.haiku-forms {
  display: grid;
  grid-template-columns: auto;
  max-width: fit-content;
  margin: auto;
}
</style>
