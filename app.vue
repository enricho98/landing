<script setup lang="ts">
useHead({
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  link: [
    { rel: 'icon', href: 'public/favicon.jpg' }
  ],
  htmlAttrs: {
    lang: 'en'
  }
})
useSeoMeta({
})

</script>

<template>
  <Header />
  <Whatsapp />

  <UMain>
    <NuxtPage />
  </UMain>

  <Footer />

  <UNotifications />
</template>
