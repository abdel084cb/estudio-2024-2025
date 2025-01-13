![[Pasted image 20250112200551.png]]
![[Pasted image 20250112200604.png]]
### Ejercicio 2
##### a)
![[Pasted image 20250112200953.png]]
##### b)
![[Pasted image 20250112201515.png]]
##### c)
Con los relojes de lamport no podemos encontrar eventos concurrentes. Si usamos las estampillas vectoriales podemos encontrar unos cuantos debido a la propiedad v1 || v2 = not v1 <= v2 and not v2 <= v1
h concurrente
i concurrente 
k concurrente
g concurrente
l concurrente
m concurrente
n concurrente
o concurrente
q concurrente
r concurrente
s concurrente
##### d)
No, **los eventos concurrentes encontrados para el evento d no son los mismos si se consideran las estampillas escalares y las vectoriales**. Esto se debe a las diferencias fundamentales entre estos dos tipos de estampillas temporales:
1. **Estampillas escalares (Lamport)**:
    - Estas estampillas proporcionan un **orden total** de los eventos, pero no pueden determinar si dos eventos son concurrentes.
    - Si dos eventos no tienen una relación de "causalidad" directa, las estampillas escalares aún imponen un orden arbitrario entre ellos debido al uso de un identificador de proceso como criterio de desempate.
2. **Estampillas vectoriales**:
    - Estas permiten determinar si dos eventos son concurrentes, ya que pueden detectar relaciones causales parciales entre eventos.
    - Dos eventos son concurrentes si sus vectores no son comparables (es decir, no se cumple que uno sea menor o igual que el otro).
En este caso:
- Con **estampillas escalares**, cualquier evento tendrá un orden (directo o por desempate), por lo que no se identificarán eventos concurrentes con d.
- Con **estampillas vectoriales**, se pueden identificar los eventos concurrentes con d porque permiten analizar la relación de causalidad parcial.
Por lo tanto, **las estampillas vectoriales identifican eventos concurrentes que no pueden ser determinados con las estampillas escalares**.

![[Pasted image 20250112203301.png]]
### Ejercicio 3
##### 3.1
Falso, Kerberos no utiliza certificados digitales ni criptografía de clave pública/asimétrica, y no depende de una infraestructura de clave pública (PKI). En cambio, Kerberos emplea un Key Distribution Center (KDC) que distribuye claves secretas simétricas entre los usuarios y los servicios. Además, utiliza **Ticket Granting Tickets (TGT)** para autenticar usuarios y permitirles obtener **Service Tickets (TS)** para acceder a servicios específicos en el sistema.
##### 3.2
Verdadero, Kubernetes utiliza **etcd**, un almacén de datos distribuido tolerante a fallos, para almacenar la configuración del clúster.
Características de etcd:
1. **Tolerancia a fallos:**
    - Al ser un sistema distribuido basado en el algoritmo de consenso **Raft**, puede manejar la pérdida de nodos mientras mantenga un quórum de nodos disponibles.
2. **Consistencia secuencial:**
    - etcd garantiza una **consistencia secuencial fuerte**, lo que significa que las operaciones de lectura y escritura siempre reflejan el orden en que se realizaron las operaciones.
3. **Uso en Kubernetes:**
    - Toda la configuración del clúster de Kubernetes, como los recursos (Pods, Deployments, Services, etc.), se almacena en **etcd**.
    - Kubernetes consulta y actualiza etcd para coordinar las operaciones dentro del clúster.
