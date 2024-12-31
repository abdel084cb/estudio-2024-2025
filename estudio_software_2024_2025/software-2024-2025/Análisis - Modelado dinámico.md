El **modelado dinámico** es una técnica utilizada para representar el comportamiento y las interacciones del sistema a lo largo del tiempo. A diferencia del modelado estático, que describe la estructura del sistema (clases, atributos y relaciones), el modelado dinámico se enfoca en cómo los objetos interactúan y cambian de estado en respuesta a eventos o acciones.

#### Diagramas de secuencia
* Muestra la secuencia cronológica de mensajes entre objetos durante un escenario concreto
* Cada objeto viene dado por una barra vertical
* El tiempo transcurre de arriba abajo
* Cuando existe demora entre el envío y la atención se puede indicar usando una línea oblicua
![[Pasted image 20241222215728.png]]
![[Pasted image 20241222215945.png]]
###### Representación de mensajes:
* Hay que tener varias cosas en cuenta :
	* Mensaje síncrono:
		* Se puede especificar un return en la línea discontinua con una etiqueta si es relevante, luego se puede usar en guardas... 
		* Llamada a una operación . Se suspende la ejecución en espera de respuesta
			![[Pasted image 20241222220618.png]]
	* Mensaje asíncrono:
		* Se envía el mensaje y se continúa sin esperar respuesta.
			![[Pasted image 20241222220652.png]]
	* Respuesta a una llamada síncrona a una operación.
		* No es obligatorio indicar el retorno del control en mensajes síncronos
		![[Pasted image 20241222220903.png]]
	* Creación y destrucción:
		* Mensaje de creación: va dirigido al rectángulo del objeto y se etiqueta con create
		* Mensaje de destrucción : va dirigido a la línea del objeto que se quiere destruir. El final de la flecha es una cruz y se etiqueta con destroy
			![[Pasted image 20241222221328.png]]
	* Solapamiento: El solapamiento en un diagrama de secuencia, como el representado en la imagen, describe una interacción en la que un objeto realiza una operación sobre otro mientras mantiene su propio flujo activo. Es decir, el flujo de ejecución se "superpone" en el tiempo. Es similar a la concurrencia, pero dentro del contexto del modelado de interacciones. En este caso, refleja que dos o más objetos pueden estar "activos" al mismo tiempo, llevando a cabo tareas que pueden solaparse temporalmente.
			![[Pasted image 20241222222010.png]]
	* Lost: . Se desconoce quien recibe el mensaje. Se interpreta como que el mensaje nunca alcanza su destinatario
			![[Pasted image 20241222221720.png]]
	* Found: . Se desconoce quien envía el mensaje. Se interpreta como que el emisor está fuera del ámbito que se describe
			![[Pasted image 20241222221735.png]]
	* Completo: El mensaje normal
* Un objeto puede enviarse a sí mismo un mensaje. Puede representar también la entrada por parte del objeto en cierta actividad de más bajo nivel
		![[Pasted image 20241222224959.png]]
###### Especificación de ejecución
Se puede hacer tanto con el rectángulo de la izquierda como con el de la derecha. Mejor usar el de la izquierda.
![[Pasted image 20241222224753.png]]

###### Interaction use o ref
Sirven para especificar una **referencia directa** a un diagrama de interacción diferente. Es como una "llamada" a otro diagrama de interacción que contiene más detalles del flujo en cuestión.
![[Pasted image 20241222225514.png]]
![[Pasted image 20241222225638.png]]

###### Fragmentos combinados

- **Alternativa (`alt`)**
    - Representa una selección condicional entre diferentes flujos de interacción.
    - Se utiliza cuando hay varias posibilidades y solo una puede ejecutarse.
- **Opción (`opt`)**
    - Representa un flujo opcional que puede o no ejecutarse dependiendo de una condición.
- **Bucle (`loop`)**
    - Representa una interacción que se repite mientras se cumpla una condición.
- **Interrupción (`break`)**
    - Representa un flujo de interacción que rompe el flujo normal bajo ciertas condiciones.
- **Continuación (`par`)**
    - Representa flujos que pueden ejecutarse en paralelo.
    - Se utiliza para modelar concurrencia.
- **Secuencia débil (`seq`)**
    - Representa un orden de ejecución en el que algunos mensajes pueden ser opcionales.
    - Más relajada que una secuencia estricta.
- **Secuencia estricta (`strict`)**
    - Representa un orden estricto de ejecución en el que los mensajes deben ejecutarse exactamente en el orden indicado.
