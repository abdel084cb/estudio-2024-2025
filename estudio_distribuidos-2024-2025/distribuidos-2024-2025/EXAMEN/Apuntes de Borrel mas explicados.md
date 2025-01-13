### IP Multicast no fiable y no garantiza FIFO
IP Multicast es un protocolo que permite enviar datos desde un remitente a múltiples receptores simultáneamente de manera eficiente. En lugar de enviar una copia a cada receptor, el remitente envía una única copia y los routers replican los datos para los miembros del grupo Multicast.
IP Multicast no es fiable porque no incluye mecanismos para garantizar la entrega de los mensajes. Esto significa que los mensajes pueden perderse por problemas como congestión, y no existe confirmación de recepción ni retransmisión automática.
Además, no garantiza el orden FIFO (First-In-First-Out) porque los paquetes pueden tomar rutas diferentes en la red, provocando que lleguen desordenados. Esto puede ser un problema en aplicaciones que dependen del orden de los mensajes.

### Raft vs Máquina sin replicación
Raft utiliza más ancho de banda y genera mayor latencia en comparación con una máquina sin replicación porque requiere comunicación constante entre los nodos del clúster. Esto incluye el intercambio de latidos, la replicación de entradas al registro y las votaciones durante las elecciones de líder.

A cambio, ofrece mayor tolerancia a fallos, ya que el sistema puede continuar funcionando incluso si algunos nodos fallan, siempre que haya quórum. En una máquina sin replicación, cualquier fallo puede detener el sistema por completo. Por lo tanto, Raft sacrifica rendimiento a cambio de mayor disponibilidad y confiabilidad.

### Kerberos -> clave y DNS -> clave/valor
Kerberos utiliza un esquema basado en claves para autenticar de manera segura a los usuarios y servicios dentro de una red. Se basa en un servidor central (KDC) que almacena claves secretas compartidas y genera tickets para establecer confianza mutua entre clientes y servidores.

El sistema DNS utiliza una estructura de clave/valor para resolver nombres de dominio en direcciones IP. Cada nombre de dominio actúa como una clave, y su dirección IP asociada es el valor, facilitando la comunicación entre dispositivos en redes distribuidas.

### TCP/IP no garantiza el orden con varios canales
TCP/IP garantiza el orden de los paquetes dentro de un único canal o conexión, ya que utiliza números de secuencia para reorganizar los paquetes si llegan desordenados. Sin embargo, cuando se establecen múltiples conexiones TCP/IP simultáneamente, no hay ninguna garantía de que los datos enviados por distintos canales lleguen en el mismo orden en que se enviaron, ya que cada conexión opera de forma independiente. Esto es importante en sistemas que requieren sincronización entre varias conexiones.

### Algoritmo de consenso (Tolerancia de errores con estado) vs Algoritmo de elección de líder (Tolerancia de errores sin estado)
Un algoritmo de consenso permite que un grupo de nodos en un sistema distribuido se pongan de acuerdo en un único valor, incluso en presencia de fallos. Esto es clave para sistemas que requieren consistencia. Por otro lado, el algoritmo del Matón no es un algoritmo de consenso, ya que su propósito principal es la elección de un líder, no acordar un valor compartido entre los nodos. Aunque selecciona un líder, no aborda la garantía de un acuerdo global sobre un estado o valor.

**Sin estado (Matón):** Se asegura únicamente que haya un líder, pero no se gestiona información compartida ni la consistencia de datos previos.

**Con estado (Raft, Paxos):** Garantiza no solo la elección de un líder, sino también la consistencia del estado distribuido, permitiendo que todos los nodos lleguen a un acuerdo sobre un estado común incluso en presencia de fallo
	**Único algoritmo de consenso** que integra la **elección de líder**

### Comparativa relojes
![[Pasted image 20250112221727.png]]

### Algoritmos descentralizados
Los algoritmos descentralizados son aquellos donde todos los procesos tienen la misma responsabilidad y ningún proceso conoce el estado global del sistema. Las decisiones se toman basándose únicamente en información local y en la interacción entre procesos.

