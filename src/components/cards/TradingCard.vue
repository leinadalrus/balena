<script setup lang="ts">
import {
  computed,
  onMounted,
  onUnmounted,
  reactive,
  ref,
  watch
} from "vue"

enum DeadOrAlives {
  Dead = 0,
  Alive = 1,
  Unknown = Dead | Alive
}

const Lancer = reactive({
  lancerID: 0,
  company: "",
  faction: "",
  lastname: "",
  firstname: "",
  alive: true
}) // Fetch JSON data of Mercenary Pilots

defineProps<{
  lancer?: typeof Lancer
}>() // if using typescript pure-type annotations

function validateLancerID() {
  computed(() => {
    return Lancer.lancerID >= 0 ? true : false
  })
}

function lancerIsLiving() {
  computed(() => {
    return Lancer.alive == true ? false : DeadOrAlives.Unknown
  })
} // check DB schema validation for conditional rendering

const positionX0 = ref(0)
const positionY0 = ref(0)

const damageComparator = defineEmits({
  submit: ({ attack, defence }) => {
    if (attack > defence)
      return true
    else
      return false
  }
}) // declarative tuple inference akin to `ruby`

function updateVector2s(mouseEvent: MouseEvent) {
  positionX0.value = mouseEvent.pageX
  positionY0.value = mouseEvent.pageY
}

onMounted(() => {
  window.addEventListener("mousemove", updateVector2s)
})

onUnmounted(() => {
  window.addEventListener("mousemove", updateVector2s)
})

watch(
  () => Lancer.lancerID,
  lancerID => {
    console.table(lancerID)
  }
) // here we use a getter
</script>

<template>
  <article :class="styles.Card">
    <div>{{ validateLancerID }}</div>
    <span>{{ lancerIsLiving }}</span>
    <h1>{{ Lancer.company }}</h1>
    <h2>{{ Lancer.faction }}</h2>
    <i>{{ Lancer.lastname }}</i>
    <p>{{ Lancer.firstname }}</p>
  </article>
</template>

<style scoped module="styles" lang="scss">
.Card {
  margin: auto;
  padding: auto;
}
</style>
