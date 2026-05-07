<script setup lang="ts">
const paymentLink = "/qr.png";
const telegramUser = "ТВОЙ_НИК";

const isOpen = ref(false);
const step = ref(1);

const form = reactive({
  name: "",
  contact: "",
  amount: "",
  comment: "",
});

const paymentId = ref("");

const makePaymentId = () => {
  return "PAY-" + Date.now().toString().slice(-6);
};

const submit = () => {
  paymentId.value = makePaymentId();

  const text = encodeURIComponent(
    "Новая заявка\n\n" +
      "ID оплаты: " + paymentId.value + "\n" +
      "Имя: " + form.name + "\n" +
      "Контакт: " + form.contact + "\n" +
      "Сумма: " + form.amount + "\n" +
      "Комментарий: " + (form.comment || "-")
  );

  window.open("https://t.me/" + telegramUser + "?text=" + text, "_blank");

  step.value = 2;
};

const closeModal = () => {
  isOpen.value = false;
  step.value = 1;
};
</script>

<template>
  <section id="payment" class="py-20 border-t border-slate-800">
    <div class="mx-auto max-w-4xl px-4 text-center">
      <h2 class="text-4xl font-bold mb-4">
        Оплата согласованной заявки
      </h2>

      <p class="text-slate-300 mb-10">
        Используйте форму ниже для оформления платежа по ранее согласованным условиям.
      </p>

      <button
        type="button"
        class="rounded-2xl bg-white text-black font-bold px-10 py-4 hover:opacity-90 transition"
        @click="isOpen = true"
      >
        Оплатить
      </button>
    </div>

    <div
      v-if="isOpen"
      class="fixed inset-0 z-50 bg-black/70 flex items-center justify-center px-4"
    >
      <div class="w-full max-w-xl rounded-3xl bg-slate-900 border border-slate-700 p-6 relative">
        <button
          type="button"
          class="absolute right-5 top-5 text-slate-400 hover:text-white"
          @click="closeModal"
        >
          ✕
        </button>

        <div v-if="step === 1">
          <h3 class="text-2xl font-bold mb-3">
            Данные для оформления платежа
          </h3>

          <p class="text-slate-400 mb-6">
            Заполните данные. После продолжения будет сформирован ID оплаты и инструкция.
          </p>

          <form class="grid gap-4" @submit.prevent="submit">
            <input
              v-model="form.name"
              required
              type="text"
              placeholder="Ваше имя"
              class="rounded-2xl bg-slate-950 border border-slate-700 px-5 py-4"
            >

            <input
              v-model="form.contact"
              required
              type="text"
              placeholder="Telegram или телефон"
              class="rounded-2xl bg-slate-950 border border-slate-700 px-5 py-4"
            >

            <input
              v-model="form.amount"
              required
              type="text"
              placeholder="Сумма"
              class="rounded-2xl bg-slate-950 border border-slate-700 px-5 py-4"
            >

            <textarea
              v-model="form.comment"
              placeholder="Комментарий"
              class="rounded-2xl bg-slate-950 border border-slate-700 px-5 py-4 min-h-28"
            ></textarea>

            <button
              type="submit"
              class="rounded-2xl bg-white text-black font-bold py-4 hover:opacity-90 transition"
            >
              Продолжить
            </button>
          </form>
        </div>

        <div v-else>
          <h3 class="text-2xl font-bold mb-3">
            Инструкция по оплате
          </h3>

          <div class="rounded-2xl bg-slate-950 border border-slate-700 p-5 mb-6">
            <p class="text-slate-400 mb-1">
              ID оплаты
            </p>
            <p class="text-2xl font-bold">
              {{ paymentId }}
            </p>
          </div>

          <ol class="grid gap-3 text-slate-300 mb-6">
            <li>1. Перейдите к оплате по QR.</li>
            <li>2. Выполните перевод на указанную сумму.</li>
            <li>3. Сохраните чек после оплаты.</li>
            <li>4. При необходимости отправьте чек менеджеру.</li>
          </ol>

          <a
            :href="paymentLink"
            target="_blank"
            class="block rounded-2xl bg-emerald-400 text-black font-bold py-4 text-center hover:opacity-90 transition"
          >
            Оплатить по QR
          </a>

          <p class="text-sm text-slate-500 mt-5">
            Условия платежа должны соответствовать ранее согласованной заявке.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>
