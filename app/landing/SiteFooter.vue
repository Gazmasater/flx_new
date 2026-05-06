<script setup lang="ts">
defineProps<{
  company: {
    legalName: string;
  };
}>();

const year = new Date().getFullYear();
</script>

<template>
  <footer class="footer">
    <div>© {{ year }} {{ company.legalName }}</div>

    <nav aria-label="Документы">
      <NuxtLink to="/offer">Оферта</NuxtLink>
      <NuxtLink to="/privacy">Политика конфиденциальности</NuxtLink>
    </nav>
  </footer>
</template>