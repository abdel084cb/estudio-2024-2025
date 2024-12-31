![[Pasted image 20241224213849.png]]

- Patrones estructurales
    - Establecen cómo se componen clases y objetos para formar estructuras mayores que implementan nueva funcionalidad.
- Patrones de comportamiento
    - Describen algoritmos y asignación de responsabilidades a objetos.
    - Describen cómo se comunican los objetos, cooperan y distribuyen las responsabilidades para lograr sus objetivos.
- Patrones de creación
    - Abstraen el proceso de instanciación.
    - Ayudan a que el sistema sea independiente de cómo se crean, componen y representan los objetos.
### Patrones Estructurales

![[Pasted image 20241224213945.png]]
#### Patrón Composite

El **patrón Composite** es un patrón de diseño estructural que permite tratar de manera uniforme a **objetos simples** y **estructuras compuestas** (jerarquías). Es ideal para representar relaciones jerárquicas "parte-todo".

**Intención**
- Permite que el cliente trabaje de la misma forma con objetos individuales y compuestos.
- Representa jerarquías recursivas "parte-todo".

Las **estructuras jerárquicas "parte-todo"** son una forma de organización en la que se representa una relación en la que:
1. **"Parte"**: Son los elementos individuales que componen un todo. Por ejemplo, en un auto, el motor o las ruedas son "partes".
2. **"Todo"**: Es el conjunto o estructura formada por las partes. Por ejemplo, el auto completo que agrupa el motor, las ruedas y demás componentes.
Estas estructuras tienen una **organización jerárquica** similar a un árbol, donde:
- Los nodos superiores representan el **todo** (la composición).
- Los nodos inferiores o terminales representan las **partes** individuales.

El patrón Composite permite tratar tanto a las "partes" como al "todo" de la misma forma, facilitando la manipulación de estructuras complejas sin diferenciar entre objetos individuales y conjuntos.

**Participantes**
1. **Componente**:
    - Interfaz común para objetos simples y compuestos.
    - Declara las operaciones que implementan hojas y compuestos.
2. **Hoja**:
    - Representa los objetos simples (nodos terminales).
    - No tiene hijos.
3. **Compuesto**:
    - Representa nodos con hijos (otros compuestos u hojas).
    - Implementa las operaciones y administra sus hijos.
4. **Cliente**:
    - Interactúa con objetos simples y compuestos a través de la interfaz común.

![[Pasted image 20241224215856.png]]

**Ejemplos:**

La relación con un asterisco (*) junto al atributo **`children`** indica que un objeto de tipo `Picture` puede contener **múltiples objetos `Graphic`** como hijos.
![[Pasted image 20241224215953.png]]

#### Patrón Adapter
El **Patrón Adapter** es un patrón de diseño estructural que actúa como un puente entre dos interfaces incompatibles. Permite que clases que no podrían trabajar juntas debido a sus diferencias de interfaz lo hagan mediante la creación de un adaptador que traduce una interfaz en otra.

 **Intención**
- Permitir que dos clases incompatibles trabajen juntas transformando la interfaz de una clase en otra que el cliente espera.
- Resolver problemas de integración cuando una clase no puede cambiarse pero debe colaborar con otra.

**Participantes**
1. **Cliente**:
    - La clase o componente que utiliza la interfaz objetivo para interactuar con los objetos.
2. **Target**:
    - Define la interfaz esperada por el cliente.
3. **Adaptee**:
    - Clase existente que necesita adaptarse para ser utilizada por el cliente. Tiene una interfaz incompatible con la que el cliente espera.
4. **Adapter**:
    - Clase que implementa la interfaz `Target` y traduce las solicitudes del cliente en llamadas específicas a los métodos de la clase `Adaptee`
![[Pasted image 20241224220622.png]]
#### Patrón Bridge
El **Patrón Bridge** es un patrón de diseño estructural que se utiliza para desacoplar una abstracción de su implementación, permitiendo que ambas evolucionen independientemente. Este patrón es especialmente útil cuando se necesita evitar la proliferación de clases debido a la combinación de múltiples variantes de abstracciones e implementaciones.

 **Intención del Patrón Bridge**
