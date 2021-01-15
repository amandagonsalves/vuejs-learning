<template>
  <div>
    <h1 :style="{color}">Hello {{ name }}</h1>
    <input v-model="name">
    <a :href="link">Telegram</a>
  </div>
</template>

<script>
export default {
  data: () => ({
    name: 'Amanda',
    color: 'tomato',
    link: 'https://t.me/vuejsbrasil'
  })
}
</script>

<style>

</style>