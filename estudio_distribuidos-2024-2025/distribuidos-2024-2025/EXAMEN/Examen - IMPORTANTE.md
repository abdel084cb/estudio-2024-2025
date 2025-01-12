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


### Algoritmo del matón

* **Características:**
	* Cada proceso conoce el PID de los demás procesos, sabe cuales son mayores
	* Interacción síncrona gestionada por timeouts
	* Red sin fallos
	* Inicia elección si el líder no responde
	* Procesos con mayor PID intimidan a los de menor para expulsarlos de la elección quedando al final un único proceso.
	* Cuando un proceso fallido re-arranca, inicia una elección automáticamente

* **Algoritmo:**
	* 4 tipos de msg:
		* Elección: anuncia elección
		* Respuesta: respuesta a elección
		* Coordinador: anuncia líder elegido
		* Latido: msg que se envía al coordinador, si contesta está vivo
	* Proceso empieza elección cuando:
		* ha expirado el timeout, es decir, el coordinador no responde
		* recibe Elección
			* Contesta si tiene el PID mayor (que lo tendrá, mas bien sería si sigue vivo) y vuelve a lanzar Elección a todos los procesos mayores.
			* Si ya estaba en elección contesta si procede pero no vuelve a lanzar Elección.
	* Proceso empieza elección
		* Envía Elección a todos los procesos con PID mas alto
		* Si no se recibe Respuesta se convierte en líder y manda el msg Coordinador a todos los procesos vivos
		* Si llega Respuesta, entonces espera Coordinador durante un tiempo (timeout)
		* Si no llega el msg Coordinador entonces reinicia la Elección
		* Si un proceso sabe que su PID es el mas alto entonces puede responder inmediatamente con Coordinador
		* Se deben ajustar los tiempos de expiración
			* `(2*RTT + Tprocesado)`
		* Si hay error durante la detección de fallo, la elección seguirá adelante.
![[Pasted image 20250111165642.png]]
![[Pasted image 20250111165709.png]]

- **RTT** significa **Round-Trip Time** o tiempo de ida y vuelta. Es el tiempo que tarda un mensaje en viajar desde un emisor hasta un receptor y que la respuesta de ese receptor vuelva al emisor.

- **Mejor caso (1 RTT, N-1 mensajes)**:
    - Ocurre cuando el proceso con **mayor PID detecta directamente la falla** del líder.
    - Este proceso se autoproclama líder y envía un único mensaje de **Coordinador** a los demás procesos.
- **Peor caso (N-1 RTTs, O(N²) mensajes)**:
    - Sucede si el proceso con **menor PID inicia la elección**.
    - Este proceso debe enviar mensajes de **Elección** a procesos con mayor PID, quienes a su vez continúan propagando la elección hasta llegar al proceso con el mayor PID. Luego, este último envía mensajes de **Coordinador** a todos los demás

![[Pasted image 20250111175052.png]]

- **Timeout para detectar la falla del líder**:
    - Cada proceso monitorea al líder actual enviándole mensajes periódicos de "latido" (heartbeat) y espera su respuesta.
    - Si el proceso no recibe respuesta dentro de un tiempo definido, el timeout expira y el proceso asume que el líder ha fallado, iniciando una elección.
- **Timeout para esperar respuestas durante la elección**:
    - Cuando un proceso inicia una elección, envía mensajes de Elección a los procesos con mayor PID y espera respuestas (mensajes de Respuesta o Coordinador).
    - Si no recibe ninguna respuesta dentro del tiempo definido, el proceso asume que los procesos con mayor PID han fallado y se declara líder enviando un mensaje de Coordinador a todos los procesos vivos.
- Se ajustan con `2*RTT + Tprocesado`

### Kubernetes

* **Pod**
	* Unidad de ejecución
		* Ejecuta una instancia de una aplicación
	* Puede contener 1 ó múltiples contenedores
		* Típicamente "misma máquina (hardware, CPU, red)"
	* Unidad de escalado
	* Su propia IP única en el clúster
		* Se comparte entre los contenedores
	* Los Pods de un clúster se pueden comunicar entre ellos sin NAT
	* Son efímeros

* **Nodos**
	* ![[Pasted image 20250111203016.png]]
	* ![[Pasted image 20250111203032.png]]