Dependiendo del algoritmo, la desventaja principal es que la falta de un líder puede aumentar la sobrecarga de comunicación, ya que cada proceso debe intercambiar mensajes con todos los demás para coordinarse. Tampoco hay tolerancia a fallos como en Raft o Matón.

En el Token Ring, los procesos se organizan en un anillo lógico. Un token especial circula entre ellos, otorgando acceso a la sección crítica solo al proceso que lo posee. Este enfoque es eficiente en mensajes, pero depende de la existencia del token, el cual debe regenerarse si se pierde.

El Algoritmo de Lamport utiliza relojes lógicos para garantizar el acceso ordenado a la sección crítica. Los procesos envían solicitudes con marcas de tiempo a todos los demás, y el acceso se otorga en orden lógico. Este método no depende de estructuras específicas, pero genera mayor sobrecarga en la red debido al número de mensajes intercambiados.

**Algoritmo RA también es descentralizado**
Cabe destacar: Orden de recepción != Orden de envío
**Ausencia de Bloqueos (Deadlocks):** No se producen bloqueos cíclicos porque las solicitudes se procesan en base a las marcas de tiempo (timestamp) de Lamport, lo que asegura un orden de prioridad bien definido. Además, los procesos siempre envían un mensaje de REPLY si no están en la sección crítica o después de haber salido de ella, lo que evita que otros procesos queden esperando indefinidamente.
**Ausencia de Inanición (Starvation):** No ocurre inanición porque las solicitudes se atienden estrictamente en el orden en que llegaron, según los timestamps. Esto garantiza que todas las solicitudes se procesen eventualmente, y ningún proceso es ignorado, ya que cada solicitud recibe una respuesta (REPLY) cuando el proceso en la sección crítica libera el acceso.

### Fallas en SSDD
Estas son las principales **fallas en sistemas distribuidos**, clasificadas según su naturaleza:
**Crash:** Ocurre cuando un proceso falla completamente y deja de funcionar, sin realizar ninguna operación más ni enviar respuestas. Es el tipo de fallo más básico y fácil de detectar.
**Omission:** Se produce cuando un proceso no responde a una petición, ya sea porque no recibió el mensaje o porque no pudo procesarlo. Esto incluye fallos en la comunicación o en el sistema.
**Timing:** El proceso responde, pero lo hace con un retardo significativo respecto al tiempo esperado. Esto puede afectar a sistemas distribuidos sensibles al tiempo.
**Response:** La respuesta recibida es incorrecta, aunque el mensaje llega en el tiempo esperado. Puede deberse a errores de cálculo o corrupción de datos.
**Byzantine:** Representa el tipo de falla más complejo, donde un proceso actúa de forma arbitraria, incluyendo enviar respuestas incorrectas intencionalmente o comportarse de manera maliciosa. Es el más difícil de manejar y requiere algoritmos especializados para tolerarlo.
### Redundancias como prevención de fallos
La **redundancia** se utiliza para prevenir fallos en sistemas distribuidos, asegurando disponibilidad y recuperación ante errores.

La **redundancia cliente** se refiere a las estrategias implementadas del lado del cliente para garantizar que sus solicitudes sean atendidas correctamente, incluso si hay fallos en los servidores que gestionan esas solicitudes.

En la **redundancia cliente**, el **algoritmo 1** aplica redundancia temporal reintentando la operación con otro servidor en caso de fallo del primero. El **algoritmo 2** combina redundancia física y temporal, enviando la solicitud a varios servidores simultáneamente y reintentando si es necesario. Ambos algoritmos manejan excepciones y errores para garantizar el correcto funcionamiento.

En la **redundancia servidor**, los fallos se detectan mediante **latidos (Heartbeat)**, donde los nodos envían señales periódicas para confirmar que están activos. En caso de fallo, los **algoritmos de elección de líder** seleccionan un nuevo proceso para coordinar las tareas críticas del grupo distribuido, asegurando la continuidad del sistema.

