<template>
  <Form :validation-schema="validationSchema" @submit="onSubmit">
    <label for="email">Email</label>
    <Field id="email" type="text" name="abc" ></Field>
    <ErrorMessage name="abc" class="error"></ErrorMessage>

    <label for="password">Password</label>
    <Field id="password" type="text" name="password" ></Field>
    <ErrorMessage name="password" class="error"></ErrorMessage>

    <button type="submit">Submit</button>
  </Form>
</template>

<script setup lang="ts">

import {toTypedSchema} from "@vee-validate/zod";
import {z} from "zod";
import {ErrorMessage, Form, Field} from "vee-validate";

const validationSchema = toTypedSchema(z.object({
  abc: z.string().min(1, 'this is required').email('It needs to be an email'),
  password: z.string().min(8, 'Too short')
}))

const onSubmit = (values: any) => {
  alert(JSON.stringify(values, null, 2))
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  max-width: 15rem;
  margin: 0 auto;
}

.error {
  color: red;
}
</style>