En resumen, etcd cumple exactamente con lo que se describe en el enunciado: es un almacén de datos tolerante a fallos que proporciona consistencia secuencial frente a fallos, siendo un componente esencial en Kubernetes.
##### 3.3
Falso, Raft no utiliza transacciones distribuidas para comprometer sus entradas en el registro. En lugar de eso:
- **Raft utiliza un algoritmo de consenso** diseñado específicamente para coordinar el compromiso de entradas entre los nodos del clúster.
- Este proceso se basa en el quórum (mayoría de nodos) y las reglas de replicación y liderazgo. Cuando un líder recibe una entrada, la replica en la mayoría de los seguidores antes de comprometerla oficialmente.
- Las transacciones distribuidas, como las implementadas en algoritmos de tipo **2PC (Two-Phase Commit)**, son diferentes porque requieren la participación y respuesta de todos los nodos, y no están diseñadas para tolerar fallos de la misma manera que Raft.
En resumen, Raft no necesita implementar transacciones distribuidas porque su diseño ya está optimizado para consenso y compromiso en sistemas distribuidos.
##### 3.4
Por ejemplo Raft **sí sería suficiente** para añadir tolerancia a fallos a un servidor Kerberos, siempre que se implemente correctamente, ya que Raft incluye tanto un mecanismo de **elección de líder** como un protocolo de **replicación de logs** consistente que garantiza:
1. **Replicación consistente:** Raft asegura que todas las operaciones (como la emisión de tickets en el caso de Kerberos) se registren de forma ordenada y consistente en todos los nodos que forman parte del clúster.
2. **Sincronización de datos:** El líder en Raft se encarga de propagar todas las entradas del log a los seguidores, garantizando que estén sincronizados.
3. **Manejo de particiones:** Raft tolera fallos de nodos y particiones de red, siempre que exista un quórum (mayoría) operativo, lo cual es suficiente para la operación consistente del sistema.
4. **Elección de líder:** Cuando el líder actual falla o se desconecta, Raft automáticamente elige un nuevo líder mediante su mecanismo de elección, asegurando que las operaciones puedan continuar.
Entonces, ¿por qué es más complejo en la práctica?
Aunque Raft proporciona todas las funcionalidades necesarias para implementar tolerancia a fallos en Kerberos, hay consideraciones adicionales:
- **Complejidad de integración:** Adaptar Kerberos para utilizar Raft no es trivial, ya que requiere modificar cómo Kerberos almacena y replica sus datos (clave secretas, tickets, etc.).
- **Compatibilidad:** Es necesario garantizar que los clientes de Kerberos puedan comunicarse con el sistema replicado sin interrupciones, incluso durante fallos o cambios de liderazgo.
- **Gestión de claves:** La seguridad de Kerberos depende de mantener las claves secretas a salvo. Raft debe garantizar que estas claves se repliquen de forma segura y no queden expuestas.
**Conclusión:** Sí, Raft sería suficiente como base para añadir tolerancia a fallos al servidor Kerberos. Sin embargo, su integración debe incluir mecanismos adicionales para asegurar la compatibilidad, seguridad y rendimiento del sistema distribuido en su conjunto.
##### 3.5
Falso, En Kubernetes, las IPs de los Pods no son prefijadas ni estáticas. Cada vez que se crea un Pod, se le asigna una IP única dentro del clúster de forma dinámica. Esta IP es válida únicamente mientras el Pod esté vivo. Si el Pod se elimina y se recrea, recibirá una nueva IP. Por esta razón, se utilizan nombres DNS asignados por servicios (Services) para proporcionar acceso estable a los Pods, independientemente de los cambios en sus IPs.