### CAP
En sistemas distribuidos (con estado), el **Teorema CAP** establece que es imposible garantizar simultáneamente **Consistencia**, **Disponibilidad** y **Tolerancia a particiones de red**. Las técnicas de consenso como Raft o Paxos intentan equilibrar estas tres propiedades, pero en situaciones de partición de red deben priorizar entre Consistencia y Disponibilidad.

La **Consistencia** significa que todas las lecturas reflejan las escrituras más recientes. Esto implica que los datos están sincronizados en todos los nodos, y no hay discrepancias entre ellos.

La **Disponibilidad** asegura que todas las peticiones reciben una respuesta, incluso si algunos nodos no están accesibles. Esto prioriza que el sistema siga funcionando, aunque implique lecturas potencialmente desactualizadas.

La **Tolerancia a Particiones de Red** garantiza que el sistema continúe operando incluso si hay fallos de comunicación que dividen los nodos en grupos separados.

El desafío en sistemas distribuidos es que, en presencia de particiones de red, el sistema debe elegir entre garantizar la consistencia (sacrificando disponibilidad) o la disponibilidad (sacrificando consistencia). Las técnicas de consenso priorizan consistencia y tolerancia a particiones, dejando la disponibilidad como secundaria durante fallos.
### Consenso
El **consenso** en sistemas distribuidos es el proceso mediante el cual los nodos acuerdan un valor único, incluso en presencia de fallos. Puede ser **simétrico sin líder**, donde todos los procesos tienen la misma responsabilidad, o **asimétrico con líder**, donde un nodo central coordina la decisión.
Las propiedades clave de un algoritmo de consenso son:
**Acuerdo:** Todos los procesos deben decidir el mismo valor, garantizando consistencia en el sistema.
**Terminación:** El algoritmo debe llegar a una decisión en un tiempo finito, asegurando que no quede en un estado indefinido.
**Integridad:** Una vez que un proceso decide un valor, este no puede ser modificado posteriormente.
**Validez:** El valor decidido debe ser uno de los valores originalmente propuestos, evitando decisiones arbitrarias o inconsistentes.
Estas propiedades son esenciales para garantizar la confiabilidad y consistencia en sistemas distribuidos.

### SMR
El **modelo de máquina de estados replicados** (SMR) es un enfoque en sistemas distribuidos que replica servicios manteniendo el mismo estado y comportamiento en múltiples nodos. En el caso de la **consistencia secuencial**, se busca garantizar que las operaciones sean visibles para los clientes en un orden que respete la secuencia local de cada cliente, pero no necesariamente el orden global. Esto implica que, aunque las operaciones no se aplican de forma simultánea en todas las réplicas, el sistema asegura que las respuestas sean coherentes desde el punto de vista de los usuarios.

En este modelo, las máquinas de estado ejecutan las mismas operaciones en el mismo orden dentro de cada réplica. La **consistencia secuencial** permite tolerar particiones en la red y ofrece mayor disponibilidad en comparación con modelos más estrictos, como la consistencia linealizable. Sin embargo, no asegura que todos los clientes observen el mismo orden de las operaciones al mismo tiempo, lo que puede ser una limitación para ciertas aplicaciones que requieren un orden global estricto.

**En conclusión**, el modelo de máquina de estados replicados con consistencia secuencial es adecuado para sistemas distribuidos que buscan equilibrio entre disponibilidad y coherencia, siendo ideal para escenarios donde no es crítico mantener un único orden global de las operaciones.

### Contenedores vs Virtualización nativa
![[Pasted image 20250112232256.png]]
La **virtualización nativa** y los **contenedores** son tecnologías clave para el desarrollo y despliegue de aplicaciones, pero operan a diferentes niveles. La virtualización nativa utiliza hipervisores para crear máquinas virtuales completas, cada una con su propio sistema operativo, lo que proporciona un alto grado de aislamiento y flexibilidad para ejecutar diferentes sistemas operativos en un mismo hardware. En contraste, los contenedores funcionan a nivel del sistema operativo, compartiendo el núcleo del host y aislando las aplicaciones mediante espacios de usuario, lo que los hace más ligeros y rápidos de desplegar.

