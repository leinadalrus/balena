<script lang="ts">
import { computed, reactive, ref } from "vue";
import TradingCard from "../cards/TradingCard.vue"

const players = reactive([ref(TradingCard)])
const tabletop = ref([[]])
</script>

<template>
  <section>
  </section>
</template>

<style scoped module="styles" lang="sass"></style>
