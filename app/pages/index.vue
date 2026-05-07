<script setup lang="ts">
import { company } from "../data/company";
import { advantages, services, steps } from "../data/landing";
</script>

<template>
  <div class="bg-slate-950 text-white min-h-screen">
    <SiteHeader :company="company" />

    <main>
      <HeroSection :company="company" />
      <ServicesSection :services="services" />
      <ProcessSection :steps="steps" />
      <AdvantagesSection :advantages="advantages" />
      <ContactsSection :company="company" />

      <LeadForm />
    </main>

    <SiteFooter :company="company" />
  </div>
</template>