En cuanto a los recursos, los contenedores son más eficientes, ya que no requieren sistemas operativos completos en cada instancia, lo que reduce el consumo de memoria y disco. Sin embargo, esto implica que el aislamiento es menor comparado con las máquinas virtuales, lo que puede ser una desventaja en entornos donde la seguridad es primordial. Por otro lado, las máquinas virtuales son más adecuadas para aplicaciones que necesitan un sistema operativo completo o acceso directo al hardware.

En resumen, los contenedores son ideales para despliegues rápidos, aplicaciones modernas y escalabilidad, mientras que la virtualización nativa es preferible para entornos heterogéneos o aplicaciones que requieren mayor aislamiento y compatibilidad con diferentes sistemas operativos.

### Kubernetes (No completo)
Los conceptos de **Deployment**, **StatefulSet**, y el uso de recursos como **Service** e **Ingress** son fundamentales en la orquestación de aplicaciones en Kubernetes y otros entornos distribuidos.
Un **Deployment** se utiliza para el despliegue de aplicaciones **sin estado**, asegurando que los pods permanezcan siempre en funcionamiento y se escalen o actualicen según las necesidades. Es ideal para aplicaciones web, microservicios o cualquier servicio que no dependa de un estado específico.
Por otro lado, un **StatefulSet** es necesario para aplicaciones **con estado**, donde cada pod tiene un identificador único y un almacenamiento persistente asociado. Esto asegura que los pods puedan mantener su estado incluso después de reinicios o escalados, siendo útil en bases de datos o sistemas de almacenamiento distribuidos.
Los recursos de red, como **Service** e **Ingress**, garantizan la accesibilidad y la tolerancia a fallos. Los **Services** proporcionan un punto de acceso estable mediante balanceo de carga interno para los pods, mientras que **Ingress** gestiona la entrada de tráfico externo, permitiendo configuraciones avanzadas de enrutamiento para servicios específicos.
En resumen, el uso combinado de Deployment, StatefulSet, Service e Ingress permite gestionar tanto aplicaciones sin estado como con estado, asegurando alta disponibilidad, accesibilidad y escalabilidad en entornos distribuidos.

### Comunicación en grupo
##### Formas de comunicación entre procesos
La comunicación entre procesos (IPC) puede dividirse en dos tipos principales: **directa** e **indirecta**.

En la **comunicación directa**, los procesos interactúan explícitamente entre sí. Ejemplos comunes incluyen **Sockets TCP/UDP**, que permiten la transmisión de datos en redes (TCP es confiable, UDP es rápido), **RPC (Remote Procedure Call)**, que facilita la ejecución de funciones en procesos remotos como si fueran locales, y **canales síncronos y asíncronos**, donde los procesos intercambian información directamente; los canales síncronos requieren sincronización simultánea, mientras que los asíncronos no.

La **comunicación indirecta** utiliza intermediarios para desacoplar procesos. Ejemplos incluyen **Linda**, que permite interacción a través de un espacio compartido de tuplas, **Publish-Subscribe**, donde productores y consumidores se comunican mediante eventos y suscripciones, y **colas de mensajes**, que almacenan mensajes hasta que el receptor esté listo, evitando que productor y consumidor dependan directamente uno del otro.
##### Requisitos comunicación en grupo
En la **comunicación en grupo**, se establecen ciertos requisitos clave para garantizar su funcionalidad y flexibilidad:
1. **Identificación por dirección IP**: Cada grupo tiene asignada una dirección IP específica que permite identificarlo de manera única en la red.
2. **Tamaño variable**: Los grupos no tienen un tamaño fijo, permitiendo que el número de miembros pueda aumentar o disminuir según sea necesario.
3. **Distribución geográfica**: Los miembros de un grupo pueden estar ubicados en cualquier lugar de Internet, sin restricciones geográficas.
4. **Entrada y salida dinámica**: Los miembros pueden unirse y abandonar el grupo en cualquier momento, asegurando flexibilidad en la participación.
5. **Desconocimiento inicial de miembros**: La lista de miembros del grupo no necesita conocerse de antemano, facilitando la creación y mantenimiento del grupo.
6. **Emisores externos**: No es obligatorio que los emisores de mensajes pertenezcan al grupo, permitiendo comunicación externa hacia el grupo.