* **Servicio**
	* Expone un nombre, un puerto y una IP estable para un grupo de Pods. Un **servicio** en Kubernetes actúa como un **alias estable** para un conjunto de pods. Si un pod encargado de una tarea tiene una IP específica y luego muere o se reinicia con otra IP diferente, el servicio sigue proporcionando la misma **IP fija** (o nombre DNS) para acceder a esos pods. Se provee a los Pods mediante DNS o una variable de entorno.
	* Un servicio te da una **dirección fija** para acceder a tus pods.
	* **Construido utilizando un selector sobre los labels de Pods**
	- Balancea la carga entre un grupo de Pods, redistribuye automáticamente el tráfico entre los pods.
	- Puede ser solo interno (dentro del clúster) o externo (visible fuera del clúster).
		- los **servicios internos** (ClusterIP) son los más comunes, mientras que los servicios externos (NodePort o LoadBalancer) son más específicos para exponer aplicaciones al mundo exterior.
	- Actúa como proxy entre los clientes y los Pods

* **Ingress**
	- **Service** es más técnico, funciona como una **IP o DNS interna** para conectar y balancear el tráfico entre pods de un clúster o exponer un único servicio al exterior. Es como una dirección IP fija dentro del sistema.
	- **Ingress** es más avanzado, se parece más a una **web pública** que permite gestionar múltiples rutas (como `/app1` y `/app2`), dominios, y conexiones HTTPS hacia varios servicios. Es como el "puente" entre el internet y los servicios internos del clúster
	- ![[Pasted image 20250111194737.png]]
	* Permite definir acceso de red desde internet a recursos de clúster
		* trabaja con balanceadores de carga
		* URL de una sola raíz
		* redes privadas de forma pública al exterior
		* permite TLS/SSL
		* ![[Pasted image 20250111200115.png]]

* **Controladores**
	* En Kubernetes, un controlador es un componente del sistema que se encarga de garantizar que el estado actual del clúster coincida con el estado deseado especificado por el usuario. Los controladores son responsables de monitorear continuamente los recursos del clúster y tomar acciones correctivas para mantener su estado esperado.
	* Un controlador actúa como un "vigilante" o "gerente" que supervisa y ajusta los recursos de Kubernetes para que funcionen de acuerdo a lo que el usuario definió en los archivos de configuración (YAML o JSON).
	* ![[Pasted image 20250111192038.png]]
		* **Estado deseado**: El usuario describe el estado deseado del clúster en un manifiesto (archivo de configuración).
		- **Monitoreo**: El controlador verifica continuamente el estado actual de los recursos en el clúster.
		- **Acción correctiva**: Si detecta que el estado actual no coincide con el deseado, toma las acciones necesarias para corregirlo.
	- **Tipos:**
		- **Job**
			- Dedicado a realizar y terminar tareas
				- Una vez terminada la tarea, el comportamiento depende de la configuración
					- Completed sin eliminar
						- Interesante para inspeccionar los pods
					- Limpieza después de terminar
					- CronJob
					- etc.
			- Crea Pods y asegura que un numero determinado de ellos termina con éxito
			- Se re arrancan Pods, si fallan o se suprimen
		- **Daemon Set**
			- Asegura que **cada nodo en un clúster (o algunos nodos seleccionados)** ejecuten una copia específica de un Pod. Es útil para tareas de soporte o administración que deben ejecutarse en todos los nodos, como recolectores de logs, monitoreo o almacenamiento.
			- Se re arrancan Pods, si fallan o se suprimen
		- **Replica Set**
			- Asegura de que un **número determinado de réplicas (Pods) estén siempre corriendo** en tu clúster. Si un Pod falla o se elimina, el ReplicaSet automáticamente crea un nuevo Pod para reemplazarlo y mantener la cantidad deseada.
		- **Deployment**
			- Forma más avanzada de gestionar tus aplicaciones. Básicamente, es como un "jefe" que se encarga de crear, actualizar y asegurarse de que tus aplicaciones (Pods) estén funcionando correctamente y en la cantidad que necesitas.
			- Se declara un estado de configuración a alcanzar a un determinado ritmo
			- **ReplicaSet** solo mantiene un número fijo de Pods funcionando.
			- **Deployment** es más completo porque, además de manejar los Pods (como lo hace el ReplicaSet), también te permite actualizar y gestionar tus aplicaciones de forma más avanzada.
			- Deployment utiliza ReplicaSets internamente para mantener un número fijo de Pods funcionando, pero añade características adicionales como:
				- Actualizaciones controladas (por ejemplo, realizar una actualización de versión de la aplicación de forma gradual).
				- Declarar un estado deseado que Kubernetes se encargará de alcanzar.
				- Recuperación automática ante fallos.
				- Posibilidad de realizar "rollbacks" (volver a un estado anterior si una actualización falla).
		- **StatefulSet**
			- Diseñado específicamente para gestionar aplicaciones **con estado**. A diferencia de los **Deployments** o **ReplicaSets**, que son ideales para aplicaciones **sin estado**, el **StatefulSet** se encarga de asegurar que los Pods mantengan una identidad única y persistente a lo largo del tiempo.
			- ![[Pasted image 20250111211258.png]]
		- **Services (No es un tipo de controlador pero trabaja con ellos)** 
			- ![[Pasted image 20250111211050.png]]
			- ![[Pasted image 20250111211101.png]]

