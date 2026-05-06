<script setup lang="ts">
defineProps<{
  company: {
    legalName: string;
    inn: string;
    email: string;
  };
}>();
</script>

<template>
  <section id="contacts" class="contacts">
    <div>
      <p class="eyebrow">Контакты</p>
      <h2>Реквизиты компании</h2>
      <p>
        Используйте этот блок для официальной презентации перед банком, процессинговыми
        партнёрами и корпоративными клиентами.
      </p>
    </div>

    <div class="contact-list">
      <div>
        <span>Компания</span>
        <strong>{{ company.legalName }}</strong>
      </div>

      <div>
        <span>ИНН</span>
        <strong>{{ company.inn }}</strong>
      </div>

      <div>
        <span>Email</span>
        <a :href="`mailto:${company.email}`">{{ company.email }}</a>
      </div>
    </div>
  </section>
</template>