##### Retos de la comunicación en grupo
Los **retos de la comunicación en grupo** abarcan diversos aspectos clave para garantizar su efectividad y confiabilidad:
1. **Vivacidad y tolerancia a fallos**: Es fundamental asegurar que los mensajes lleguen a los destinatarios, incluso en presencia de fallos en la red o en los nodos, garantizando la fiabilidad del sistema.
2. **Atomic Multicast**: Este desafío implica que un mensaje enviado a un grupo debe ser entregado a todos sus miembros o a ninguno, asegurando consistencia y evitando estados incoherentes entre los participantes.
3. **Orden de llegada de mensajes**: Se debe decidir si el orden en que los mensajes llegan a los miembros refleja el orden en que fueron emitidos. Esto puede ser crítico para mantener coherencia en sistemas distribuidos.
4. **Gestión de la pertenencia al grupo**: Es necesario manejar de manera eficiente la entrada y salida dinámica de miembros, asegurando al mismo tiempo el anonimato o la identidad según las necesidades del sistema.

##### Ordenación de mensajes
La **ordenación de mensajes** en sistemas distribuidos define cómo los mensajes se entregan y procesan, garantizando distintos niveles de consistencia y orden:
1. **Best-Effort Broadcast**: Los mensajes se envían al grupo de receptores, pero no se garantiza que todos los nodos los reciban, ni que los reciban en un orden específico. Es un enfoque básico y no garantiza fiabilidad en la entrega.
2. **Reliable Broadcast**: Asegura que si un mensaje es recibido por un proceso correcto (sin fallos), todos los procesos correctos también lo recibirán. Si ocurre un fallo, ningún proceso lo recibirá.
3. **FIFO Broadcast**: Garantiza que los mensajes enviados por un mismo emisor se entregan a los receptores en el mismo orden en que fueron enviados. Sin embargo, no asegura orden entre emisores distintos.
4. **Causal Broadcast**: Respeta las relaciones causales entre mensajes. Si un mensaje _m1_ precede causalmente a otro _m2_ (según el modelo de "sucede antes"), todos los receptores deben entregar _m1_ antes que _m2_.
5. **Total Order Broadcast**: Asegura que todos los mensajes se entregan a todos los procesos en el mismo orden, independientemente del orden en que fueron emitidos. Este nivel de ordenación es el más fuerte y útil en sistemas que requieren consistencia global.

##### Alternativas para la comunicación en grupo
**IP Multicast** es un mecanismo para la comunicación en grupo en redes IP. Permite enviar mensajes a múltiples destinatarios sin necesidad de enviar copias individuales, optimizando el uso del ancho de banda y reduciendo la carga en el emisor.
- **Funcionamiento**: Cada grupo se identifica mediante una dirección IP multicast. Los emisores envían un mensaje a esa dirección, y los routers de la red lo replican solo cuando es necesario, entregándolo a los miembros del grupo.
- **Ventajas**: Eficiencia en el uso de la red y reducción de tráfico redundante.
- **Desafíos**: No siempre se garantiza fiabilidad, y no todos los nodos pueden retransmitir si ocurre un fallo.

**Network Overlay** construye redes virtuales sobre una red física subyacente para mejorar o personalizar la comunicación. Se utiliza para superar limitaciones del **IP Multicast** o añadir nuevas funcionalidades. Evolución de los enfoques:
1. **Punto a punto (Primer intento)**:
    - Directamente conecta emisores y receptores.
    - Problema: Si un nodo falla, sus mensajes no se retransmiten, reduciendo fiabilidad.
