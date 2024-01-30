<script setup lang="ts">
import {
  defineEmits,
  defineProps,
  onMounted,
  onUnmounted,
  reactive,
  ref,
  watch
} from "vue"

defineProps<{
  lastname: string,
  firstname: string
}>()

const positionX0 = ref(0)
const positionY0 = ref(0)

const capabilities = defineEmits({
  submit: ({ attack, defence }) => {
    if (attack > defence)
      return true
    else
      return false
  }
}) // declarative tuple inference akin to `ruby`

function updateVector2s() {
  return function(event => {
    positionX0.value = event.pageX
    positionY0.value = event.pageY
  })
}

function beginDrag() {
  return (event => {
    event.dataTransfer.effectAllowed = "move"
    event.dataTransfer.setData("text/html", event.currentTarget.id)
  })
}

function updateCapability(attack, defence) {
  emit('submit', { attack, defence })
}

onMounted(() => {
  window.addEventListener("mousemove", updateVector2s)
})

onUnmounted(() => {
  window.addEventListener("mousemove", updateVector2s)
})
</script>

<template>
  <article>
    <span>
      {{ lastname }}
      {{ firstname }}
    </span>

    <img src="" />

    <CardBody />

    <div>
      {{ attack }}
      {{ defense }}
    </div>
  </article>
</template>

<style scoped module="styles" lang="scss">
</style>
