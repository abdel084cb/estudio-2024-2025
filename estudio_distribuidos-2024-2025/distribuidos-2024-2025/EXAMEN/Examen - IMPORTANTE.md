### Relojes escalares o lógicos

![[IMG_3597.jpg]]

* No permiten distinguir eventos concurrentes
	* Eso en el modelo total
	* ¿Pero y en el modelo parcial?
* Los **relojes lógicos** y **relojes escalares** permiten establecer un **orden total** al añadir el par `(date, pid)` 
1. **Orden Total**: La relación lexicográfica entre los pares `(date, pid)` asegura que todos los eventos puedan ser comparados, incluso si originalmente estaban concurrentes en el modelo parcial.
2. **Distinguir Concurrencia**: Sin embargo, estos relojes no pueden determinar si dos eventos son concurrentes o no. Dos eventos con diferentes date pueden estar relacionados (uno ocurre antes que el otro) o pueden ser concurrentes (sin relación de causalidad). Este orden total **impone una secuencia arbitraria** entre eventos concurrentes, pero no puede identificar la concurrencia en sí.

Si es necesario distinguir eventos concurrentes, los **relojes vectoriales** son la solución adecuada, ya que almacenan más información sobre la causalidad y permiten identificar cuándo dos eventos no están relacionados causalmente.

![[Pasted image 20250110222746.png]]
![[Pasted image 20250110222936.png]]

### Relojes vectoriales

![[IMG_3598.jpg]]

![[Pasted image 20250110223809.png]]
![[Pasted image 20250110224540.png]]
![[Pasted image 20250110224808.png]]

### Ricart-Agrawala

![[Pasted image 20250111002606.png]]
 **1. Estructura de datos compartida (SHARED DATABASE)**
- Define las variables necesarias para manejar la exclusión mutua.
    - **Constantes:**
        - `me`: Identificador único del nodo.
        - `N`: Número total de nodos en el sistema.
    - **Variables de control:**
        - `Our_Sequence_Number`: Número de secuencia asignado a las solicitudes de este nodo.
        - `Highest_Sequence_Number`: El número de secuencia más alto observado en la red.
        - `Outstanding_Reply_Count`: Número de respuestas (REPLY) esperadas de otros nodos.
        - `Requesting_Critical_Section`: Indica si este nodo está solicitando acceso a la sección crítica.
        - `Reply_Deferred`: Array que guarda si hemos diferido una respuesta a algún nodo.
    - **Semáforo binario:**
        - `Shared_vars`: Proporciona acceso seguro a las variables compartidas.
![[Pasted image 20250111002843.png]]
 **2. Proceso que solicita exclusión mutua (Pre-protocolo y Post-protocolo)**
Este es el algoritmo que se ejecuta cuando un nodo quiere acceder a la sección crítica:
**Pre-protocolo (solicitar acceso):**
1. Incrementa el `Our_Sequence_Number` basado en el `Highest_Sequence_Number`.
2. Marca `Requesting_Critical_Section` como `TRUE`.
3. Envía un mensaje de solicitud (`REQUEST`) a todos los nodos con el número de secuencia actual y el identificador del nodo.
4. Espera a que todos los nodos respondan (`Outstanding_Reply_Count = 0`).
**Post-protocolo (liberar acceso):**
1. Marca `Requesting_Critical_Section` como `FALSE`.
2. Para cada nodo, verifica si se ha diferido una respuesta (`Reply_Deferred`).
3. Si hay respuestas diferidas, las envía ahora.
![[Pasted image 20250111003013.png]]
 **3. Procesos para manejar solicitudes y respuestas**
Estos son los procesos que gestionan los mensajes recibidos:
 **Al recibir un `REQUEST`:**
1. Actualiza el `Highest_Sequence_Number` al valor máximo entre el número de secuencia recibido y el actual.
2. Evalúa si debe diferir la respuesta usando la prioridad:
    - Tiene prioridad si no está solicitando la sección crítica.
    - Tiene prioridad si su número de secuencia es menor.
    - Si los números de secuencia son iguales, decide por el identificador del nodo.
3. Si el nodo remoto tiene mayor prioridad, se difiere la respuesta.
**Al recibir un `REPLY`:**
1. Reduce el contador de respuestas pendientes (`Outstanding_Reply_Count`).

![[Pasted image 20250111004818.png]]
- **`ldrᵢ`** ≈ **`Our_Sequence_Number`**.
- **`clockᵢ`** ≈ **`Highest_Sequence_Number`**

`when sending a REQUEST (acquire_mutex) do`
	`lrdi <- clocki + 1`
	`send(REQUEST(lrdi,i))
`when receiving REQUEST(lrdi,i)`
	`clockj <- max(clockj,lrdi)`

Esto sin tener en cuenta el aumento de reloj en eventos internos. Es decir solo utilizamos el reloj para los mutex.
