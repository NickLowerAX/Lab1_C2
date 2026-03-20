<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// PROPS
const props = defineProps(['minutos'])
const emit = defineEmits(['finalizado'])

// VARIABLES REACTIVAS
const tiempo = ref(props.minutos * 60)
const activo = ref(false)
const terminado = ref(false)


let intervalo = null

// INICIAR
function start() {
  if (activo.value) return

  activo.value = true

  intervalo = setInterval(() => {
    if (tiempo.value > 0) {
      tiempo.value--
    } else {
      clearInterval(intervalo)
      activo.value = false
      terminado.value = true
      emit('finalizado') // 👈 AQUÍ SE DISPARA EL EVENTO
    }
  }, 1000)
}

// PAUSAR
function pause() {
  clearInterval(intervalo)
  activo.value = false
}

// REINICIAR
function reset() {
  clearInterval(intervalo)
  tiempo.value = props.minutos * 60
  activo.value = false
  terminado.value = false
}

// LIMPIEZA
onUnmounted(() => {
  clearInterval(intervalo)
})

// FORMATO
function formatoTiempo() {
  const min = Math.floor(tiempo.value / 60)
  const sec = tiempo.value % 60
  return `${min}:${sec < 10 ? '0' : ''}${sec}`
}
</script>

<template>
  <div class="timer">
    <h2>{{ formatoTiempo() }}</h2>

    <button @click="start">▶</button>
    <button @click="pause">⏸</button>
    <button @click="reset">🔄</button>

    <p v-if="terminado">¡Tiempo terminado!</p>
  </div>
</template>