- Separar una abstracción (Handle) de su implementación (Body) para que puedan variar independientemente.
- Resolver el problema de combinaciones explosivas de clases, evitando una jerarquía rígida.

**Participantes del Patrón Bridge**
1. **Abstraction (Handle)**:
    - Define una interfaz abstracta de alto nivel que utiliza el cliente.
    - Contiene una referencia a un objeto del tipo `Implementor`.
2. **AbstrationImpl**:
    - Una especialización concreta de la abstracción que agrega comportamiento específico.
    - Utiliza los servicios de la implementación a través del objeto `Implementor`.
3. **Implementor (Body)**:
    - Define la interfaz para la implementación concreta.
    - Proporciona las operaciones de bajo nivel que la abstracción utiliza para realizar sus tareas.
4. **ConcreteImplementor**:
    - Una implementación concreta de la interfaz `Implementor`.

* **Similitudes con el patrón Adapter
	* Ambos se utilizan para ocultar los detalles de la implementación subyacente
* **Diferencias con el patrón Adapter
	* El patrón Adapter está orientado a conseguir que componentes no relacionados trabajen juntos
	*  Se aplica a sistemas que ya están diseñados (reingeniería)
	* Un Bridge , por otro lado, se utiliza por adelantado en un diseño para permitir que las abstracciones y las implementaciones varíen independientemente
![[Pasted image 20241224221033.png]]

**Ejemplos:**
![[Pasted image 20241224221827.png]]
#### Patrón Façade
El **Patrón Façade** es un patrón de diseño estructural que proporciona una interfaz simplificada a un conjunto más complejo de subsistemas o clases. Sirve como un "punto de entrada" único para interactuar con un sistema, ocultando la complejidad subyacente y facilitando su uso para los clientes.
**Intención del Patrón Façade**
- Proveer una **interfaz unificada y simplificada** a un conjunto de interfaces de un subsistema.
- Reducir la dependencia entre los clientes y las partes internas de un sistema.
- Mejorar la **legibilidad y mantenimiento** del código al encapsular la complejidad de un subsistema.
**Participantes del Patrón Façade**
1. **Façade**:
    - Proporciona una interfaz más sencilla para acceder a las funcionalidades del subsistema.
    - Puede contener referencias a los componentes del subsistema y delegarles las solicitudes del cliente.
2. **Subsistemas**:
    - Son las clases o componentes internos que contienen la lógica y funcionalidad real.
    - No están directamente expuestos al cliente, sino que son utilizados a través de la fachada.
3. **Cliente**:
    - Interactúa únicamente con el **Façade**, sin preocuparse de los detalles internos del subsistema.
**Cómo funciona el Façade**
1. El cliente solicita una operación al **Façade**.
2. El **Façade** traduce esa solicitud y la delega a los componentes apropiados del subsistema.
3. Los componentes del subsistema realizan las operaciones requeridas y devuelven el resultado al cliente a través del **Façade**.
![[Pasted image 20241224222257.png]]

**Ejemplos:**
![[Pasted image 20241224222408.png]]
#### Patrón Proxy
El **Patrón Proxy** es un patrón de diseño estructural que proporciona un representante o sustituto de un objeto para controlar el acceso al mismo. Es decir, crea un intermediario que actúa como si fuera el objeto real, permitiendo añadir control, optimización o seguridad sin cambiar el objeto original.

**Intención del Patrón Proxy**
- Proveer un **sustituto controlado** que actúa como el objeto real.
- Controlar el acceso al objeto real según sea necesario.
- Usar un proxy en lugar del objeto real para añadir funcionalidades adicionales, como caché, permisos o cargas diferidas.

**Participantes del Patrón Proxy**
1. **Interfaz Común (Subject)**:
    - Define una interfaz común que tanto el objeto real como el proxy implementan.
    - Permite que el cliente interactúe con el proxy o el objeto real de la misma manera.
2. **Objeto Real (RealSubject)**:
    - Es el objeto que realiza la funcionalidad real.
    - El proxy delega las solicitudes al objeto real cuando es necesario.
