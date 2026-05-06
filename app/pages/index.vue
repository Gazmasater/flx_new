
<script setup lang="ts">
import { company } from "~/data/company";
import { advantages, services, steps } from "~/data/landing";

useHead({
  title: "IT-платформа для обработки данных и интеграций",
  meta: [
    {
      name: "description",
      content:
        "Презентационный сайт IT-компании: платформа для обработки данных, интеграций и автоматизации бизнес-процессов.",
    },
  ],
});
</script>

<template>
  <main class="site-shell">
    <SiteHeader :company="company" />
    <HeroSection />
    <ServicesSection :services="services" />
    <ProcessSection :steps="steps" />
    <AdvantagesSection :advantages="advantages" />
    <ContactsSection :company="company" />
    <SiteFooter :company="company" />
  </main>
</template>