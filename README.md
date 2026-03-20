integrantes
Noé Isaí Hernández Rivas
Eduardo Antonio Fuentes Melara

¿Qué es Vue.js y cuál es su función en esta aplicación? 
Vue.js es una herramienta que ayuda a crear páginas web dinámicas e interactivas.
En esta aplicación se utilizó para que el temporizador funcione en tiempo real, actualizando los datos en pantalla sin necesidad de recargar la página.

 Describa qué variables reactivas utilizó en su aplicación y cuál es la función de
cada una dentro del sistema.

Las variables reactivas permiten que cuando un dato cambie, también cambie automáticamente en la interfaz.
minutos: guarda el tiempo que escribe el usuario.
error: muestra mensajes si el dato ingresado es incorrecto.
iniciar: controla cuándo aparece el temporizador.
historial: guarda las sesiones terminadas.
tiempo: lleva la cuenta regresiva en segundos.
activo: indica si el temporizador está funcionando.
terminado: muestra cuando el tiempo finaliza.


Diferencia entre v-bind y v-model 

v-model se usa para conectar un input con una variable, por ejemplo lo que escribe el usuario.
v-bind se usa para enviar datos dinámicos a otro componente.
En este proyecto, v-model se usó en el input de minutos y v-bind para pasar ese valor al temporizador.

Mencione al menos un ejemplo de evento utilizado dentro de su aplicación

Un evento que utilicé fue el click, por ejemplo cuando el usuario presiona el botón de iniciar el temporizador. 
Ese evento permite que se ejecute la función que comienza la cuenta regresiva.

Explique para qué utilizó la directiva v-for dentro de su aplicación

La directiva v-for la utilicé para mostrar el historial de sesiones completadas. 
Sirve para recorrer cada elemento guardado en la lista y mostrarlo automáticamente en pantalla.

Describa en qué situación utilizó v-if y qué problema resuelve dentro de su interfaz

Usé v-if para mostrar ciertos elementos solo cuando son necesarios, por ejemplo el mensaje de error 
cuando el usuario ingresa un dato incorrecto o el temporizador cuando ya se inicia. Esto ayuda a que la interfaz se vea más ordenada 
y solo aparezca la información necesaria.

Explique cómo se realiza la validación de datos en su aplicación y por qué es importante validar la información ingresada por el usuario

La validación se hace revisando el valor que el usuario escribe antes de iniciar el temporizador. 
Por ejemplo, no se permite ingresar números menores o iguales a cero ni mayores a 60.
Esto es importante porque evita errores en el funcionamiento de la aplicación y asegura que el temporizador trabaje con datos correctos.