- **Namespaces**
	- Los **namespaces** en Kubernetes son divisiones lógicas dentro del clúster que permiten organizar y aislar recursos (como Pods, servicios y configuraciones). Son útiles para separar entornos (producción, desarrollo, pruebas) o para gestionar múltiples equipos o proyectos dentro del mismo clúster, evitando conflictos entre nombres de recursos
- **Labels**
	- Los **labels** son pares clave-valor que se asignan a los recursos de Kubernetes (Pods, servicios, etc.) para clasificarlos y organizarlos. Permiten realizar selecciones y filtrados eficientes, facilitando la gestión de recursos agrupados según sus características, como roles, entornos o versiones.
### Certificados digitales
- **Autenticación y seguridad:**
    - Los certificados digitales son documentos electrónicos utilizados para garantizar la identidad de una persona, empresa o entidad en la red.
    - Permiten verificar que una entidad es quien dice ser y establecen un canal seguro para intercambiar información.
- **Criptografía asimétrica:**
    - Usa dos claves:
        - **Clave pública:** Compartida con cualquiera y contenida en el certificado.
        - **Clave privada:** Guardada de forma segura y nunca compartida.
    - Estas claves permiten cifrar y firmar mensajes de manera segura.
- **Contenido del certificado:**
    - Incluye información como:
        - **Clave pública** del titular (persona/empresa).
        - **Datos básicos** del titular (nombre, dirección, fecha de caducidad).
        - Una **firma digital** de una entidad certificadora (CA), que verifica la autenticidad del certificado.
- **Firma digital:**
    - Generada por una entidad certificadora confiable, que actúa como un "notario digital".
    - Garantiza que el certificado no ha sido alterado y es válido.
