<template>
  <form @submit="onSubmit">
    <InputField id="email" type="text" label="Email" :error="errors.email"/>
    <InputField id="password" type="password" label="Password" :error="errors.password"/>
    <button>Submit</button>
  </form>
</template>

<script setup lang="ts">
import {toTypedSchema} from "@vee-validate/zod";
import {z} from "zod";
import {useForm} from 'vee-validate';

const validationSchema = toTypedSchema(
    z.object({
      email: z.string().min(1, 'this is required').email('It needs to be an email'),
      password: z.string().min(8, 'Too short')
    }))
const {handleSubmit, errors} = useForm({
  validationSchema,
});

const onSubmit = handleSubmit(values => {
  alert(JSON.stringify(values, null, 2));
});
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  max-width: 15rem;
  margin: 0 auto;
}
</style>