2. **Retransmisiones exhaustivas (Segundo intento)**:
    - Asegura que todos los nodos retransmitan mensajes.
    - Problema: Genera una sobrecarga extrema en la red, haciéndolo ineficiente.
3. **Gossiping (Tercer intento)**:
    - Los mensajes se propagan de forma probabilística entre nodos, similar al "boca a boca".
    - Ventajas: Escalable y tolerante a fallos, pero puede haber retrasos en la entrega.

### Consistencia y transacciones distribuidas
![[Pasted image 20250112234018.png]]
##### Transacción Distribuida
- **Definición**: Una transacción distribuida es una secuencia de operaciones que involucra múltiples servidores en un sistema distribuido. Estas operaciones se coordinan de manera que todas se ejecuten correctamente como una unidad o ninguna de ellas se ejecute, garantizando consistencia en el sistema.
- **Características Principales**:
    - **Atomicidad**: Todas las operaciones de la transacción se completan, o ninguna lo hace. Esto asegura que el sistema no quede en un estado inconsistente.
    - **Coordinación entre servidores**: Los servidores deben trabajar juntos para garantizar que la transacción se ejecute de manera íntegra.
    - **Consistencia**: Al final de la transacción, el sistema debe permanecer en un estado coherente.
**Conclusión**:  
El propósito principal de las transacciones distribuidas es garantizar que las operaciones en sistemas distribuidos mantengan propiedades como atomicidad y consistencia, incluso en escenarios de fallo o concurrencia.

##### Consenso vs Transacción (Atomic Commit)
1. **Diferencia 1**:
    - **Consenso**: Se enfoca en que uno o más nodos propongan un valor y que el sistema llegue a un acuerdo sobre un único valor entre los propuestos. No todos los nodos necesitan participar directamente en la propuesta.
    - **Atomic Commit**: Es un mecanismo específico para transacciones. Aquí, todos los nodos involucrados deben votar si están de acuerdo en **commit** o si prefieren **abort**. Se requiere una votación explícita de cada nodo.
2. **Diferencia 2**:
    - **Consenso**: El sistema decide sobre uno de los valores propuestos, asegurando que todos los nodos correctos acuerden el mismo valor final.
    - **Atomic Commit**: El resultado depende de un voto unánime. Si todos votan **commit**, la transacción se ejecuta; si al menos un nodo vota **abort**, la transacción no se realiza.
3. **Diferencia 3**:
    - **Consenso**: Es tolerante a fallos siempre que exista un quórum suficiente (es decir, la mayoría de nodos operativos para tomar decisiones). Esto permite que el sistema continúe funcionando incluso si algunos nodos fallan.
    - **Atomic Commit**: Es más restrictivo. Si algún nodo falla o no responde, la transacción se aborta para garantizar consistencia y evitar estados inconsistentes en el sistema.

Mientras que el **consenso** está diseñado para alcanzar un acuerdo sobre un valor único entre nodos, la **transacción distribuida** mediante atomic commit se centra en garantizar que una operación compuesta (transacción) se ejecute completamente o no se ejecute en absoluto, sacrificando tolerancia a fallos para mantener consistencia.

##### Propiedades ACID
Las transacciones en un solo servidor se rigen por las **propiedades ACID**, que garantizan la fiabilidad y consistencia en el manejo de datos. Estas propiedades son fundamentales en sistemas de bases de datos y aseguran que las transacciones se ejecuten correctamente incluso en presencia de fallos.
1. **Atómica**: Una transacción se considera una unidad indivisible de trabajo. Esto significa que, o se ejecuta completamente (todos los cambios se aplican), o no se ejecuta en absoluto (se revierten todos los cambios realizados). Esto asegura que no queden operaciones intermedias en caso de fallo.
2. **Consistente**: Antes y después de una transacción, el sistema debe estar en un estado consistente. Esto implica que todas las reglas de integridad y restricciones definidas en el sistema se respetan durante la ejecución de la transacción.
3. **Isolation (Aislamiento)**: Cuando varias transacciones se ejecutan de manera concurrente, cada una debe ejecutarse como si fuera la única en el sistema. Esto evita condiciones de carrera y garantiza que el resultado final sea el mismo que si las transacciones se ejecutaran secuencialmente.
4. **Durabilidad**: Una vez que una transacción ha sido confirmada, todos sus efectos se registran permanentemente en el almacenamiento. Incluso si ocurre un fallo en el sistema, los cambios realizados por la transacción no se perderán.
Las propiedades ACID son esenciales para mantener la fiabilidad, consistencia y robustez en sistemas de bases de datos que operan en un solo servidor. Estas propiedades aseguran que las transacciones sean seguras y predecibles, incluso en situaciones de concurrencia o fallos inesperados.

