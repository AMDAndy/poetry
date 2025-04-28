<script setup lang="ts">
import type { Haiku } from '@/models/Haiku'
import HaikuList from './HaikuList.vue'
import HaikuImport from './HaikuImport.vue'
import { ref } from 'vue'

const haikus = ref<{ [key: string]: Haiku[] }>({})

const showImport = ref(false)

const formAuthor = ref('')
const formPrompt = ref('')
const formFirstLine = ref('')
const formSecondLine = ref('')
const formThirdLine = ref('')

function clearFields(): void {
  formAuthor.value = ''
  formPrompt.value = ''
  formFirstLine.value = ''
  formSecondLine.value = ''
  formThirdLine.value = ''
}

function addHaiku(): void {
  const key = formAuthor.value

  const newHaiku: Haiku = {
    author: formAuthor.value,
    prompt: formPrompt.value,
    firstLine: formFirstLine.value,
    secondLine: formSecondLine.value,
    thirdLine: formThirdLine.value,
  }

  if (!haikus.value[key]) {
    haikus.value[key] = []
  }

  haikus.value[key].push(newHaiku)
  localStorage.setItem('haikus', JSON.stringify(haikus.value))
  clearFields()
}

function getHaikus(): void {
  const storedHaikus = localStorage.getItem('haikus')
  if (storedHaikus) {
    haikus.value = JSON.parse(storedHaikus)
  }
}

function deleteAuthor(author: string): void {
  delete haikus.value[author]
  localStorage.setItem('haikus', JSON.stringify(haikus.value))
}

function deleteHaiku(author: string, index: number): void {
  haikus.value[author].splice(index, 1)
  localStorage.setItem('haikus', JSON.stringify(haikus.value))
}

// FIXME: ANDY FIX IT
// this doesn't work ;w;
function importJson(jsonUrl: Haiku): void {
  // formAuthor.value = jsonUrl.author
  // formPrompt.value = jsonUrl.prompt
  // formFirstLine.value = jsonUrl.firstLine
  // formSecondLine.value = jsonUrl.secondLine
  // formThirdLine.value = jsonUrl.thirdLine

  // const newHaiku: Haiku = {
  //   author: formAuthor.value,
  //   prompt: formPrompt.value,
  //   firstLine: formFirstLine.value,
  //   secondLine: formSecondLine.value,
  //   thirdLine: formThirdLine.value,
  // }

  // const key = formAuthor.value

  // if (!haikus.value[key]) {
  //   haikus.value[key] = []
  // }

  try {
    console.log(jsonUrl)
    // haikus.value[key].push(newHaiku)
    localStorage.setItem('haikus', JSON.stringify(jsonUrl))
    console.log('aaaaaaaaaaaaaaaaaaa')
  } catch {
    console.log('oh no!!!!!!!!')
  }
}

function cancelImport() {
  showImport.value = false
}

getHaikus()
</script>

<template>
  <div id="haikutainer">
    <form>
      <div id="haiku-form">
        <label id="author-label" for="author-input" class="haiku-forms">Author:</label>
        <input id="author-input" placeholder="Merpsy Werpsy" type="text" v-model="formAuthor" />
        <label id="prompt-label" for="prompt-input" class="haiku-forms">Prompt:</label>
        <input id="prompt-input" placeholder="viscera" type="text" v-model="formPrompt" />
        <label id="first-line-label" for="first-line-input" class="haiku-forms">First Line:</label>
        <input
          id="first-line-input"
          placeholder="Place here a sentence."
          type="text"
          v-model="formFirstLine"
        />
        <label id="second-line-label" for="second-line-input" class="haiku-forms"
          >Second Line:</label
        >
        <input
          id="second-line-input"
          placeholder="Gently we all grow through life."
          type="text"
          v-model="formSecondLine"
        />
        <label id="third-line-label" for="third-line-input" class="haiku-forms">Third Line:</label>
        <input
          id="third-line-input"
          placeholder="The end begins again."
          type="text"
          v-model="formThirdLine"
        />
        <button id="click-add" @click.prevent="addHaiku">Submit haiku :3</button>
        <button id="click-reset" @click.prevent="clearFields">o no D:!</button>
      </div>
    </form>
  </div>
  <div id="import-container">
    <button id="click-import" @click.prevent="showImport = !showImport">Import Haiku ...</button>
    <div v-if="showImport">
      <HaikuImport :haikus="haikus" @importJson="importJson" @cancel="cancelImport" />
    </div>
  </div>

  <HaikuList :haikus="haikus" @delete-haiku="deleteHaiku" @delete-author="deleteAuthor" />
</template>

<style>
#import-container {
  margin-top: 1rem;
  background-color: rgb(74, 65, 130);
}
#click-import {
  margin-top: 1em;
}
#haikutainer {
  margin: auto;
  background-color: rgb(74, 65, 130);
  padding: 1rem;
}

main {
  margin: auto;
  padding: 1rem;
}

#haiku-form {
  display: grid;
  grid-template-columns: auto;
  justify-content: left;
}

#haiku-list {
  display: grid;
  grid-template-columns: auto;
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
  margin: 0.3em;
  padding: 1em;
  &:active,
  &:focus {
    background-color: rgb(184, 174, 245);
  }
  &:disabled {
    color: silver;
  }
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