- **Región crítica (`critical`)**
    - Representa un bloque de interacción que no puede ser interrumpido por otras interacciones.
    - Se utiliza para modelar exclusión mutua.
- **Aserción (`assert`)**
    - Representa una condición que debe cumplirse en el flujo de interacción.
    - Se utiliza para modelar reglas o restricciones específicas.

Se puede ver el uso de guardas para gestionar un alt:
![[Pasted image 20241222230843.png]]

Ejemplo opt:
![[Pasted image 20241222230944.png]]

Se puede continuar la finalización de un alt de la siguiente manera
![[Pasted image 20241222231720.png]]
Se puede ver que si tiene insuficiente balance toma una traza de ejecución distinta terminando el programa después de ejecutar esa traza:
![[Pasted image 20241222231945.png]]

Ejemplo de par y critical:
![[Pasted image 20241222235229.png]]

Invariantes: ignore, consider y assert:
![[Pasted image 20241223180128.png]]

Tiempo:
![[Pasted image 20241223180535.png]]
###### Tipos de control:
* Centralizado (Tenedor)
* Descentralizado (Escalera)

#### Diagrama de estados

- **Propósito**:
    - Modelar el comportamiento interno de los objetos.
    - Representar el patrón de comportamiento compartido por todos los objetos de una clase.
- **Características**:
    - Útil para clases con **comportamiento dinámico relevante**.
    - Objetos sin comportamiento relevante se consideran con un único estado.
    - Basados en el formalismo de **statecharts de Harel**.
    - Son **autómatas de estados finitos** adaptados al modelado orientado a objetos.
- **Aplicación**:
    - Modelar objetos que **responden a eventos discretos** (comportamiento reactivo).
    - Cada clase tiene un único diagrama de estados que define el comportamiento común a sus objetos.

![[Pasted image 20241223181958.png]]

![[Pasted image 20241223182103.png]]

![[Pasted image 20241223182301.png]]


Objeto con vida finita: Nace y muere.
![[Pasted image 20241223182356.png]]

Ejemplo de juego de ajedrez simplificado:
![[Pasted image 20241223182439.png]]

Condiciones/Guardas, se establecen sobre sus atributos:
![[Pasted image 20241223182859.png]]

Ejemplo (control de semáforos en una intersección de 2 vías)
![[Pasted image 20241223183224.png]]
![[Pasted image 20241223184427.png]]
###### Operaciones en Diagramas de Estados

1. **Introducción:**
    - Los diagramas de estados muestran secuencias de eventos y especifican las **operaciones** que realiza un objeto como respuesta a estos eventos.
    - Las operaciones ejecutan **computaciones**.
2. **Tipos de Operaciones:**
    - **Acciones:** Instantáneas o inmediatas (su duración es insignificante respecto a la vida del objeto).
    - **Actividades:** Operaciones más complejas con una duración mayor (no detallado en este fragmento).
###### Acciones

- **Definición:**
    - Son operaciones instantáneas asociadas a computaciones o envío de eventos.
    - Se consideran inmediatas en el contexto del diagrama, aunque requieren algo de tiempo en la realidad.
- **Asociaciones:**
    - **Transiciones:**
        - Formato: `evento [guarda] / acción`
            - **Evento:** Invocación a una operación de la clase (mensaje de entrada en un diagrama de secuencia).
            - **Guarda:** Expresión booleana basada en parámetros del evento y el contexto del objeto.
            - **Acción:** Invocación a una operación propia o de otra clase:
                - Formatos:
                    - `<NombreClase>.operación`
                    - `<referenciaObjeto>.operación`
        - Se pueden incluir varios eventos separados por comas.
    - **Estados:**
        - **Acción de entrada:** `entry / acción`
        - **Acción de salida:** `exit / acción`
![[Pasted image 20241223194006.png]]
![[Pasted image 20241223194644.png]]

###### Actividades
* Son operaciones cuya realización requiere un cierto tiempo
* Están asociadas a los estados
* Ejemplos: mostrar una imagen, llevar a cabo un cálculo
* La actividad comienza en cuanto el objeto entra en el estado `do/actividad`
* La actividad o bien termina por sí misma o bien es abortada por un evento antes de su finalización
* Duran hasta que salen del estado.

![[Pasted image 20241223195335.png]]
Una transición sin nombre de evento es una transición automática. Se dispara cuando las acciones y la actividad asociada al estado se completan
![[Pasted image 20241223195423.png]]

