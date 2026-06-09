<script setup lang="ts">
const paymentLink = "/qr.png";
const isOpen = ref(false);
const step = ref(1);

const form = reactive({
  lastName: "",
  name: "",
  patronymic: "",
  contact: "",
  amount: "",
  comment: "",
});

const agreements = reactive({
  offer: false,
  amlKyc: false,
  personalData: false,
  riskDisclaimer: false,
});

const agreementText = {
  offer: "Я принимаю условия Публичной оферты",
  amlKyc: "Я ознакомлен с AML/KYC Policy",
  personalData: "Я согласен на обработку персональных данных",
  riskDisclaimer: "Я ознакомлен с уведомлением о рисках",
};

const allAgreementsAccepted = computed(() => {
  return agreements.offer && agreements.amlKyc && agreements.personalData && agreements.riskDisclaimer;
});

const paymentId = ref("");
const isSaving = ref(false);
const saveError = ref("");

const makePaymentId = () => {
  return "PAY-" + Date.now().toString().slice(-6);
};

const submit = async () => {
  saveError.value = "";
  isSaving.value = true;
  paymentId.value = makePaymentId();

  try {
    await $fetch("/api/leads", {
      method: "POST",
      body: {
        paymentId: paymentId.value,
        lastName: form.lastName,
        name: form.name,
        patronymic: form.patronymic,
        contact: form.contact,
        amount: form.amount,
        comment: form.comment,
        agreements: { ...agreements },
        agreementText,
        documentsVersion: "2026-06-09",
      },
    });

    step.value = 2;
  } catch (error) {
    saveError.value = "Не удалось сохранить заявку. Попробуйте ещё раз.";
  } finally {
    isSaving.value = false;
  }
};

const closeModal = () => {
  isOpen.value = false;
  step.value = 1;
};
</script>

<template>
  <section id="payment" class="payment-section">
    <div class="payment-card">
      <p class="eyebrow">Оплата заявки</p>
      <h2>Оплата согласованной заявки</h2>
      <p>
        Используйте форму ниже для оформления платежа по ранее согласованным условиям.
        После заполнения будет сформирован ID оплаты.
      </p>

      <button type="button" class="primary-button payment-button" @click="isOpen = true">
        Оплатить
      </button>
    </div>

    <div v-if="isOpen" class="modal-backdrop">
      <div class="modal-card" role="dialog" aria-modal="true">
        <button type="button" class="modal-close" aria-label="Закрыть" @click="closeModal">
          ✕
        </button>

        <div v-if="step === 1">
          <p class="eyebrow">Шаг 1</p>
          <h3>Данные для оформления платежа</h3>
          <p class="modal-note">
            Заполните данные. После продолжения будет сформирован ID оплаты и инструкция.
          </p>

          <form class="lead-form" @submit.prevent="submit">
            <div class="form-row fio-row">
              <input v-model="form.lastName" required type="text" placeholder="Фамилия">
              <input v-model="form.name" required type="text" placeholder="Имя">
              <input v-model="form.patronymic" required type="text" placeholder="Отчество">
            </div>
            <input v-model="form.contact" required type="text" placeholder="Telegram или телефон">
            <input v-model="form.amount" required type="text" placeholder="Сумма">
            <textarea v-model="form.comment" placeholder="Комментарий"></textarea>

            <div class="agreements-box">
              <label class="legal-check">
                <input v-model="agreements.offer" type="checkbox" required>
                <span>Я принимаю условия <NuxtLink to="/offer" target="_blank">Публичной оферты</NuxtLink>.</span>
              </label>

              <label class="legal-check">
                <input v-model="agreements.amlKyc" type="checkbox" required>
                <span>Я ознакомлен с <NuxtLink to="/aml-kyc" target="_blank">AML/KYC Policy</NuxtLink>.</span>
              </label>

              <label class="legal-check">
                <input v-model="agreements.personalData" type="checkbox" required>
                <span>Я согласен на <NuxtLink to="/personal-data-consent" target="_blank">обработку персональных данных</NuxtLink>.</span>
              </label>

              <label class="legal-check">
                <input v-model="agreements.riskDisclaimer" type="checkbox" required>
                <span>Я ознакомлен с <NuxtLink to="/risk-disclaimer" target="_blank">уведомлением о рисках</NuxtLink>.</span>
              </label>
            </div>

            <p v-if="saveError" class="form-error">
              {{ saveError }}
            </p>

            <button type="submit" class="primary-button form-submit" :disabled="isSaving || !allAgreementsAccepted">
              {{ isSaving ? "Сохраняем..." : "Продолжить" }}
            </button>
          </form>
        </div>

        <div v-else>
          <p class="eyebrow">Шаг 2</p>
          <h3>Инструкция по оплате</h3>

          <div class="payment-id-card">
            <span>ID оплаты</span>
            <strong>{{ paymentId }}</strong>
          </div>

          <ol class="instruction-list">
            <li>Перейдите к оплате по QR.</li>
            <li>Выполните перевод на указанную сумму.</li>
            <li>Сохраните чек после оплаты.</li>
            <li>При необходимости отправьте чек менеджеру.</li>
          </ol>

          <a :href="paymentLink" target="_blank" class="primary-button form-submit">
            Оплатить по QR
          </a>

          <p class="modal-note small-note">
            Условия платежа должны соответствовать ранее согласованной заявке.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>
