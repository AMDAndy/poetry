<script setup lang="ts">
import type { Haiku } from '@/models/Haiku'
import { ref } from 'vue'

const haikus = ref<{ [key: string]: Haiku[] }>({})

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
  clearFields()
}
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

<style>
#click-reset {
  margin-top: 1em;
}

/* I'm lazy, will fix later */
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