##### Equivalencia serial frente operaciones conflictivas

**Entrelazado equivalente serial**:  
Un entrelazado de dos transacciones V y W es un equivalente serial si el resultado de ejecutar ambas transacciones con ese entrelazado es idéntico al de ejecutarlas de forma secuencial, es decir, primero V y luego W, o viceversa. Esto significa que el orden de las operaciones de las transacciones, aunque se entrelacen, no afecta el estado final del sistema siempre y cuando se preserve la equivalencia serial. Este concepto es clave para garantizar la **propiedad de aislamiento** en los sistemas que permiten la concurrencia de transacciones.

**Operaciones conflictivas**:  
Dos operaciones op1 y op2 son conflictivas si el resultado final de su ejecución depende del orden en que se llevan a cabo. En términos de bases de datos, esto ocurre generalmente cuando las operaciones afectan los mismos datos y al menos una de ellas es de escritura. Por ejemplo:
- **Lectura y escritura sobre el mismo dato**: Si op1 lee un dato que op2 actualiza, el orden afecta el resultado.
- **Escritura y escritura sobre el mismo dato**: Si ambas operaciones intentan escribir valores diferentes, el orden determina qué valor queda finalmente.

El concepto de entrelazado equivalente serial garantiza la consistencia en sistemas con transacciones concurrentes, asegurando resultados equivalentes a los de ejecuciones secuenciales. Las operaciones conflictivas, por otro lado, deben gestionarse adecuadamente (e.g., bloqueos) para evitar inconsistencias en los datos debido a la dependencia en el orden de ejecución.

##### Two-phase commit
![[Pasted image 20250112235028.png]]

El protocolo **Two-Phase Commit** es una solución clásica para garantizar la atomicidad de una transacción distribuida en sistemas que involucran múltiples nodos o servidores (como A y B en el diagrama). Este protocolo asegura que todos los participantes de la transacción acuerden un resultado común: **commit** (finalizar exitosamente) o **abort** (deshacer los cambios).
1. **Fase de preparación (Prepare Phase):**
    - El coordinador (en el centro del diagrama) envía un mensaje de _prepare_ a todos los nodos participantes (A y B).
    - Cada nodo ejecuta la transacción localmente hasta el punto en que esté listo para confirmarla.
    - Si el nodo está listo, responde con un mensaje de _ok_ al coordinador. Si no, responde con un _abort_.
2. **Fase de compromiso (Commit Phase):**
    - Si todos los nodos responden con _ok_, el coordinador envía un mensaje de _commit_ a todos los participantes, indicando que deben finalizar la transacción.
    - Si algún nodo responde con _abort_ (o no responde), el coordinador envía un mensaje de _abort_ a todos los nodos, anulando la transacción.

 **Características clave:**
- **Atomicidad:** Todos los nodos completan la transacción o ninguno lo hace.
- **Consistencia:** La decisión es consistente en todos los participantes.
- **Coordinación centralizada:** El coordinador toma la decisión final.

 **Conclusión:**
El protocolo **2PC** garantiza la coherencia y atomicidad en transacciones distribuidas. Sin embargo, tiene desventajas como la latencia y la dependencia del coordinador. Un fallo del coordinador puede llevar al bloqueo del sistema, lo que ha motivado la creación de protocolos más avanzados, como el **Three-Phase Commit (3PC)**.

