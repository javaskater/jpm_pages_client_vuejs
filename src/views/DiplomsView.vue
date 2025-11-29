<template>
  <main>
    <h2>Les diplômes</h2>
  </main>
</template>

<script setup>
import { reactive, ref } from 'vue'
import { useRoute } from 'vue-router'

const diploms = reactive({})
const route = useRoute()
const language = route.params.lang
const fetchUser = (lang) => {
  const url = `http://localhost/diploms/${lang}`
  fetch(url, {})
    .then((response) => response.json())
    .then((result) => {
      Object.assign(diploms, result.data)
      diploms.data.map((x) => console.log(`${x.schoolName} - ${x.cursusDescription}`))
    })
}

fetchUser(language)
</script>