3. **Proxy**:
    - Contiene una referencia al objeto real.
    - Implementa la misma interfaz que el objeto real.
    - Controla el acceso al objeto real y puede añadir funcionalidades adicionales.
4. **Cliente**:
    - Interactúa con el objeto a través de la interfaz común, sin preocuparse de si está tratando con el proxy o el objeto real.

- **Proxy Remoto**:
    - Actúa como un representante local para un objeto ubicado en un espacio de direcciones diferente.
    - Es útil para minimizar comunicaciones mediante el cacheo de información, especialmente cuando la información no cambia con frecuencia.
- **Proxy Virtual**:
    - Sirve como sustituto para objetos cuyo tamaño es demasiado grande para ser creado o descargado de inmediato.
    - Retrasa evaluaciones o cálculos costosos, lo que resulta ideal para optimizar el uso de memoria o tiempo de inicialización.
- **Proxy de Protección**:
    - Proporciona control de acceso al objeto real.
    - Es útil cuando diferentes usuarios u objetos requieren distintos derechos de acceso o visualización al mismo recurso, como un documento compartido
![[Pasted image 20241224222920.png]]
**Ejemplos:**
![[Pasted image 20241224223254.png]]
![[Pasted image 20241224223403.png]]
### Patrones de Comportamiento
![[Pasted image 20241224225723.png]]
#### Patrón Command
El patrón **Command** es un patrón de diseño que encapsula una solicitud como un objeto, permitiendo parametrizar clientes con diferentes solicitudes, encolar o registrar solicitudes, y soportar operaciones que se pueden deshacer.

**Intención**
- Encapsular una solicitud como un objeto, lo que permite:
    - Pasar solicitudes como argumentos a otros objetos.
    - Encolar y registrar solicitudes.
    - Implementar funcionalidades como deshacer/rehacer.
 
 **Participantes**
1. **Command (Comando)**
    - Declara una interfaz para ejecutar una operación.
2. **ConcreteCommand (Comando Concreto)**
    - Implementa la interfaz `Command`.
    - Almacena una referencia al receptor (receiver).
    - Llama a los métodos correspondientes del receptor para ejecutar la operación.
3. **Receiver (Receptor)**
    - El objeto que realiza la acción asociada al comando.
    - Contiene la lógica de negocio necesaria.
4. **Invoker (Invocador)**
    - Almacena el comando y lo ejecuta cuando se solicita.
    - Puede almacenar una lista de comandos para soportar la ejecución secuencial o deshacer.
5. **Client (Cliente)**
    - Crea los comandos concretos y configura el invocador con ellos.
 
 **Estructura**
El patrón se compone de los siguientes elementos clave:
1. **Cliente**: Configura la relación entre los comandos y el invocador.
2. **Invocador**: Llama al método `execute()` en el comando.
3. **Comando Concreto**: Implementa el método `execute()` y llama al receptor para realizar la acción.
4. **Receptor**: Ejecuta la lógica real de la acción.

![[Pasted image 20241224230250.png]]
![[Pasted image 20241224230416.png]]


**Ejemplos:**

 Componentes del Ejemplo:
1. **Command**:
    - Es la interfaz que define el método `execute()`.
    - Todas las acciones (como pegar o cortar) se implementan como comandos concretos que heredan de esta interfaz.
2. **PasteCommand** (Comandos Concretos):
    - Implementa el método `execute()` y define qué debe hacerse.
    - En este caso, invoca el método `paste()` del receptor (documento).
3. **Receiver (Receptor)**:
    - Es el objeto que realmente realiza la acción cuando se invoca un comando.
    - En este caso, el receptor es un **Document** (Documento), que tiene métodos como `open()`, `close()`, `cut()`, `copy()`, y `paste()`.
4. **Invoker (Invocador)**:
    - Es el componente que interactúa con el comando.
    - Aquí, el **MenuItem** (Elemento de menú) actúa como invocador.
    - Cuando se hace clic en un elemento de menú, este llama al método `execute()` del comando asociado.
5. **Client (Cliente)**:
    - Configura los comandos asignándolos a los elementos del menú.
    - Por ejemplo, asocia el comando `PasteCommand` al botón "Pegar" del menú.