### Middleware
El **middleware** es un software intermedio que facilita la interacción entre diferentes aplicaciones, servicios o sistemas. Actúa como un puente que permite que aplicaciones que pueden estar escritas en distintos lenguajes de programación o ejecutándose en plataformas heterogéneas trabajen juntas de manera eficiente. Su función principal es manejar la comunicación, la interoperabilidad y la gestión de datos entre sistemas distribuidos.

Entre sus características más importantes se encuentra la **transparencia**, ya que oculta la complejidad de la red, permitiendo que las aplicaciones interactúen como si estuvieran en el mismo entorno. Además, proporciona **escalabilidad**, lo que permite gestionar grandes volúmenes de datos y usuarios, así como **seguridad** en la transferencia de datos entre aplicaciones.

El middleware tiene múltiples áreas de uso, como los sistemas distribuidos, donde coordina componentes distribuidos en diferentes ubicaciones; aplicaciones web, donde gestiona las solicitudes entre clientes y servidores; y microservicios, donde asegura una comunicación eficiente entre servicios independientes. Ejemplos comunes incluyen sistemas de mensajería como **RabbitMQ** o **Apache Kafka**, middleware de bases de datos y plataformas de comunicación como **RPC** o **CORBA**.

En conclusión, el middleware es una pieza clave en sistemas modernos y distribuidos, ya que permite integrar aplicaciones y servicios de manera efectiva, mejorando la interoperabilidad, la flexibilidad y la eficiencia en la gestión de sistemas complejos.
### Raft
La **Log Matching Property** en el contexto del algoritmo Raft establece que: **si dos entradas de registro en diferentes servidores tienen el mismo índice y mandato, entonces almacenan la misma operación, y todos los registros anteriores también coinciden de manera idéntica en ambos servidores.** Esta propiedad garantiza la coherencia entre los registros de los diferentes nodos en el clúster, lo que es fundamental para asegurar que las decisiones de consenso sean válidas y replicadas correctamente.
### Principales propiedades de Raft:
1. **Seguridad**: Raft garantiza que ninguna entrada de registro confirmada puede sobrescribirse o eliminarse. Una entrada confirmada implica que ha sido replicada en la mayoría de los nodos y, por tanto, será parte permanente del estado del sistema.
2. **Elección de líder**: En cualquier momento, como mucho, puede haber un solo líder válido en el clúster. El líder se encarga de recibir todas las solicitudes de los clientes y replicarlas en los seguidores, asegurando un flujo ordenado de las operaciones.
3. **Consenso basado en mayorías**: Raft toma decisiones únicamente si la mayoría de los nodos del clúster las aprueba. Esto garantiza tolerancia a fallos, ya que el sistema puede seguir funcionando incluso si algunos nodos fallan.
	1. Mayoría = N/2 redondeo hacia abajo + 1
4. **Durabilidad**: Una vez que una operación ha sido confirmada y aplicada en la mayoría de los nodos, su efecto persiste incluso si algunos de esos nodos fallan. Esto se logra replicando la información en múltiples nodos.
5. **División en términos y mandatos**: El tiempo en Raft está dividido en términos. Cada término comienza con una elección para seleccionar al líder, y este mandato regula el periodo en el que el líder puede proponer entradas al registro. Esto organiza las operaciones y asegura que solo un líder legítimo esté a cargo en cada momento.
6. **Consistencia en el registro**: Gracias a la **Log Matching Property**, Raft garantiza que el registro de operaciones sea consistente entre los nodos, incluso en situaciones de fallo del líder o de los seguidores.

El algoritmo Raft se centra en garantizar la coherencia, seguridad y disponibilidad del sistema distribuido mediante propiedades bien definidas como la **Log Matching Property**, consenso por mayorías y mecanismos de elección de líderes. Esto lo convierte en uno de los algoritmos más robustos y comprensibles para la implementación de sistemas distribuidos consistentes.