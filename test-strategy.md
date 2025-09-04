## Objetivo
Comprobar que el juego funcione de acuerdo a lo solicitado: que el usuario pueda adivinar un número entre 1 y 100 en máximo 10 intentos, y que se le den pistas correctas (“más alto” o “más bajo”) hasta ganar o perder.

## Alcance
- Se probarán las funciones principales: ingreso de número, validación de rango, botón de enviar, mensajes de acierto/error, contador de intentos y reinicio del juego.
- No se incluye la parte de estilos, ya que no fue solicitada por el cliente.

## Errores encontrados y correcciones
- 1. **El botón no hacía nada**
   - *Causa*: El botón era `type="submit"` y no tenía asociado ningún evento JS.  
   - *Solución*: Cambié el botón a `type="button"` y añadí un listener en JS con `addEventListener('click', ...)`.

- 2. **No había validación de entrada**
   - *Causa*: Si el usuario ingresaba letras o números fuera de 1–100, el juego se rompía.  
   - *Solución*: Se agregó verificación con `Number.isInteger(valor)` y rangos válidos.

- 3. **El juego no reiniciaba correctamente**
   - *Causa*: Una vez adivinado el número, el estado no se reseteaba.  
   - *Solución*: Implementé función `reiniciar()` que limpia variables, genera nuevo número y habilita de nuevo el input.

- 4. **Errores en consola: elementos `null`**
   - *Causa*: Los `querySelector` buscaban IDs/clases que no coincidían con el HTML.  
   - *Solución*: Alinear nombres: `#guessField`, `.guessSubmit`, `.guesses`, `.lastResult`, `.lowOrHi`.

- 5. **La logica de los mensajes esta mala**
   -  if(userGuess === randomNumber) {
      lastResult.textContent = '!!!Pérdistes!!!';
      lastResult.style.backgroundColor = 'black';
      lowOrHi.textContent = '';
      setGameOver();
    } else if(guessCount === ATTEMPS) {
      lastResult.textContent = 'Felicitaciones! adivinaste el número!';
      lastResult.style.backgroundColor = 'red';
      setGameOver();
    } else {
      lastResult.textContent = 'Incorrecto! ';
      lastResult.style.backgroundColor = 'green';
      if(userGuess < randomNumber) {
        lowOrHi.textContent = 'El número es mayor!';
      } else if(userGuess > randomNumber) {
        lowOrHi.textContent = 'El número es menor!';

- 6. **Generador de nuemro aleatorio esta malo**
    - let randomNumber = Math.random() * 10; y debería de ser de 100 
    - let randomNumber = Math.floor(Math.random() * 100) + 1; // 1..100 (solucion)
- 7. **UserGusses es string**
    - esto genera que hayan letras o numeros vacios y pueda que se genere un bug al ingresar una letra
    - esto deberia de parsearse con un <Number.IsInteger>
- 8. **El reset deja fondo en blanco y el texto en blanco**
    - esto al resetearlo deja el texto blanco sobre fondo blanco 


## Casos de prueba clave
- Ingresar un valor vacío → debe mostrar error.
- Ingresar número fuera de rango (ej. 0 o 101) → debe mostrar error.
- Ingresar número menor que el secreto → mensaje “más alto”.
- Ingresar número mayor → mensaje “más bajo”.
- Adivinar el número → mensaje de éxito y reinicio.
- Llegar a 10 intentos fallidos → mensaje de fin de juego y reinicio.

## Soluciones
- Que se cambie el <input type="submit"> por <button type="button"> y añadí el addEventListener('click', checkGuess) correctamente escrito (antes estaba con mayúsculas mal).
- evitar el uso de <Number(guessField.value)> el guessFiled.value puede que se usen letras o vacios y esto hace que se rompa el juego, mejor usar el <Number.isInteger> para validar solo numeros enteros y que se maneje del rango del 1 al 100.
- crear una funcion RESETGAME() para limpiar mensajes y reiniciar variables. tambien Math.floor(Math.random()*100)+1 para que genere numeros aleatorios
- Corregir <document.querySelector('lowOrHi')> a <document.querySelector('.lowOrHi')> y revisé que todos los querySelector coincidan con los id y class del HTML.
- evitar los eventos mal escritos como <addeventListener> por <addEventListener>.
- Ajusté la lógica: ahora al ganar muestra “¡Felicitaciones!” en verde, "haz perdido" en rojo y al quedarse sin intentos muestra “Fin del juego” en negro.
- <lastResult.style.backgroundColor = '';> esto hara que limpie el fondo en lugar de ponerlo blanco. 

