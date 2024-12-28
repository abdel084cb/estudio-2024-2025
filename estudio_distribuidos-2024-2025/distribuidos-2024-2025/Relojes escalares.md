* Consideramos que un **sistema distribuido** es un conjunto de **procesos secuenciales P1...Pn** que se **comunican mediante el paso de mensajes asíncrono.**
	* Con intercambio de mensajes los procesos pueden cambiar de estado.
#### Relojes lógicos
* **evento *e***:
	* La **ejecución de una sentencia** de un **proceso**.
	* **Envío** de un **msg**.
	* **Recepción** de un **msg**.
![[Pasted image 20241228190352.png]]
![[Pasted image 20241228190510.png]]
![[Pasted image 20241228191026.png]]
* La relación -> (con ev encima), se denomina **happens-before**.

![[Pasted image 20241228191403.png]]
* La **medición temporal** mas **simple** que existe es mediante una **secuencia creciente de enteros.**
	* Una **fecha** es un **entero**.
	* Cada **proceso Pi** gestiona una **variable local** (de tipo entero), que se denomina **reloj lógico.**
		* Se **inicializa a 0**.
	* Operación:
		* Justo **antes** de producirse un **evento reloj++**.
		* El **valor del reloj** es la **fecha** del **evento.**
		![[Pasted image 20241228191810.png]]

![[Pasted image 20241228191950.png]]
![[Pasted image 20241228192047.png]]
Las **dos barritas** significa que **son concurrentes**, es decir, **no hay una relación de causalidad** entre ellos. Ninguno ocurre antes que el otro.


![[Pasted image 20241228195003.png]]
		Cuando comparamos **fechas lógicas** (por ejemplo, marcas de tiempo de relojes escalares), no siempre podemos determinar si dos eventos en un sistema distribuido están causalmente relacionados. Esto se debe a que las fechas proporcionadas por los relojes escalares reflejan un **orden parcial**. Podemos transformar esta **relación de orden parcial** en una **relación de orden total**, asegurando que todos los eventos sean comparables.
		![[Pasted image 20241228200209.png]]
		Se utiliza el PID para desempatar.

### Relojes Escalares
Los **relojes escalares** son un mecanismo introducido por Leslie Lamport en 1978 para establecer un **orden parcial** entre eventos en sistemas distribuidos. Este sistema no depende del tiempo físico, sino que utiliza un número entero creciente para reflejar la relación causal entre eventos.

**Características principales**
1. **Fecha lógica (timestamp):**
    - Cada evento en un proceso se asocia con un número entero que representa su marca de tiempo lógico.
    - Esta marca se utiliza para determinar el orden causal entre eventos.
2. **Reglas de actualización:**
    - **Antes de cualquier ejecución de sentencia interna:** el proceso incrementa su reloj lógico en 1.
    - **Al enviar un mensaje:** se incrementa el reloj del proceso y se incluye en el mensaje como metadato.
    - **Al recibir un mensaje:** el proceso actualiza su reloj al valor máximo entre su propio reloj y el timestamp recibido, y después lo incrementa en 1.
3. **Preservación del orden causal:**
    - Si un evento e1 ocurre antes que otro evento e2 en el orden causal (happens-before), entonces:
        ```
        date(e_1) < date(e_2)
        ```
4. **Limitaciones:**
    - Los relojes escalares no distinguen eventos concurrentes. Dos eventos no relacionados pueden tener la misma marca de tiempo o una relación arbitraria en el tiempo lógico.

**Propósito**
Los relojes escalares son útiles para:
- Sincronizar procesos en sistemas distribuidos.
- Resolver conflictos en operaciones concurrentes.
- Garantizar consistencia en aplicaciones distribuidas.

**Extensión a un orden total**
Aunque los relojes escalares generan un **orden parcial**, pueden ampliarse a un **orden total** utilizando un criterio adicional, como el identificador del proceso:
- Se compara primero el timestamp.
- Si los timestamps son iguales, se desempata utilizando el identificador del proceso (relación lexicográfica).
Este método permite comparar y ordenar todos los eventos de manera única y consistente.