Sin un mecanismo como los Services, no sería posible garantizar una dirección fija para comunicarse con los Pods.
##### 3.6
Falso, Una transacción distribuida **no se soluciona únicamente añadiendo un algoritmo de elección de líder**. La elección de líder es un componente que puede ser útil en sistemas de consenso (como Raft o Paxos) para coordinar decisiones, pero no aborda por sí sola todos los aspectos necesarios para garantizar la atomicidad y consistencia de las transacciones distribuidas.
En el contexto de transacciones distribuidas:
1. **La elección de líder**: Puede ayudar a coordinar quién toma decisiones durante un fallo, pero no garantiza que todas las réplicas tengan la información necesaria para comprometer o abortar la transacción.
2. **Protocolos específicos**: Las transacciones distribuidas suelen usar protocolos como **2PC (Two-Phase Commit)** o **3PC (Three-Phase Commit)**, que manejan el compromiso de todas las partes involucradas.
3. **Fallos complejos**: En una transacción distribuida, un fallo del coordinador puede dejar en un estado inconsistente a los participantes. Resolver esto requiere un protocolo que permita a los nodos restantes alcanzar consenso sobre el estado de la transacción.
Por lo tanto, simplemente implementar un algoritmo de elección de líder no es suficiente. Es necesario un protocolo que garantice la consistencia, atomicidad y tolerancia a fallos, lo cual va más allá de la simple elección de un nuevo líder.
##### 3.7
Falso, TLS utiliza criptografía asimétrica durante el proceso de handshake para intercambiar o negociar una clave simétrica.
Explicación:
- Durante el handshake de TLS, los participantes (cliente y servidor) intercambian información de manera segura utilizando criptografía asimétrica (claves públicas y privadas).
- Una vez establecido el canal seguro, acuerdan una clave simétrica compartida que será utilizada para cifrar los datos durante la sesión.
- Esto es más eficiente porque la criptografía simétrica es mucho más rápida que la asimétrica para el cifrado de grandes cantidades de datos.
Este intercambio de claves simétricas garantiza la confidencialidad, integridad y eficiencia de la comunicación posterior.

Si interpretamos "durante la conexión" como el proceso **completo** (incluyendo el handshake y la comunicación posterior), entonces la afirmación es **verdadera**. Pero si restringimos "durante la conexión" al momento exacto del handshake, sería **falsa** porque ahí se usa criptografía asimétrica.

La ambigüedad radica en cómo se entiende el término "conexión". En contexto técnico más amplio, incluiría tanto el establecimiento como la comunicación.
##### 3.8
Falso. Kubernetes no utiliza **Kerberos** para proveer servicios de seguridad distribuidos. Kubernetes implementa sus propias soluciones para la seguridad, como **TLS** para las comunicaciones seguras y **ServiceAccounts** junto con tokens para la autenticación y autorización dentro del clúster. Además, utiliza **RBAC (Role-Based Access Control)** para gestionar los permisos de acceso. Kerberos, por otro lado, es un protocolo de autenticación basado en clave simétrica que no forma parte de la arquitectura de Kubernetes.
##### 3.9
Falso En Raft no existen dos algoritmos de consenso separados. Raft utiliza un único algoritmo de consenso que abarca tanto el proceso de elección de un líder como la replicación y compromiso de entradas en el registro. Estas dos funcionalidades (elección de líder y compromiso de entradas) están integradas en el mismo protocolo.
Explicación:
1. Elección de líder: Se realiza cuando un líder falla o no se reciben latidos a tiempo. Los nodos inician una votación utilizando el mismo mecanismo de consenso para decidir quién será el nuevo líder.
2. Compromiso de entradas: El líder utiliza el consenso para garantizar que las entradas en el registro sean replicadas en la mayoría de los nodos antes de considerarlas comprometidas.
Por tanto, Raft implementa un solo algoritmo de consenso que maneja ambos aspectos, no algoritmos separados.
##### 3.10
Falso. En el algoritmo del matón, cuando ocurre una partición de red, se pueden elegir líderes independientes en cada partición de la red. Esto sucede porque los procesos en cada partición al no poder comunicarse entre sí, cada partición sigue el protocolo del algoritmo y termina eligiendo un líder dentro de su propio subconjunto de nodos disponibles.

![[Pasted image 20250112213011.png]]

### Ejercicio 4
##### 4.1
 **Ventajas de la virtualización nativa:**
