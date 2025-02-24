<script setup lang="ts">
import { ref } from 'vue'

export type Haiku = {
  author: string
  prompt: string
  haiku: string
}

const haikus = ref<{ [key: string]: Haiku[] }>({})

const formAuthor = ref('')
const formPrompt = ref('')
const formHaiku = ref('')

function clearFields(): void {
  formAuthor.value = ''
  formPrompt.value = ''
  formHaiku.value = ''
}

function addHaiku(): void {
  const key = formAuthor.value
  const newHaiku: Haiku = {
    author: formAuthor.value,
    prompt: formPrompt.value,
    haiku: formHaiku.value,
  }

  if (!haikus.value[key]) {
    haikus.value[key] = []
  }
  haikus.value[key].push(newHaiku)
  console.log(newHaiku)
  clearFields()
}
</script>

<template>
  <main>
    <div class="home-haiku">
      <p>Place here a sentence.</p>
      <p>Gently we all grow through life.</p>
      <p>The end begins again.</p>
    </div>
    <form>
      <div id="haiku-form">
        <label id="author-label" for="author-input" class="haiku-forms">Author:</label>
        <input id="author-input" type="text" v-model="formAuthor" />
        <label id="prompt-label" for="prompt-input" class="haiku-forms">Prompt:</label>
        <input id="prompt-input" type="text" v-model="formPrompt" />
        <label id="haiku-label" for="haiku-input" class="haiku-forms">Haiku:</label>
        <input id="haiku-input" type="text" v-model="formHaiku" />
        <button id="click-add" @click.prevent="addHaiku">Submit haiku :3</button>
        <button id="click-reset" @click.prevent="clearFields">o no D:!</button>
      </div>
    </form>
  </main>
  <div id="haiku-list">
    <li v-for="(myHaikus, key) in haikus" :key="key">
      <strong>{{ key }}</strong>
      <ul>
        <li v-for="haiku in myHaikus" :key="haiku.author">
          <p>Author: {{ haiku.author }}</p>
          <p>Prompt: {{ haiku.prompt }}</p>
          <p>Haiku: {{ haiku.haiku }}</p>
        </li>
      </ul>
    </li>
  </div>
</template>

<style>
#click-reset {
  margin-top: 1em;
}
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