- **Técnica básica de autentificación del certificado**
	- Una firma digital es una manera de garantizar que los datos no han sido alterados y que provienen de una entidad confiable (en este caso, la CA o Autoridad Certificadora)
	- `firma_digital = cifrar( Hash(datos-certificado), Kpriv-CA)`
	- Para validar un certificado digital:
		- `A = Descrifrar(firma_digital, Kpub-CA)
		- `B = CalcularHash(datos-certificado)`
		- `A==B` Valida el certificado
	- `CA y Kpriv-CA comprometidas => anular certificados`
		- Todos los certificados firmados por esa CA se vuelven inseguros. Se podrían falsificar.
* Tienen **tiempo de vida limitado** para disminuir riesgos de capturas de la clave privada asociada
* Un certificado digital puede ser **revocado** por la Autoridad Certificadora (CA) antes de su fecha de expiración. Esto ocurre cuando se detecta algún problema de seguridad
	* Los sistemas que confían en certificados (por ejemplo, navegadores web) deben consultar periódicamente las CRLs para asegurarse de que los certificados que están validando no han sido revocados.
	* **Lista de Revocación de Certificados (CRL)**: Es un archivo generado y mantenido por la CA que contiene un listado de los certificados que han sido revocados y, por lo tanto, ya no son válidos.
### Distribución de claves públicas
* Kerberos almacena y distribuye claves secretas (las de sesión)
* **PKI (infraestructura de clave pública) para la distribución**
	* Vincula Kpub con identidades mediante certificados digitales: certificados digitales garantizan que una Kpub pertenece realmente a una persona o a una entidad.
	* Cada uno guarda su Kpriv
* **Modelos de PKIs:**
	- **Centros de distribución o Autoridades Certificadoras (CA):** Organismos que emiten y garantizan la validez de los certificados digitales.
	- **Venta de certificados:** Generalmente, las CAs venden estos certificados para validar identidades (ejemplo: empresas compran certificados SSL).
	- **Cadenas de confianza:** Esquema en el cual una autoridad certificadora de confianza respalda a otras entidades para garantizar la autenticidad de los certificados
		- Si una entidad A confía en una CA y esta CA certifica a una entidad B, entonces A puede confiar en B. Esto es lo que crea la "cadena".
		- ![[Pasted image 20250112012059.png]]
		- ![[Pasted image 20250112012546.png]]

### Protocolo SSL/TLS

### Kerberos

**Definición:** Kerberos es un protocolo de autenticación diseñado para sistemas distribuidos que permite a usuarios y servicios autenticarse de manera segura en una red, minimizando riesgos de ataques como la interceptación de contraseñas o la reinyección de datos (replay attacks).

 **Características Principales:**
1. **Autenticación centralizada:**
    - Los usuarios y servicios se autentican a través de un servidor central llamado **Centro de Distribución de Claves (KDC)**.
2. **Single Sign-On (SSO):**
    - Los usuarios solo necesitan autenticarse una vez por sesión para acceder a múltiples servicios en la red.
3. **Uso de cifrado simétrico:**
    - Diseñado originalmente en los años 1980 para reducir el coste computacional de los algoritmos de cifrado.
4. **Tickets de autenticación:**
    - Kerberos utiliza tickets no falsificables para autenticar a usuarios y servicios.
5. **Confianza en una tercera entidad:**
    - El KDC almacena y gestiona claves secretas duraderas asociadas a cada usuario o servicio.
6. **Resistencia a ataques de reinyección:**
    - Los tickets incluyen información de tiempo de creación y tiempo de vida limitado.

 **Componentes de Kerberos:**
1. **Key Distribution Center (KDC):**
    - Entidad central que gestiona las claves y tickets. Incluye:
        - **Authentication Server (AS):** Valida la identidad inicial del usuario.
        - **Ticket Granting Server (TGS):** Emite tickets de servicio (TS) basados en los tickets de autenticación.
2. **Tickets:**
    - **Ticket Granting Ticket (TGT):** Ticket inicial que permite solicitar otros tickets sin necesidad de volver a ingresar credenciales.
    - **Ticket de Servicio (TS):** Ticket específico para acceder a un servicio.
3. **Claves:**
    - Clave secreta duradera: Conocida solo por el KDC y el usuario/servicio.
    - Clave de sesión: Generada para una sesión específica, incluida en los tickets.

 **Funcionamiento del Protocolo:**
1. **Autenticación inicial:**
    - El usuario envía sus credenciales (clave maestra) cifradas al AS (servidor de autenticación del KDC).
    - El AS verifica las credenciales y devuelve un **TGT** cifrado con la clave secreta del usuario.
2. **Solicitar acceso a un servicio:**
    - El usuario utiliza el TGT para solicitar un ticket de servicio (TS) al TGS.
    - El TGS genera el TS y lo envía al usuario.
3. **Acceso al servicio:**
    - El usuario presenta el TS al servicio deseado.
    - El servicio verifica el ticket y establece la sesión.

 **Ventajas de Kerberos:**
- **Seguridad:**
    - Contraseñas nunca viajan en texto claro por la red.
    - Los tickets tienen una vida limitada para evitar abusos.
- **Eficiencia:**
    - Uso de cifrado simétrico para reducir la carga computacional.
- **Flexibilidad:**
    - Compatible con múltiples sistemas operativos (Unix, Windows, etc.).
- **Single Sign-On:**
    - Simplifica la autenticación en sistemas distribuidos.

 **Limitaciones:**
1. **Dependencia del KDC:**
    - Si el KDC falla, la autenticación en toda la red se ve afectada.
2. **Complejidad de implementación:**
    - La gestión de claves y tickets requiere una configuración cuidadosa.
3. **Cifrado simétrico:**
    - Aunque es eficiente, implica compartir claves secretas, lo cual puede ser un riesgo si no se protege adecuadamente.

### Consistencia

* **Replicación como técnica de escalabilidad**
	* Replicación puede mejorar las prestaciones
	* Mantener la consistencia puede suponer un coste enorme `=>` Relajar la consistencia
		* **Consistencia secuencial
			* ![[Pasted image 20250109222832.png]]
			* Lo importante es que **todos los procesos ven las mismas operaciones en el mismo orden**:
			- En el primer caso, el orden observado por **P3** y **P4** es: `b` primero, luego `a`.
			- Aunque el orden real de escritura sea diferente, **este orden es consistente para todos los procesos**
			- ¿Segundo caso no válido?
		* **Consistencia casual
			* ![[Pasted image 20250109223749.png]]
		* **Consistencia eventual
			* ![[Pasted image 20250109224401.png]]
		* ![[Pasted image 20250112015857.png]]