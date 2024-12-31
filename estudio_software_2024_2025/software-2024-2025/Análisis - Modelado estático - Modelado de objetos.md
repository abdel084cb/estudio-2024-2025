**¿Cuál es la solución del problema?

*La estructura estática del sistema: Modelo de
objetos

*El comportamiento del sistema: Modelo dinámico*


#### Objetos

* `<nombre_del_objeto>: <nombre_de_la_clase>`
* `: <nombre_de_la_clase> `
	* Objeto anónimo de una clase en concreto.
* `<nombre_del_objeto>: <nombre_de_la_clase> [<estado>]`
![[Pasted image 20241221185714.png]]
#### Clases

*Una clase describe un grupo de objetos que
comparten propiedades (atributos y
operaciones), restricciones, relaciones con otros
y tienen una semántica común*

* Representación de clases en UML:
	* nombre
	* atributos
	* operaciones
![[Pasted image 20241221190057.png]]
![[Pasted image 20241221190234.png]]
- **Método**: Implementación concreta de una operación.
- **Operación que modifica el estado**: Cambia atributos del objeto (p. ej., `mover`).
- **Consulta**: Operación que no altera el estado del objeto, como `seleccionar`.
- **Atributo derivado**: Consulta sin parámetros que calcula su valor en tiempo real.
![[Pasted image 20241221190623.png]]
#### Dependencia

![[Pasted image 20241221190903.png]]
**PeliculaDeVideo depende de Canal**.
- En el diagrama UML, la **línea discontinua con una flecha** apunta de **PeliculaDeVideo** hacia **Canal**.
- Esto significa que **PeliculaDeVideo necesita a Canal para realizar ciertas operaciones** (como el método `reproducirEn(c:Canal)`), pero **Canal no necesita a PeliculaDeVideo** para existir o funcionar.

#### Asociación

La asociación implica que las clases asociadas pueden interactuar mutuamente (dependiendo de varios factores, esto puede cambiar).

![[Pasted image 20241221191402.png]]
* Nombres de la asociación
	![[Pasted image 20241221191456.png]]
* Roles
	![[Pasted image 20241221191534.png]]
	* Los roles se utilizan para recorrer las asociaciones. Se ven como pseudoatributos unaPersona.empleador
	* Los roles son opcionales si el modelo no es ambiguo
	* Si hay varias asociaciones entre las clases entonces hay que usar roles y/o nombres de asociación para distinguirlas
		![[Pasted image 20241221191751.png]]
	* Los roles son obligatorios en las asociaciones reflexivas
		![[Pasted image 20241221191839.png]]
* Multiplicidad
	* Indica cuántos objetos de una clase se relacionan con una única instancia de la otra clase de la asociación
		![[Pasted image 20241221200019.png]]
		 ![[Pasted image 20241221200054.png]]
	* Cada instancia de la clase `A` puede "contener / estar asociada" de 0 a 1 instancias de la clase B.
	* Cada instancia de la clase `B` puede estar asociada 3 a 8 instancias de la clase `A`
	* Cada persona puede ser empleado en 0 o varias empresas. Mientras que una empresa puede tener 1 o varios empleados.
		* 1 es equivalente a 1..1
		* `*` es equivalente a `0..*`
	* `valorMin..valorMax`

#### Navegación y visibilidad

En la fase de análisis todas las asociaciones son consideradas bidireccionales.
Sin embargo en diseño aparece la Navegación y Visibilidad.

* <u>La navegación</u> indica que un objeto puede llegar a los objetos del otro extremo. Es la **dirección en que puede accederse a los objetos** de una relación. En UML, esto se representa con flechas que indican cómo un objeto puede acceder al otro.
	- Ejemplo: En este diagrama, `Usuario` puede acceder a `Clave`, ya que hay una flecha de navegación hacia `Clave`.
		![[Pasted image 20241221200748.png]]
- <u>La visibilidad</u> es una propiedad más conceptual que indica si un objeto **es accesible desde fuera de la asociación**.
	- En este caso, `Clave` no es visible para `GrupoUsuarios`, porque no hay una relación directa entre ellos. Solo un `Usuario` tiene visibilidad sobre sus propias claves.
		![[Pasted image 20241221201411.png]]

#### Clase asociación

