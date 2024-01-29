<script setup lang="ts">
import { computed, reactive, ref } from "vue";

const lancer = reactive({
  lancerID: 0,
  company: "",
  faction: "",
  lastname: "",
  firstname: "",
  alive: true
}) // Fetch JSON data of Mercenary Pilots

function validateLancerID(){
  computed(() => {
    return lancer.lancerID >= 0 ? true : false
  })
}

function healthCheck(){
  computed(() => {
    return lancer.alive == true ? false : validateLancerID()
  })
} // check DB schema validation for conditional rendering
</script>

<template>
  <article :class="styles.Card">
    <div>{{ validateLancerID() }}</div>
    <span>{{ healthCheck() }}</span>
    <h1>{{ lancer.company }}</h1>
    <h2>{{ lancer.faction }}</h2>
    <i>{{ lancer.lastname }}</i>
    <p>{{ lancer.firstname }}</p>
  </article>
</template>

<style scoped module="styles" lang="sass">
@mixin theme($theme: Sunbather)
  background: $theme
  color: #1e1c1d

.Card
  @include theme
</style>
