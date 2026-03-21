<h1> integrantes </h1>
Noé Isaí Hernández Rivas
Eduardo Antonio Fuentes Melara

Codigo Fuente completo en la Branch "main"

¿Qué es Vue.js y cuál es su función en esta aplicación? 

Vue.js es un framework de JavaScript que permite crear interfaces web interactivas y dinámicas. Su función en esta aplicación es actualizar automáticamente la interfaz cuando cambian los datos, como el tiempo del temporizador o el estado del Pomodoro.

Describa qué variables reactivas utilizó en su aplicación y cuál es la función de
cada una dentro del sistema.

trabajoInput: almacena el tiempo ingresado por el usuario
trabajo: tiempo de trabajo en segundos
descanso: tiempo de descanso en segundos
tiempoRestante: controla el tiempo actual
enTrabajo: indica si está en modo trabajo o descanso
activo: indica si el temporizador está en ejecución
ciclos: cuenta los ciclos completados
error: muestra mensajes de validación


Diferencia entre v-bind y v-model 

v-bind: se usa para enviar datos desde JavaScript al HTML
v-model: permite enlazar datos en ambas direcciones (usuario ↔ sistema)

Mencione al menos un ejemplo de evento utilizado dentro de su aplicación

Ejemplo de codig: <button @click="iniciar">

Evento "click", Este evento ejecuta la función cuando el usuario hace clic como para 
iniciar eltiempo establecido del pomodoro

Explique para qué utilizó la directiva v-for dentro de su aplicación



Describa en qué situación utilizó v-if y qué problema resuelve dentro de su interfaz

La directiva v-if se utilizó para mostrar u ocultar elementos dependiendo del estado de la aplicación. 
Por ejemplo, se utiliza para mostrar mensajes de error cuando el usuario ingresa datos incorrectos en el campo de entrada. 
Esto resuelve el problema de mostrar información innecesaria en la interfaz, ya que el mensaje solo aparece cuando realmente existe un error.

Explique cómo se realiza la validación de datos en su aplicación y por qué es importante validar la información ingresada por el usuario

La validación de datos se realiza mediante funciones en JavaScript que verifican la información ingresada por el usuario antes de iniciar el temporizador.

en la funcionamiento se valida que:
El campo no esté vacío
El valor sea numérico
El número sea mayor que 0
No supere el límite permitido (25 minutos)

La validación es importante porque evita errores en la ejecución del programa y asegura que el sistema funcione correctamente.
Aparte de mejorar la experiencia que tiene el usuario interactuando libremente.