1. **Aislamiento completo:** Cada máquina virtual (VM) incluye su propio sistema operativo, lo que proporciona un aislamiento total entre las aplicaciones. Esto es útil para ejecutar sistemas operativos completamente diferentes en el mismo hardware.
2. **Seguridad:** Al estar más aisladas (gracias al hipervisor y al sistema operativo completo), las VMs ofrecen una mayor protección frente a ataques, ya que comprometer una VM no afecta directamente a otras.
3. **Compatibilidad:** Permiten ejecutar aplicaciones que requieren entornos muy específicos o sistemas operativos antiguos, ya que simulan hardware completo.
**Desventajas de la virtualización nativa:**
1. **Consumo de recursos:** Las VMs son pesadas, ya que cada una incluye un sistema operativo completo, lo que requiere más CPU, RAM y almacenamiento.
2. **Lentitud:** El arranque y ejecución son más lentos debido a la sobrecarga del hipervisor y el sistema operativo en cada VM.
3. **Escalabilidad limitada:** Escalar con máquinas virtuales es menos eficiente en términos de recursos, ya que cada instancia consume una gran cantidad de memoria y CPU.

 **Ventajas de los contenedores:**
1. **Ligereza:** Los contenedores comparten el mismo kernel del sistema operativo anfitrión, lo que los hace más ligeros en términos de memoria y almacenamiento.
2. **Velocidad:** Se inician y detienen rápidamente porque no necesitan cargar un sistema operativo completo.
3. **Escalabilidad:** Son ideales para sistemas distribuidos y microservicios, ya que se pueden replicar y escalar fácilmente.
4. **Consistencia:** Facilitan el despliegue de aplicaciones en diferentes entornos, garantizando que se ejecuten igual en desarrollo, pruebas y producción.

 **Desventajas de los contenedores:**
1. **Menor aislamiento:** Comparten el mismo kernel del sistema operativo anfitrión, lo que puede representar un riesgo de seguridad si un contenedor se ve comprometido.
2. **Compatibilidad limitada:** No permiten ejecutar sistemas operativos completamente diferentes, ya que dependen del kernel del anfitrión.
3. **Complejidad operativa:** Requieren herramientas adicionales (como Kubernetes) para gestionar grandes despliegues y garantizar tolerancia a fallos.

En resumen, la elección entre virtualización nativa y contenedores depende de las necesidades específicas: la virtualización nativa ofrece mayor aislamiento y compatibilidad, mientras que los contenedores son más ligeros y eficientes para aplicaciones modernas basadas en microservicios.


##### 4.2
 **Elementos más importantes de Kubernetes y su función según tus apuntes**
1. **etcd**:
    - Es el almacén de datos distribuido donde Kubernetes guarda toda su configuración.
    - Proporciona tolerancia a fallos y consistencia secuencial usando el algoritmo de consenso **Raft**.
2. **Pod**:
    - Unidad básica de ejecución en Kubernetes, que puede contener uno o más contenedores.
    - Posee una IP única y es la unidad de escalado dentro del clúster.
3. **Nodo**:
    - Cada máquina (física o virtual) que ejecuta los pods. Contiene el runtime de contenedores y el **kubelet**.
4. **Servicio**:
    - Actúa como un alias estable para acceder a un grupo de pods, proporcionando balanceo de carga y direcciones IP/DNS fijas.
5. **Ingress**:
    - Gestiona accesos externos al clúster, permitiendo exponer servicios a través de rutas HTTP/HTTPS.
    - Útil para gestionar múltiples aplicaciones desde un único punto de entrada.
