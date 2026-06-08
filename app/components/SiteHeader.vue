<script setup lang="ts">
defineProps<{
  company: {
    brand: string;
  };
}>();
</script>

<template>
  <header class="topbar">
    <NuxtLink class="brand" to="/" aria-label="Главная">
      <span class="brand-mark">F</span>
      <span>{{ company.brand }}</span>
    </NuxtLink>

    <nav class="nav" aria-label="Разделы сайта">
      <a href="/#services">Услуги</a>
      <a href="/#process">Процесс</a>
      <a href="/#contacts">Контакты</a>
      <NuxtLink to="/documents">Документы</NuxtLink>
    </nav>
  </header>
</template>
