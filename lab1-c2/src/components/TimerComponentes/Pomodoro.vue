<script setup>
import { ref } from 'vue'

// VARIABLES REACTIVAS
const trabajo = ref(25 * 60)
const descanso = ref(5 * 60) 
const trabajoInput = ref('25') 
const ciclos = ref(0) 

const tiempoRestante = ref(trabajo.value)
const enTrabajo = ref(true)

const activo = ref(false)

const error = ref('')

let intervalo = null

// FORMATO
function formatoTiempo(segundos) {
  const min = Math.floor(segundos / 60)
  const sec = segundos % 60
  return `${min}:${sec < 10 ? '0' : ''}${sec}`
}

// INICIAR
function iniciar() {
  if (activo.value) return

  // VALIDAR ANTES DE INICIAR
  if (!validarTrabajo()) return

  activo.value = true

  intervalo = setInterval(() => {
    if (tiempoRestante.value > 0) {
      tiempoRestante.value--
    } else {
      cambiarModo()
    }
  }, 1000)
}

// PAUSAR
function pausar() {
  clearInterval(intervalo)
  activo.value = false
}

// REINICIAR
function reiniciar() {
  clearInterval(intervalo)
  activo.value = false
  enTrabajo.value = true
  tiempoRestante.value = trabajo.value
}

// CAMBIAR ENTRE TRABAJO Y DESCANSO
function cambiarModo() {
  clearInterval(intervalo)
  activo.value = false

  if (enTrabajo.value) {
    ciclos.value++

    // 🔁 Cada 3 ciclos → descanso largo
    if (ciclos.value % 3 === 0) {
      descanso.value = 15 * 60
      notificar('¡Descanso largo (15 min)!')
    } else {
      descanso.value = 5 * 60
      notificar('¡Descanso corto (5 min)!')
    }

    tiempoRestante.value = descanso.value
  } else {
    notificar('¡Hora de trabajar!')
    tiempoRestante.value = trabajo.value
  }

  enTrabajo.value = !enTrabajo.value
}

// VALIDACIÓN Y GUARDAR TIEMPOS
function guardarTiempos() {
  if (!trabajoInput.value || !descansoInput.value) {
    error.value = 'Campos obligatorios'
    return
  }

  const t = parseInt(trabajoInput.value)
  const d = parseInt(descansoInput.value)

  if (isNaN(t) || isNaN(d) || t <= 0 || d <= 0) {
    error.value = 'Ingrese números válidos mayores a 0'
    return
  }

  trabajo.value = t * 60
  descanso.value = d * 60

  reiniciar()
  error.value = ''
}

function notificar(mensaje) {
  // Notificación del navegador
  if (Notification.permission === 'granted') {
    new Notification(mensaje)
  }

  // Sonido simple
  const audio = new Audio('https://www.soundjay.com/buttons/beep-01a.mp3')
  audio.play()
}

if (Notification.permission !== 'granted') {
  Notification.requestPermission()
}

function validarTrabajo() {
  const t = parseInt(trabajoInput.value)

  if (!trabajoInput.value) {
    error.value = 'Campo obligatorio'
    return false
  }

  if (isNaN(t) || t <= 0) {
    error.value = 'Debe ser un número válido'
    return false
  }

  if (t > 25) {
    error.value = 'Máximo 25 minutos'
    return false
  }

  trabajo.value = t * 60
  error.value = ''
  return true
}
</script>

<template>
  <div class="pomodoro">

    <h2>Estado: {{ enTrabajo ? 'Trabajo' : 'Descanso' }}</h2>

    <input 
     type="number"
     v-model="trabajoInput"
     placeholder="Minutos de trabajo (máx 25)"
    >

    <h1>{{ formatoTiempo(tiempoRestante) }}</h1>

    <button @click="iniciar">Iniciar</button>
    <button @click="pausar">Pausar</button>
    <button @click="reiniciar">Reiniciar</button>

    <p v-if="error" style="color:red;">{{ error }}</p>
  </div>
</template>

<style>
.pomodoro {
  background-color: white;
  padding: 30px;
  border-radius: 20px;
  width: 320px;
  text-align: center;

  /* sombra suave */
  box-shadow: 0 8px 20px rgba(0,0,0,0.1);
}

/* ESTADO */
h2 {
  color: #43334C;
  margin-bottom: 10px;
}

/* TIEMPO */
h1 {
  font-size: 50px;
  margin: 20px 0;
  color: #E83C91; /* acento fuerte */
}

/* INPUT */
input {
  width: 80%;
  padding: 10px;
  border-radius: 10px;
  border: 1px solid #ccc;
  margin-bottom: 15px;
  text-align: center;
  font-size: 16px;
}

/* BOTONES */
button {
  margin: 5px;
  padding: 10px 15px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  background-color: #FF8FB7; /* acento suave */
  color: white;
  font-weight: bold;
  transition: 0.3s;
}

button:hover {
  background-color: #E83C91; /* acento fuerte */
}

/* ERROR */
p {
  color: #E83C91;
  font-weight: bold;
  margin-top: 10px;
}
</style>
