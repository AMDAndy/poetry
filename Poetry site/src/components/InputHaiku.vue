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
      <label id="second-line-label" for="second-line-input" class="haiku-forms">Second Line:</label>
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
