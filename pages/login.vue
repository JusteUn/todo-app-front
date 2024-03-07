<script setup lang="ts">
import { object, string } from "yup";
import type { FormSubmitEvent } from "#ui/types";

const schema = object({
  email: string().email().required("Email is required"),
  password: string().required("Password is required"),
});

const state = reactive({
  email: undefined,
  password: undefined,
});

async function onSubmit(event: FormSubmitEvent<any>) {
  console.log(event.data);
}

definePageMeta({
  layout: "auth",
});
</script>

<template>
  <UCard>
    <div class="mx-auto flex w-full max-w-lg flex-col gap-3 p-10">
      <h1 class="text-2xl font-bold">Login</h1>
      <UDivider />
      <div>
        <UForm
          :schema="schema"
          :state="state"
          class="space-y-3"
          @submit="onSubmit"
        >
          <UFormGroup label="Email" name="email">
            <UInput
              v-model="state.email"
              icon="i-heroicons-user-16-solid"
              size="sm"
              color="white"
              :trailing="false"
              placeholder="john.doe@gmail.com"
              dynamic
            />
          </UFormGroup>
          <UFormGroup label="Password" name="password">
            <UInput
              v-model="state.password"
              icon="i-heroicons-key-16-solid"
              size="sm"
              color="white"
              :trailing="false"
              placeholder="••••••••"
              type="password"
            />
          </UFormGroup>
          <UButton type="submit"> Submit </UButton>
        </UForm>
      </div>
      <UDivider />
      <div class="flex justify-center">
        <ULink to="/register">Don't have an account? Register</ULink>
      </div>
    </div>
  </UCard>
</template>