6. **Controladores**:
    - Supervisan el estado del clúster y aseguran que los recursos cumplan el estado deseado. Ejemplos:
		- **Job**:
		    - Ejecuta tareas específicas y garantiza que un número definido de pods termine exitosamente.
		    - Los pods se reinician si fallan o son eliminados.
		    - Ejemplo: **CronJob**, para tareas programadas.
		- **DaemonSet**:
		    - Asegura que cada nodo (o un subconjunto de nodos) ejecute una copia específica de un pod.
		    - Ideal para tareas administrativas como monitoreo, recolección de logs, o configuraciones de red.
		    - Los pods se reinician automáticamente si fallan o son eliminados.
		- **ReplicaSet**:
		    - Mantiene un número constante de pods en ejecución.
		    - Es la base de otros controladores como **Deployments**.
		- **Deployment**:
		    - Gestiona la creación, actualización y escalado de aplicaciones.
		    - Ofrece actualizaciones controladas, rollbacks y escalado automático.
		    - Se construye sobre **ReplicaSets**, pero añade más funcionalidades avanzadas.
		- **StatefulSet**:
		    - Diseñado específicamente para aplicaciones con estado.
		    - Proporciona:
		        - Nombres DNS estables.
		        - Orden en la creación y eliminación de pods.
		        - Almacenamiento persistente mediante **PersistentVolumeClaims**.
		    - Ideal para bases de datos, sistemas de mensajería, y otras aplicaciones distribuidas
1. **Namespaces**:
    - Dividen el clúster en secciones lógicas para organizar recursos, facilitando la gestión de múltiples proyectos o entornos.
2. **Labels**:
    - Permiten clasificar y seleccionar recursos mediante pares clave-valor.
 **Relaciones entre los elementos según tus apuntes**
- Los **pods** ejecutados en los **nodos** son gestionados por controladores como **ReplicaSets** y **Deployments**.
- Los **servicios** actúan como puntos de acceso estables para los pods, mientras que **Ingress** permite exponerlos al exterior.
- **etcd** almacena toda la configuración y asegura la consistencia del clúster.
- **Namespaces** y **labels** proporcionan organización y segmentación lógica dentro del clúster.
Este resumen incorpora tus apuntes detallados, destacando las funciones y las relaciones entre los elementos más importantes en Kubernetes.

##### 4.3
1. **Tipo de mensaje**:
    - Los latidos son mensajes enviados periódicamente por el líder a los seguidores. Estos mensajes confirman la presencia del líder y mantienen vivo su liderazgo.
2. **Gestión**:
    - Si un seguidor no recibe un latido dentro de un período de tiempo determinado (timeout), asume que el líder ha fallado.
    - Entonces, ese seguidor inicia un proceso de **elección de nuevo líder**, convirtiéndose en candidato y enviando solicitudes de voto (RequestVote) a otros nodos.
3. **Implicaciones de tiempo**:
    - El intervalo de latidos y los timeouts deben estar configurados cuidadosamente:
        - **Demasiado cortos**: Incrementan el tráfico en la red y pueden causar elecciones innecesarias debido a retrasos.
        - **Demasiado largos**: Pueden retrasar la detección de fallos, impactando la disponibilidad del sistema.
    - La configuración típica usa latidos cada pocos milisegundos o cientos de milisegundos, y un timeout varias veces superior al intervalo de latidos para evitar elecciones prematuras.
En resumen, los latidos son esenciales en Raft para mantener la sincronización entre nodos y detectar fallos de manera eficiente.

##### 4.4
1. **Qué ocurre si no se consigue elegir un líder en un mandato de Raft?**
    - Raft continuará intentando elegir un líder en el siguiente mandato. Esto ocurre porque los nodos reiniciarán su **timeout de elección** y comenzarán un nuevo proceso de elección enviando solicitudes de voto (RequestVote). Este ciclo continúa hasta que se alcanza un quórum y se elige un líder.
    - Sin un líder, no se pueden procesar nuevas entradas en el registro, lo que puede afectar la disponibilidad del sistema.
2. **¿Qué ocurre si en un mandato de Raft se comprometen entradas de mandatos anteriores, pero no se consigue comprometer ninguna entrada de ese mismo mandato?**
    - **No se puede comprometer una entrada de un mandato anterior sin comprometer una del mandato actual.**
    - Si no se consigue comprometer ninguna entrada del mandato actual, significa que no hay actividad nueva en el sistema, por lo que las previas tampoco podrán comprometerse.