![[Pasted image 20241223195747.png]]
Auto-transición: Entra y sale - Transición interna: Ni entra ni sale, solo ejecuta:
![[Pasted image 20241223200807.png]]

Un **evento diferido** es un evento que no se procesa inmediatamente en el estado actual, sino que se guarda en una cola especial hasta que el objeto alcance un estado donde pueda ser manejado.

Esto significa que el evento es "retenido" en lugar de ser ignorado, y será procesado cuando se llegue a un estado que tenga una transición asociada para ese evento:
![[Pasted image 20241223201016.png]]

###### Estructuración de diagramas

- **Estado inicial (círculo negro):**
    - El sistema comienza en el **estado inicial** y transita hacia el estado **Punto muerto**.
- **Punto muerto:**
    - Es un estado donde no hay marcha activa.
    - Desde este estado:
        - **Transición hacia "Marcha atrás":** Ocurre con el evento **atrás**.
        - **Transición hacia "Marcha adelante":** Ocurre con el evento **adelante**.
- **Marcha atrás:**
    - El estado en el que el vehículo está en reversa.
    - Desde este estado:
        - Se puede regresar a **Punto muerto** con el evento **p_muerto**.
- **Marcha adelante:**
    - Es un **estado compuesto** que contiene subestados: **Primera**, **Segunda**, y **Tercera**.
    - Desde **Punto muerto**, se accede a este estado con el evento **adelante**.
    - Si se abandona el estado **Marcha adelante** y luego se vuelve a entrar, el sistema **comenzará siempre desde el subestado "Primera"**.
![[Pasted image 20241223202019.png]]

![[Pasted image 20241223202656.png]]

![[Pasted image 20241223202811.png]]
La transición automática se ejecutará tras terminarse todos los subestados:
![[Pasted image 20241223202944.png]]
![[Pasted image 20241223204239.png]]

Ejemplos: Estado de la batería de un coche
La **transición heredada** indica que, al activarse el evento `reset`, el sistema volverá al estado `Vacía` dentro del estado compuesto `En funcionamiento`.
![[Pasted image 20241223204353.png]]
![[Pasted image 20241223204428.png]]
###### Concurrencia

Concurrencia en el Sistema:
- El **modelo dinámico** describe un conjunto de objetos concurrentes.
- Cada objeto tiene su propio **diagrama de estados** y estado individual.
- Los objetos son **concurrentes** y cambian de estado de forma independiente.
- El estado del sistema es la **agregación** de los estados de todos los objetos que lo componen.
    - Ejemplo: En un coche, el estado del sistema incluye el estado de la transmisión, encendido, acelerador, frenos, etc.

Concurrencia dentro de un Objeto:
- Surge cuando el objeto puede descomponerse en subconjuntos de **atributos** o **enlaces**.
- Cada subconjunto define su propia **región** dentro del diagrama de estados.
**Concurrencia**: Ambas regiones se ejecutan de manera paralela e independiente, pero pueden estar sincronizadas por eventos compartidos, como `tapar` y `llenar`:
![[Pasted image 20241223205734.png]]
#### Diagramas de actividad
- **Definición**: Representan el flujo de control destacando las actividades que tienen lugar a lo largo del tiempo en sistemas intensivos en software.
- **Relación con Diagramas de Estados**: Son similares a los diagramas de estados, pero sin eventos; los estados contienen actividades.

**Comparación: Diagramas de Actividades vs Diagramas de Interacción**
- **Enfoque**:
    - **D. Interacción**: Se centran en los objetos.
    - **D. Actividades**: Se centran en las actividades que tienen lugar entre los objetos.
- **Contenido**:
    - **D. Interacción**: Muestran objetos que se pasan mensajes.
    - **D. Actividades**: Muestran operaciones que se pasan objetos.
![[Pasted image 20241223214627.png]]


###### Estados de Acción
- **Características**:
    - Su ejecución tiene un tiempo insignificante en el contexto del sistema.
    - Representan computaciones atómicas.
- **Ejemplos de Acciones**:
    - Crear o borrar un objeto.
    - Invocar una operación sobre un objeto.
    - Evaluar una expresión.
    - Cambiar el valor de un atributo.
- **Propiedades**:
    - No son descomponibles.
    - UML no impone un lenguaje específico para expresiones
![[Pasted image 20241223215001.png]]

###### Estados de Actividad
- **Características**:
    - Su ejecución tiene una duración definida.
    - Agrupan acciones o actividades.
- **Diferencias con Estados de Acción**:
    - **Descomponibles**: Pueden ser especificados por otro Diagrama de Actividades.
    - Los estados de acción son atómicos, los de actividad no.