* Un `Usuario` podría tener permiso de **lectura** para un `Fichero A` pero permiso de **lectura y escritura** para un `Fichero B`. Estos detalles (los permisos) no son atributos propios de `Usuario` ni de `Fichero`, sino de la relación entre ambos.
		![[Pasted image 20241221202902.png]]
		![[Pasted image 20241221203606.png]]
* El siguiente diagrama explica cómo se puede utilizar una clase de asociación para modelar relaciones que tienen atributos y comportamientos propios, en lugar de pertenecer únicamente a las clases que conecta.
			![[Pasted image 20241221204457.png]]


#### Calificación

La calificación en el contexto de diseño de software o modelado UML se refiere a un mecanismo que permite restringir una asociación entre dos clases usando un atributo llamado calificador. Este atributo actúa como un "filtro" que reduce la multiplicidad de la relación y especifica cómo se accede a los objetos relacionados.

![[Pasted image 20241221210329.png]]

 **Relación entre `Directorio` y `Archivo` (parte superior derecha)**
- **Con calificación (`nombre`):**
    - Aquí se introduce un calificador llamado `nombre` que permite identificar de manera única un `Archivo` dentro de un `Directorio`.
    - Esto implica que, aunque un directorio puede contener múltiples archivos, cada archivo se distingue por su `nombre` dentro de ese directorio.
    - La multiplicidad cambia a `1..1` porque, dado un nombre específico, solo puede haber un archivo en ese directorio.

**Relación entre `DescripcionVuelo` y `Vuelo`**
- **Con calificación (`fecha_salida`):**
    - Se añade un calificador llamado `fecha_salida` para identificar un vuelo específico de una `DescripcionVuelo`.
    - Esto indica que un vuelo en particular está determinado por su `fecha_salida` en relación con su descripción.
    - La multiplicidad se reduce a `1..1`, lo que significa que, dado un número de vuelo y una fecha de salida, solo puede haber un vuelo real.

**En algunos casos no se reduce la multiplicidad:**
![[Pasted image 20241221211435.png]]
A pesar de introducir un calificador (`oficina`), **la multiplicidad no se reduce**:
- La multiplicidad en el extremo de `Persona` es `1..*`, lo que significa que cada `Empresa` está asociada con al menos una `Persona`.
- En el extremo de `Empresa`, la multiplicidad es `*`, lo que significa que cada persona puede estar relacionada con varias empresas (por ejemplo, a través de diferentes oficinas).
- La relación sigue permitiendo que una `Empresa` tenga muchas personas y que cada persona esté asociada a una o más empresas.
- Esto ocurre porque el calificador agrega una dimensión adicional (la oficina), pero no cambia las reglas de cuántas personas pueden estar asociadas con una empresa o viceversa.

**Los calificadores pueden ser compuestos:**
![[Pasted image 20241221212231.png]]![[Pasted image 20241221212438.png]]
*Es obvio entenderlo mirando ambas imágenes...*


#### Asociaciones n-arias

- **Team (Equipo):**
    - Representa un equipo.
    - Puede participar en múltiples combinaciones de temporadas y jugadores.
- **Player (Jugador):**
    - Representa un jugador.
    - Puede pertenecer a múltiples equipos en diferentes temporadas.
- **Year (Año):**
    - Representa una temporada (año).
    - Cada temporada puede incluir múltiples equipos y jugadores.
![[Pasted image 20241221213502.png]]

#### Agregaciones

* La agregación es una forma especial de asociación.
* Modela una relación todo/parte o tiene un
* Una clase (`el todo`) consta de elementos más pequeños (`las partes`)
![[Pasted image 20241221220107.png]]

#### Composiciones

* Es una relación de pertenencia y vidas coincidentes de la parte con el todo
* Las partes pueden crearse después del todo pero una vez creadas viven y mueren con él
* El todo gestiona la creación y destrucción de las partes
* Las partes no tienen existencia independiente
![[Pasted image 20241222170716.png]]
- Cada "Coche" tiene exactamente **un Motor** (`1`) y **una Carrocería** (`1`).
- A su vez, un "Motor" o una "Carrocería" solo pertenecen a un único "Coche" (`1`).
* En la composición, el todo también se llama objeto compuesto y las partes las componentes

![[Pasted image 20241222171409.png]]

