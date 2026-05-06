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

      <section id="lead" class="py-20 border-t border-slate-800">
        <div class="mx-auto max-w-4xl px-4">
          <h2 class="text-4xl font-bold mb-4">
            Оставьте заявку
          </h2>

          <p class="text-slate-300 mb-10">
            Покупка и продажа USDT. Укажите удобный способ связи и сумму сделки.
          </p>

          <form
            class="grid gap-4"
            @submit.prevent="
              () => {
                window.open(
                  `https://t.me/ТВОЙ_НИК`,
                  '_blank'
                )
              }
            "
          >
            <input
              type="text"
              placeholder="Ваше имя"
              class="rounded-2xl bg-slate-900 border border-slate-700 px-5 py-4"
            />

            <input
              type="text"
              placeholder="Telegram или телефон"
              class="rounded-2xl bg-slate-900 border border-slate-700 px-5 py-4"
            />

            <select
              class="rounded-2xl bg-slate-900 border border-slate-700 px-5 py-4"
            >
              <option>Купить USDT</option>
              <option>Продать USDT</option>
              <option>Консультация</option>
            </select>

            <input
              type="text"
              placeholder="Сумма"
              class="rounded-2xl bg-slate-900 border border-slate-700 px-5 py-4"
            />

            <textarea
              placeholder="Комментарий"
              class="rounded-2xl bg-slate-900 border border-slate-700 px-5 py-4 min-h-32"
            ></textarea>

            <button
              class="rounded-2xl bg-white text-black font-bold py-4 hover:opacity-90 transition"
            >
              Отправить заявку
            </button>
          </form>

          <p class="text-sm text-slate-500 mt-6">
            Перед проведением сделки может потребоваться подтверждение личности и источника средств.
          </p>
        </div>
      </section>
    </main>

    <SiteFooter :company="company" />
  </div>
</template>