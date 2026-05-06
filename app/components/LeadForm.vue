<script setup lang="ts">
const form = reactive({
  name: "",
  contact: "",
  amount: "",
  direction: "Купить USDT",
  comment: "",
});

const submit = () => {
  const text = `Заявка Fluxora:%0A
Имя: ${form.name}%0A
Контакт: ${form.contact}%0A
Направление: ${form.direction}%0A
Сумма: ${form.amount}%0A
Комментарий: ${form.comment}`;

  window.open(`https://t.me/ТВОЙ_НИК?text=${text}`, "_blank");
};
</script>

<template>
  <section id="lead" class="py-20 bg-slate-950 text-white">
    <div class="mx-auto max-w-4xl px-4">
      <h2 class="text-3xl font-bold mb-4">
        Оставьте заявку на покупку или продажу USDT
      </h2>

      <p class="mb-8 text-slate-300">
        Напишите сумму и удобный способ связи. Мы уточним детали, курс, порядок сделки и необходимые документы.
      </p>

      <form @submit.prevent="submit" class="grid gap-4">
        <input v-model="form.name" required placeholder="Ваше имя"
          class="rounded-xl px-4 py-3 text-black" />

        <input v-model="form.contact" required placeholder="Telegram или телефон"
          class="rounded-xl px-4 py-3 text-black" />

        <select v-model="form.direction" class="rounded-xl px-4 py-3 text-black">
          <option>Купить USDT</option>
          <option>Продать USDT</option>
          <option>Обсудить обмен</option>
        </select>

        <input v-model="form.amount" placeholder="Сумма, например 100 000 ₽"
          class="rounded-xl px-4 py-3 text-black" />

        <textarea v-model="form.comment" placeholder="Комментарий"
          class="rounded-xl px-4 py-3 text-black min-h-28"></textarea>

        <button class="rounded-xl bg-white text-slate-950 font-bold py-4">
          Отправить заявку
        </button>
      </form>

      <p class="mt-6 text-sm text-slate-400">
        Операции проводятся после проверки заявки. Сервис не является инвестиционной рекомендацией.
      </p>
    </div>
  </section>
</template>