* En la composición, un objeto puede formar parte de sólo una parte compuesta a la vez. No se reutilizan los componentes
* En la agregación, una parte se puede compartir por varios agregados

![[Pasted image 20241222171639.png]]
* En la composición existe la propagación de operaciones y atributos
#### Herencia

![[Pasted image 20241222171830.png]]
* Desde el punto de vista de la implementación es un mecanismo de reutilización de código
* Desde un punto de vista conceptual es una abstracción para compartir similitudes entre clases al tiempo que se mantienen sus diferencias


![[Pasted image 20241222172008.png]]
* Las subclases heredan atributos y métodos de la superclase, pudiendo añadir los suyos propios
	* Parte heredada o derivada
	* Parte emergente o incremental

#### Discriminadores

![[Pasted image 20241222172415.png]]
* El diagrama muestra el concepto de **discriminadores** en la generalización de clases en UML. Los discriminadores son etiquetas que indican qué propiedad o criterio se usa para diferenciar subclases dentro de una jerarquía de generalización.

#### Matices

* Los **matices** en un modelo de generalización en UML son reglas o restricciones que determinan cómo se relacionan las clases padre con las clases hijas.
	* complete : no se permiten clases hijas adicionales
	* incomplete : se permiten clases hijas adicionales
	* disjoint : los objetos de la clase padre no pueden tener más de una de las clases hijas como tipo; clases mutualmente incompatibles si se crea una nueva clase hija con herencia múltiple
	* overlapping : los objetos de la clase padre pueden tener más de una de las clases hijas como tipo; clases compatibles si se crea una nueva clase hija con herencia múltiple
	* Posibles combinaciones:
		* {complete ,disjoint}
		* {complete, overlapping}
		* {incomplete, disjoint}
		* {incomplete, overlapping}
![[Pasted image 20241222173506.png]]
#### Redefinición de operaciones

* **Redefinición de operaciones**: por definición de especialización, las operaciones aplicables a una clase lo son a todas sus subclases.
* Redefinición por extensión: la nueva operación es la misma que la heredada pero añade nuevo comportamiento que suele afectar a los nuevos atributos de la subclase
		![[Pasted image 20241222174734.png]]
* Redefinición por restricción: La nueva operación restringe el protocolo de la heredada. La restricción no puede afectar al número de parámetros, únicamente al tipo. Los nuevos tipos deben ser subtipos de los iniciales
			![[Pasted image 20241222175340.png]]
* Redefinición por optimización: aprovecha las características de la nueva clase añadiendo un código más eficiente
		![[Pasted image 20241222175719.png]]
* Consideraciones:
	* Se heredan todas las operaciones: consulta, actualización, creación y destrucción
	* Una operación no puede ser redefinida para que se comporte de modo distinto
	* Se puede añadir un comportamiento adicional
	* Todas las operaciones deben tener la misma interfaz

* En Análisis la herencia es conceptual no un mero mecanismo de reutilización de código
		![[Pasted image 20241222180132.png]]

#### Clases abstractas

* Una clase abstracta no posee instancias, pero sus descendientes sí
* Una clase abstracta tiene al menos una operación sin código y por tanto no pueden instanciarse
* Las operaciones sin código deben definirse en las subclases.
* Todas las subclases concretas suministran la implementación
* Una clase abstracta puede implementarse en su totalidad (o parcialmente)
![[Pasted image 20241222180353.png]]
#### Herencia múltiple

* Cuando una clase tiene más de una clase antecesora directa
* Hereda los atributos y operaciones definidos en todas las clases antecesoras
* Una característica que llegue por distintas vías sólo se heredará una vez
![[Pasted image 20241222182937.png]]

#### Delegación

* Mecanismo mediante el cual un objeto le pasa una operación a otro para que la ejecute
* Delegación empleando agregación de roles 
	* La superclase se refunde en forma de agregado, donde cada componente sustituye a una generalización
	* Sustituye un único objeto (con una única identidad) por un grupo de objetos
	- En lugar de tratar una superclase única que agrupe todas las características posibles de un empleado (como nómina y pensión), estas características se modelan como clases separadas conectadas mediante agregación.
	- Esto permite que la clase principal `Empleado` delegue responsabilidades en componentes específicos, como `NominaEmpleado` y `PensionEmpleado`.
	![[Pasted image 20241222183315.png]]
