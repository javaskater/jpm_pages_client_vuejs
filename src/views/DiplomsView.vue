<template>
  <main>
    <h2>{{ title }}</h2>
    <ul>
      <li v-for="diplom in diploms">{{ diplom.schoolName }} - {{ diplom.cursusDescription }}</li>
    </ul>
  </main>
</template>

<script setup>
import { reactive, ref } from 'vue'
import { useRoute } from 'vue-router'

const diploms = reactive({})
const route = useRoute()
const language = route.params.lang
const title = ref('')
switch (language) {
  case 'fr_FR':
    title.value += 'Les Diplômes obtenus'
    break
  case 'de_DE':
    title.value += 'Erhaltene Diplome'
    break
  default:
    title.value += 'Diplomas obtained'
}
const fetchUser = (lang) => {
  const url = `http://localhost:8081/diploms/${lang}`
  fetch(url, {
    method: 'GET',
    headers: {
      Accept: 'application/json',
    },
  })
    .then((response) => {
      console.log(`[then1] Retour d'une réponse pour ${url}`)
      var jsonData = response.json()
      console.log(`[then1] response vaut ${jsonData}`)
      return jsonData
    })
    .then((result) => {
      console.log(`[then2] données result valent ${result}`)
      Object.assign(diploms, result)
      result.forEach((x) => console.log(`${x.schoolName} - ${x.cursusDescription}`))
    })
}

fetchUser(language)
</script>
