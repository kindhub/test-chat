<template>
  <div>
    <UCard class="max-w-[600px] mx-auto" :ui="{ body: { padding: 'p-5 sm:p-8' } }">
      <template #header>
        <div class="flex items-center justify-center gap-x-3 text-primary">
          <div class="text-primary font-semibold text-center text-3xl">Тестовый чат</div>
        </div>
      </template>

      <UForm :state="state" @submit="onSubmit" class="space-y-6">
        <UFormGroup label="Пользователь" name="username">
          <UInput v-model="state.username" />
        </UFormGroup>

        <UFormGroup label="Комната" name="room">
          <USelect v-model="state.room" :options="rooms" />
        </UFormGroup>

        <UButton type="submit" size="xl" block :disabled="!state.username || !state.room">
          Войти
        </UButton>
      </UForm>
    </UCard>
  </div>
</template>

<script setup lang="ts">
import type { FormSubmitEvent } from '#ui/types';
const rooms = ['Чат1', 'Чат2'];
const state = reactive({
  username: '',
  room: rooms[0],
});

async function onSubmit(event: FormSubmitEvent<any>) {
  navigateTo(`/chat?username=${state.username}&room=${state.room}`);
}
</script>

<style scoped></style>