![[Pasted image 20241224230516.png]]
![[Pasted image 20241224230530.png]]


#### Patrón Observer
El **Patrón Observer** (también conocido como **Publish and Subscribe**) es un patrón de diseño de comportamiento que permite establecer una relación uno a muchos entre objetos, de modo que cuando un objeto cambia de estado, todos los objetos dependientes (observadores) son notificados y actualizados automáticamente.
 
 **Intención:
- **Definir una dependencia uno-a-muchos** entre objetos, de manera que cuando uno de ellos cambie de estado, notifique automáticamente a todos los demás.
- Facilitar la comunicación entre objetos desacoplados.
**Componentes del Patrón Observer:
1. **Subject (Sujeto)**:
    - Es el objeto que contiene el estado principal.
    - Mantiene una lista de observadores (suscriptores) interesados en sus cambios.
    - Define métodos para **agregar, eliminar y notificar observadores**:
        - `attach(observer)`
        - `detach(observer)`
        - `notify()`
2. **Observer (Observador)**:
    - Es una interfaz o clase abstracta que define el método `update()`, el cual será llamado por el sujeto para notificar cambios.
    - Cada observador se suscribe al sujeto para recibir actualizaciones.
3. **ConcreteSubject (Sujeto Concreto)**:
    - Implementa la lógica del sujeto.
    - Mantiene su propio estado y llama al método `notify()` cuando ocurre un cambio.
4. **ConcreteObserver (Observador Concreto)**:
    - Implementa la interfaz de observador.
    - Contiene la lógica específica que se ejecuta cuando recibe una notificación del sujeto.

![[Pasted image 20241224232348.png]]
![[Pasted image 20241224232514.png]]
![[Pasted image 20241224232659.png]]
#### Patrón Mediator
El **Patrón Mediator** es un patrón de diseño de comportamiento que facilita la comunicación entre objetos sin que estos dependan directamente unos de otros. En lugar de que los objetos interactúen entre sí de manera directa (lo que genera un fuerte acoplamiento), este patrón introduce un **mediador** que centraliza y coordina la comunicación.

**Intención del Patrón Mediator:
- **Centralizar la comunicación** entre varios objetos para reducir las dependencias mutuas.
- Evitar el "enredo" de conexiones entre objetos, creando un sistema más limpio y fácil de mantener.
**Motivación:**
Cuando múltiples objetos interactúan entre sí, pueden generar dependencias mutuas complicadas. Este patrón **desacopla los objetos** al introducir un mediador que se encarga de coordinar las interacciones.

Ejemplo: En una interfaz gráfica, varios componentes como botones, cuadros de texto y listas pueden necesitar interactuar entre ellos. Sin un mediador, cada componente tendría que estar consciente de los demás, complicando el diseño.

**Componentes del Patrón Mediator:**
- **Mediator (Interfaz Mediador):**
    - Define la interfaz para la comunicación entre los objetos (componentes).
    - Actúa como punto central para coordinar las interacciones.
- **ConcreteMediator (Mediador Concreto):**
    - Implementa la lógica de coordinación entre los colegas (componentes).
    - Contiene referencias a los objetos colegas, lo que le permite gestionar la comunicación entre ellos.
    - Decide qué acciones tomar en función de los eventos que recibe de los colegas.
- **Colleague (Colega):**
    - Representa los objetos que participan en la interacción.
    - Cada colega tiene una referencia al Mediador, pero no conoce a otros colegas directamente.
    - Notifica al Mediador sobre eventos y recibe comandos de este.
- **ConcreteColleague (Colega Concreto):**
    - Son las implementaciones específicas de los objetos colegas.
    - Ejecutan su lógica principal pero delegan las interacciones o comunicación al Mediador.
    - Se aseguran de que su comportamiento esté desacoplado de otros colegas gracias al Mediador.
    - Por ejemplo, un botón, un cuadro de texto o una lista desplegable en una interfaz gráfica serían **ConcreteColleagues**.
![[Pasted image 20241224234448.png]]

