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
main {
  background-color: rgb(74, 65, 130);
  margin: auto;
  padding: 1rem;
}

#haiku-form {
  display: grid;
  grid-template-columns: auto;
  justify-content: left;
}

#haiku-list {
  text-align: center;
  max-width: fit-content;
  margin: auto;
}

.home-haiku > p {
  height: 0;
  padding-bottom: 0.7rem;
}

#click-add {
  margin-top: 1rem;
}

.home-haiku {
  text-align: center;
  color: antiquewhite;
}

.home-haiku,
.haiku-forms {
  display: grid;
  grid-template-columns: auto;
  max-width: fit-content;
  margin: auto;
}

button {
  outline: none;
  border: none;
  border-radius: 3px;
  background-color: rgb(134, 124, 195);
  color: antiquewhite;
  padding: 1em;
}

label {
  padding-top: 1.5em;
}

input {
  color: antiquewhite;
  background-color: rgb(166, 158, 219);
  border: none;
  border-radius: 3px;
  padding: 12px 10px;
}

input:focus {
  outline: none;
  box-shadow: 0 0 5px #950cbb;
  background-color: rgb(81, 70, 157);
  transition:
    color 0.5s,
    background-color 0.5s;
  border: none;
}
</style>