* Heredar la clase más importante y delegar el resto
	* Se mantiene la identidad y la herencia a través de una generalización
	 ![[Pasted image 20241222183912.png]]
* Generalización anidada
	* Primero se factoriza por una generalización y después por otra
	* Mantiene la herencia pero se multiplican las posibles combinaciones
	![[Pasted image 20241222184041.png]]
* Consideraciones:
	- Si una subclase tiene varias superclases igualmente importantes, puede ser mejor utilizar **delegación** para distribuir las responsabilidades.
	- Si una superclase es más importante que las demás, se puede utilizar **herencia simple** para la clase principal y **delegación** para los aspectos secundarios.
	- Si el número de combinaciones posibles entre clases es pequeño, **anidar** puede ser una solución adecuada.
	- Se recomienda **anidar primero según el criterio más importante** y continuar con los siguientes criterios en orden de prioridad.
	- Si una superclase tiene más atributos que las otras o representa un cuello de botella en el rendimiento, se debe **mantener la herencia principal a través de esa superclase**.
	- Si es importante **mantener la identidad de los objetos**, la única solución adecuada es usar **generalización anidada**.

#### Pasos recomendados:
###### **Paso 1: Identificar Clases**

- Hacer una lista inicial exhaustiva con los **sustantivos** que aparecen en los requisitos.
###### **Paso 2: Retener las Clases Correctas**

- Revisar la lista inicial para descartar:
    - **Clases redundantes:** Duplicadas o superfluas.
    - **Clases irrelevantes:** No relacionadas con el dominio del problema.
    - **Clases poco precisas:** Una clase debe ser específica y bien definida.
    - **Atributos:** Si un nombre describe un objeto individual, puede ser considerado un atributo.
    - **Operaciones:** Si un nombre describe una operación aplicada a objetos, no es una clase.
    - **Roles:** El nombre de una clase debe reflejar su naturaleza intrínseca, no el rol que juega en una asociación.
###### **Paso 3: Preparar un Diccionario de Datos**

- Para cada clase, escribir un párrafo que la describa con precisión:
    - **Alcance:** Rol de la clase dentro del problema.
    - **Suposiciones:** Restricciones y características clave.

**Ejemplo: Clase "Cuenta" en un Cajero Automático:**

- _Cuenta:_ Cuenta individual de un banco a la que se pueden aplicar transacciones. Las cuentas pueden ser de varios tipos; como mínimo serán de ahorro o corrientes. Un cliente puede tener más de una.
###### **Paso 4: Identificar Asociaciones, Agregaciones y Composiciones**

- Generalmente corresponden con **verbos** en el dominio del problema.
- Usualmente reflejan:
    - Localizaciones físicas.
    - Relaciones de pertenencia o posesión.
    - Verificación de condiciones (e.g., trabaja para, dirige, casado con).
###### **Paso 5: Retener las Asociaciones Correctas**

- Revisar la lista inicial y descartar:
    - **Asociaciones irrelevantes** o específicas de implementación.
    - **Acciones:** Verbos que representan operaciones no son asociaciones.
    - **Requisitos expresados como acciones.**
    - **Asociaciones ternarias** y derivadas (si no son estrictamente necesarias).
###### **Paso 6: Identificar Atributos**

- Normalmente **no aparecen directamente** en los requisitos.
- Descartar:
    - **Identificadores:** Estos no suelen ser considerados atributos.
    - **Atributos discordantes:** Que no se alinean con el dominio del problema.
- **Simplificar el modelo:** Usar calificadores y clases asociación solo si son relevantes.
###### **Paso 7: Organizar el Diagrama con Generalización/Especialización (Herencia)**

- Revisar el modelo y aplicar **generalización/especialización** para agrupar clases con atributos y comportamientos comunes.
###### **Paso 8: Iterar el Modelo de Objetos**

- El análisis es un proceso iterativo:
    - ¿Faltan clases?
    - ¿Sobran clases?
    - ¿Faltan asociaciones?
    - ¿Sobran asociaciones?
- Construir un subconjunto inicial e ir extendiéndolo.
###### **Paso 9: Agrupar Clases en Subsistemas**

- Organizar las clases en subsistemas coherentes. _(Este paso se ampliará en el tema de Diseño del Sistema)._

**Hay que acordarse de que estamos en análisis no en diseño**