**Ejemplos:**
![[Pasted image 20241224234809.png]]
![[Pasted image 20241224235017.png]]
#### Patrón Strategy
El patrón **Strategy** es un patrón de diseño de comportamiento que permite definir una familia de algoritmos, encapsularlos en clases separadas y hacerlos intercambiables en tiempo de ejecución. Este patrón se utiliza cuando hay múltiples maneras de realizar una tarea, y se quiere seleccionar o cambiar el algoritmo sin alterar el código del cliente que utiliza esos algoritmos.

 **Intención del Patrón Strategy**
1. Permitir que un algoritmo sea seleccionado en tiempo de ejecución.
2. Desacoplar el comportamiento de un objeto de su implementación.
3. Facilitar la extensión o modificación de los algoritmos sin modificar la clase cliente.

 **Componentes del Patrón Strategy**
- **Policy (Cliente):**
    - Es el objeto que solicita un servicio al `Context`.
    - Interactúa con el `Context`, pero no necesita conocer detalles de las estrategias específicas.
    - Decide qué estrategia concreta se utilizará y la configura en el `Context`.
- **Context (Contexto):**
    - Representa el cliente directo de las estrategias.
    - Contiene una referencia a un objeto del tipo `Strategy`.
    - Tiene un método (`contextInterface()`) que delega la ejecución del algoritmo a la estrategia actualmente configurada.
    - Encapsula y abstrae la relación entre el cliente (`Policy`) y las estrategias concretas.
- **Strategy (Estrategia):**
    - Es una interfaz o clase abstracta que define el contrato común para todas las estrategias.
    - Declara un método (`algorithmInterface()`) que será implementado por las estrategias concretas.
- **ConcreteStrategyA, ConcreteStrategyB, ConcreteStrategyC (Estrategias Concretas):**
    - Implementan el método definido en `Strategy`.
    - Cada una representa un algoritmo o comportamiento específico.
    - Se pueden intercambiar dinámicamente en tiempo de ejecución, permitiendo flexibilidad al sistema.

![[Pasted image 20241224235537.png]]
**Ejemplos:**
![[Pasted image 20241224235933.png]]

### Patrones de Creación
![[Pasted image 20241225001446.png]]
#### Patrón Abstract Factory
El **Patrón Abstract Factory** es un patrón de diseño creacional que proporciona una interfaz para crear familias de objetos relacionados o dependientes sin especificar sus clases concretas. Este patrón es útil cuando el sistema debe ser independiente de cómo se crean, componen o representan los productos, o cuando se requiere garantizar que los objetos creados sean compatibles entre sí.

 **Intención del Patrón Abstract Factory**
- Proporcionar una interfaz para crear familias de objetos relacionados.
- Permitir que las familias de objetos cambien dinámicamente en tiempo de ejecución.
- Garantizar la compatibilidad entre los objetos creados por una misma fábrica.

 **Componentes del Patrón Abstract Factory**
1. **AbstractFactory (Fábrica Abstracta):**
    - Declara una interfaz para crear cada tipo de producto.
    - Define métodos para producir diferentes tipos de objetos (familias de productos).
2. **ConcreteFactory (Fábrica Concreta):**
    - Implementa la interfaz de la fábrica abstracta.
    - Crea objetos concretos de cada tipo de producto, asegurando que sean compatibles.
3. **AbstractProduct (Producto Abstracto):**
    - Declara una interfaz para cada tipo de producto que se puede crear.
4. **ConcreteProduct (Producto Concreto):**
    - Implementa la interfaz del producto abstracto.
    - Representa las instancias específicas de los productos que se crean por las fábricas concretas.
5. **Client (Cliente):**
    - Usa únicamente las interfaces declaradas en las fábricas y los productos abstractos.
    - Permanece independiente de las implementaciones concretas de los productos.

![[Pasted image 20241225001916.png]]
**Ejemplos:**
No Abstract Factory:
![[Pasted image 20241225002035.png]]
Abstract Factory:
![[Pasted image 20241225002052.png]]
#### Patrón Singleton
El **Patrón Singleton** es un patrón de diseño creacional que asegura que una clase tenga **una única instancia** y proporciona un punto global de acceso a ella. Este patrón es útil cuando se necesita un único objeto que coordine acciones en todo el sistema, como un registro de configuración, un administrador de base de datos, o un gestor de conexiones.

 **Intención del Patrón Singleton**
