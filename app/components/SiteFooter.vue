<script setup lang="ts">
defineProps<{
  company: {
    fullLegalName: string;
    inn: string;
    ogrnip: string;
  };
}>();

const year = new Date().getFullYear();
</script>

<template>
  <footer class="footer">
    <div>© {{ year }} {{ company.fullLegalName }} · ИНН {{ company.inn }} · ОГРНИП {{ company.ogrnip }}</div>

    <nav aria-label="Документы">
      <NuxtLink to="/documents">Документы</NuxtLink>
      <NuxtLink to="/offer">Оферта</NuxtLink>
      <NuxtLink to="/aml-kyc">AML/KYC</NuxtLink>
      <NuxtLink to="/privacy">ПДн</NuxtLink>
      <NuxtLink to="/cookies">Cookies</NuxtLink>
    </nav>
  </footer>
</template>