- **Herramientas CASE**:
    - Mantienen el estado de actividad asociado con el diagrama que lo especifica.
![[Pasted image 20241223215051.png]]
###### Flujos de control
* Cuando se completa una acción el flujo de control pasa inmediatamente a la siguiente acción
* El flujo se representa con una flecha sin etiqueta de evento
![[Pasted image 20241223215153.png]]

###### Nodos de Bifurcación y Mezcla
- **Nodos de Bifurcación**:
    ![[Pasted image 20241223215250.png]]
    - Representan **caminos alternativos**.
    - **Características**:
        - Una transición de entrada.
        - Dos o más transiciones de salida con **guardas excluyentes** (UML no especifica lenguaje, se puede usar `else`).
- **Nodos de Mezcla**:
    ![[Pasted image 20241223215308.png]]
    - Permiten **mezclar caminos múltiples**.
    - **Características**:
        - Dos o más transiciones de entrada.
        - Una transición de salida.

![[Pasted image 20241223215445.png]]



###### Nodos de División y Unión
- **Nodos de División**:
    - Modelan **flujos concurrentes**.
    - **Características**:
        - Una transición de entrada.
        - Dos o más transiciones de salida que continúan en paralelo.
- **Nodos de Unión**:
    - Sincronizan los flujos concurrentes.
    - **Características**:
        - Dos o más transiciones de entrada.
        - Una transición de salida.
        - Espera a que todos los flujos de entrada lleguen antes de continuar.
![[Pasted image 20241223215739.png]]

Ejemplo de flujo de trabajo para reproducir una conversación en un dispositivo que imita la voz y los gestos humanos:

![[Pasted image 20241223215629.png]]
![[Pasted image 20241223222834.png]]
###### Calles en Diagramas de Actividad
- **Definición**: Dividen los nodos en grupos.
- **Características**:
    - Cada grupo o calle representa una parte de la organización responsable de las actividades.
    - Las calles tienen nombres únicos.
    - Una calle puede ser implementada por varias clases. Cada clase puede ser una calle
    - Los flujos pueden cruzar entre calles.

![[Pasted image 20241227223003.png]]

![[Pasted image 20241223223048.png]]
###### Flujo de Objetos
- **Definición**: Los objetos pueden participar en el flujo de control.
- **Características**:
    - Algunas actividades **crean** objetos.
    - Otras **usan** o **modifican** esos objetos.
    - Se puede representar el **estado** del objeto en cada punto del flujo.

![[Pasted image 20241223223403.png]]


###### Operaciones sobre Conjuntos de Elementos
- **Uso**:
    - Simplifican el modelo al evitar iteraciones explícitas.
    - Se aplican cuando una misma operación se ejecuta sobre un conjunto de elementos.
- **Formato**:
    - Entradas y salidas son **colecciones de valores**, representadas como **arrays**.
    - Los elementos del array se procesan en la región, **posiblemente en concurrencia**.

![[Pasted image 20241223223540.png]]

###### Usos de los Diagramas de Actividad
- **Propósito general**:
    - Modelar la dinámica de sistemas, subsistemas, clases, casos de uso, etc.
- **Usos principales**:
    1. **Modelar flujos de trabajo**:
        - Representan procesos en sistemas intensivos en software.
        - Hacen énfasis en actividades desde la perspectiva de los actores.
        - Modelan procesos de negocio donde colaboran humanos y sistemas automáticos.
    2. **Modelar operaciones**:
        - Actúan como diagramas de flujo para modelar detalles de cálculos y computaciones.
###### Modelado de Flujos de Trabajo
1. **Centrarse en un aspecto relevante**: No mostrar todos los flujos en un único diagrama.
2. **Definir límites del flujo**: Establecer precondiciones y poscondiciones.
3. **Desde el estado inicial**: Especificar las acciones a lo largo del tiempo.
4. **Estructurar actividades**: Organizar el flujo de forma lógica.
5. **Considerar bifurcaciones y concurrencia**: Incluir decisiones y flujos paralelos.
6. **Especificar flujo de objetos**: Mostrar cómo los objetos interactúan en el flujo.



### Actividades y acciones

 **Ejemplos de Acciones:**

Las acciones son operaciones que se ejecutan de manera **instantánea** o que son **atómicas**, lo que significa que ocurren de manera muy rápida o se perciben como un único paso desde el punto de vista del diagrama de estados.
1. **Llamar a un método o función**:
    - Ejemplo: En el diagrama de estados, cuando se llama a un método para realizar una tarea, como `calcularSuma()`, esa es una acción, ya que se realiza de forma rápida y el sistema espera a que termine de ejecutarse antes de avanzar al siguiente estado.
