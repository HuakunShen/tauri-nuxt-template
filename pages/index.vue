<script setup>
const { locale } = useI18n()
</script>

<template>
  <div>
    <NuxtLink to="/about">About</NuxtLink>
    <form>
      <select v-model="locale">
        <option value="en">en</option>
        <option value="fr">fr</option>
      </select>
      <p>{{ $t('welcome') }}</p>
    </form>
  </div>
</template>
