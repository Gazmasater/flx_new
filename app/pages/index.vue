<script setup lang="ts">
import { company } from "../data/company";
import { advantages, services, steps } from "../data/landing";
</script>

<template>
  <div class="site-shell">
    <SiteHeader :company="company" />

    <main>
      <HeroSection />
      <ServicesSection :services="services" />
      <ProcessSection :steps="steps" />
      <AdvantagesSection :advantages="advantages" />
      <ContactsSection :company="company" />
      <LeadForm />
    </main>

    <SiteFooter :company="company" />
  </div>
</template>