- Garantizar que una clase tenga **una única instancia** en todo el sistema.
- Proveer un punto global de acceso a esta instancia.
- Controlar el acceso a los recursos compartidos o a configuraciones globales.

![[Pasted image 20241225002534.png]]
### Pistas para identificar patrones de diseño:
![[Pasted image 20241225002618.png]]
![[Pasted image 20241225002733.png]]

### Definiciones breves de los patrones:

 **Patrones Estructurales**
1. **Patrón Composite**:
    - Permite tratar objetos individuales y compuestos de manera uniforme. Útil para estructuras jerárquicas como árboles.
    - **Úsalo cuando**: Necesites manejar colecciones de objetos como si fueran un único objeto.
2. **Patrón Adapter**:
    - Convierte la interfaz de una clase en otra que el cliente espera.
    - **Úsalo cuando**: Quieras que dos clases incompatibles trabajen juntas.
3. **Patrón Bridge**:
    - Separa una abstracción de su implementación para que ambas puedan evolucionar independientemente.
    - **Úsalo cuando**: Tengas varias dimensiones de cambio en una jerarquía de clases.
4. **Patrón Façade**:
    - Proporciona una interfaz simplificada para un conjunto de subsistemas complejos.
    - **Úsalo cuando**: Quieras ocultar la complejidad de un sistema.
5. **Patrón Proxy**:
    - Proporciona un representante para controlar el acceso a otro objeto.
    - **Úsalo cuando**: Necesites controlar acceso o mejorar el rendimiento.

 **Patrones de Comportamiento**
6. **Patrón Command**:
    - Encapsula solicitudes como objetos, permitiendo operaciones como deshacer y cola de comandos.
    - **Úsalo cuando**: Quieras separar la lógica de comandos del receptor.
8. **Patrón Observer**:
    - Define una relación de uno a muchos, donde un cambio en un objeto se notifica automáticamente a otros.
    - **Úsalo cuando**: Necesites que varios objetos reaccionen a cambios en otro.
8. **Patrón Mediator**:
    - Facilita la comunicación entre objetos desacoplándolos mediante un mediador central.
    - **Úsalo cuando**: Quieras reducir las dependencias entre múltiples objetos.
9. **Patrón Strategy**:
    - Define una familia de algoritmos, encapsulándolos y haciéndolos intercambiables.
    - **Úsalo cuando**: Quieras cambiar algoritmos dinámicamente.
 **Patrones de Creación**
10. **Patrón Abstract Factory**:
    - Proporciona una interfaz para crear familias de objetos relacionados sin especificar sus clases concretas.
    - **Úsalo cuando**: Quieras garantizar la compatibilidad entre los objetos creados.
11. **Patrón Singleton**:
    - Garantiza que una clase tenga una única instancia y proporciona un punto de acceso global.
    - **Úsalo cuando**: Necesites un único punto de control.
### Guía para elegir patrones:
1. **¿Es un problema de estructura?**
    - **Sí**:
        - ¿Necesitas manejar jerarquías de objetos? → **Composite**
        - ¿Clases incompatibles deben trabajar juntas? → **Adapter**
        - ¿Separar abstracción e implementación? → **Bridge**
        - ¿Simplificar una interfaz compleja? → **Façade**
        - ¿Controlar acceso o mejorar rendimiento? → **Proxy**
2. **¿Es un problema de comportamiento?**
    - **Sí**:
        - ¿Encapsular acciones o comandos? → **Command**
        - ¿Notificar cambios entre objetos? → **Observer**
        - ¿Reducir dependencias en comunicación? → **Mediator**
        - ¿Cambiar algoritmos en tiempo de ejecución? → **Strategy**
3. **¿Es un problema de creación?**
    - **Sí**:
        - ¿Crear familias de objetos relacionados? → **Abstract Factory**
        - ¿Garantizar una sola instancia? → **Singleton**