<script setup lang="ts">
import { object, string, ref } from "yup";
import type { FormSubmitEvent } from "#ui/types";

const schema = object({
  email: string().email().required("Email is required"),
  password: string()
    .min(8, "Password required at least 8 characters")
    .required("Password is required"),
  passwordConfirmation: string()
    .oneOf([ref("password")], "Passwords must match")
    .required("Password confirmation is required"),
  username: string().required("Username is required"),
  firstname: string().required("First name is required"),
  lastname: string().required("Last name is required"),
});

const state = reactive({
  email: undefined,
  password: undefined,
  passwordConfirmation: undefined,
  username: undefined,
  firstname: undefined,
  lastname: undefined,
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
      <h1 class="text-2xl font-bold">Register</h1>
      <UDivider />
      <div>
        <UForm
          :schema="schema"
          :state="state"
          class="space-y-3"
          @submit="onSubmit"
        >
          <div class="flex flex-row gap-3">
            <UFormGroup label="Firstname" name="firstname">
              <UInput
                v-model="state.firstname"
                icon="i-heroicons-user-16-solid"
                size="sm"
                color="white"
                :trailing="false"
                placeholder="John"
              />
            </UFormGroup>
            <UFormGroup label="Lastname" name="lastname">
              <UInput
                v-model="state.lastname"
                icon="i-heroicons-user-16-solid"
                size="sm"
                color="white"
                :trailing="false"
                placeholder="Doe"
                dynamic
              />
            </UFormGroup>
          </div>
          <UFormGroup label="Username" name="username">
            <UInput
              v-model="state.username"
              icon="i-heroicons-user-16-solid"
              size="sm"
              color="white"
              :trailing="false"
              placeholder="johndoe"
              dynamic
            />
          </UFormGroup>
          <UFormGroup label="Email" name="email">
            <UInput
              v-model="state.email"
              icon="i-heroicons-user-16-solid"
              size="sm"
              color="white"
              :trailing="false"
              placeholder="john.doe@gmail.com"
            />
          </UFormGroup>
          <div class="flex flex-row gap-2">
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
            <UFormGroup label="Confirme password" name="passwordConfirmation">
              <UInput
                v-model="state.passwordConfirmation"
                icon="i-heroicons-key-16-solid"
                size="sm"
                color="white"
                :trailing="false"
                placeholder="••••••••"
                type="password"
              />
            </UFormGroup>
          </div>
          <UButton type="submit"> Submit </UButton>
        </UForm>
      </div>
      <UDivider />
      <div class="flex justify-center">
        <ULink to="/login">Already have an account ? Login</ULink>
      </div>
    </div>
  </UCard>
</template>
