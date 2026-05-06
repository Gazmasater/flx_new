    <script setup lang="ts">
import { company } from "../data/company";
import { advantages, services, steps } from "../data/landing";
</script>

<template>
  <div>
    <SiteHeader :company="company" />

    <main>
      <HeroSection :company="company" />
      <ServicesSection :services="services" />
      <ProcessSection :steps="steps" />
      <AdvantagesSection :advantages="advantages" />
      <ContactsSection :company="company" />
    </main>

    <SiteFooter :company="company" />
  </div>
</template>