2. **Asignar un valor a una variable**:
    - Ejemplo: Asignar un valor a una variable en el sistema, como `x = 5`, es una acción porque es un paso atómico que ocurre inmediatamente.
3. **Enviar un mensaje (sin esperar respuesta)**:
    - Ejemplo: Un sistema de mensajería que envía un mensaje, como enviar una notificación de "nuevo mensaje" a otro sistema, es una acción porque no requiere esperar a que el mensaje se reciba o procese para avanzar al siguiente estado.
4. **Cambiar el valor de un atributo**:
    - Ejemplo: Si el sistema cambia el estado de un objeto, como `estado = "Activo"`, este cambio de estado es una acción rápida y se considera atómica.
5. **Iniciar un proceso de validación**:
    - Ejemplo: Al pulsar un botón de "validar" en una interfaz de usuario, se inicia el proceso de validación, lo cual es una acción. Aunque el proceso de validación puede tomar tiempo, la transición hacia el estado "validando" ocurre inmediatamente.
 **Ejemplos de Actividades:**

Las actividades son operaciones **prolongadas**, que se ejecutan durante un tiempo mientras el sistema está en un estado específico. Estas actividades suelen ser **continuas** o **recurrentes** y pueden involucrar varias acciones o pasos.
1. **Cálculo prolongado (por ejemplo, procesar datos de grandes volúmenes)**:
    - Ejemplo: Si el sistema está procesando un conjunto de datos o realizando cálculos complejos durante varios segundos o minutos, como calcular estadísticas de un gran conjunto de datos, esto es una actividad. El sistema sigue en el estado "Procesando datos" hasta que la operación termine.
2. **Esperar la respuesta de un servidor (operación asincrónica)**:
    - Ejemplo: Si un sistema envía una solicitud HTTP y espera una respuesta del servidor, este proceso de "esperar respuesta" sería una actividad. La solicitud es una acción, pero el esperar la respuesta puede ser una actividad porque el sistema se mantiene en el estado "Esperando respuesta" hasta recibir los datos.
3. **Despliegue de una interfaz gráfica o animación**:
    - Ejemplo: Si el sistema está realizando un proceso largo de carga de una interfaz gráfica o animación, como una animación de bienvenida o una carga de recursos visuales, esa carga es una actividad porque toma tiempo y puede involucrar varias acciones internas.
4. **Operación continua sobre un archivo o base de datos**:
    - Ejemplo: Si el sistema está monitorizando y actualizando un archivo de registro o una base de datos en tiempo real (como registrar eventos o realizar consultas repetidas), esto es una actividad. Aunque las operaciones individuales (como escribir en el archivo o hacer una consulta) son acciones, el proceso continuo de mantener actualizado el archivo o la base de datos durante un período de tiempo es una actividad.
5. **Transferencia de archivos de gran tamaño**:
    - Ejemplo: Si el sistema está en el estado "Transfiriendo archivos", donde el archivo está siendo enviado a través de una red, esta es una actividad. La transferencia es un proceso largo y continuo que ocurre mientras el sistema está en ese estado, aunque puede implicar varias acciones, como la apertura de una conexión, la transferencia de bloques de datos, etc.
6. **Escaneo de un dispositivo**:
    - Ejemplo: Un sistema que escanea un dispositivo (como un escáner de documentos o un antivirus que escanea archivos en busca de virus) realiza una actividad, ya que es un proceso que puede durar un tiempo determinado y ocurre mientras el sistema está en ese estado específico.
 Resumen de la Diferencia:

- **Acciones**: Son pasos atómicos, rápidos e instantáneos que pueden ocurrir durante la transición entre estados. Implican operaciones simples y directas, como ejecutar una función, cambiar el valor de una variable o enviar un mensaje.
    
- **Actividades**: Son procesos más largos, continuos o repetitivos que ocurren mientras el sistema permanece en un estado determinado. Estas operaciones suelen tomar tiempo y pueden implicar varias acciones subyacentes, como procesar datos, esperar respuestas, o realizar un trabajo prolongado.
    
En términos prácticos, en un diagrama de estados:
- **Acciones** se representan generalmente dentro de un estado o en una transición, indicando que se ejecutan de forma rápida antes de pasar al siguiente estado.
- **Actividades** se representan dentro de un estado y continúan durante el tiempo que el sistema permanece en ese estado.