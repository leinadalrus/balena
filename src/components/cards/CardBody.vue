<script setup lang="ts">
import {
  defineProps,
  reactive,
  ref,
  watch
} from "vue"

defineProps(["flavour", "description"])
</script>

<template>
  <address>
    {{ flavour }}
  </address>
  <span>
    {{ description }}
  </span>
</template>

<style scoped module="styles" lang="scss">
</style>

