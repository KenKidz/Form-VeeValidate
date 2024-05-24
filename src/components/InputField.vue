<template>
  <label :for="$attrs.id">{{ label }}</label>
  <input v-bind="$attrs" v-model="value">
  <span class="error" v-show="error">{{ error }}</span>
</template>

<script setup lang="ts">
defineOptions({
  name: 'InputField',
  inheritAttrs: false,
})
import {useField} from "vee-validate";

interface Prop {
  label: string
  error: string
}
defineProps<Prop>()
const attrs : any = useAttrs()

const {value} = useField(attrs.id)
</script>

<style scoped>
.error {
  color: red;
}
</style>
