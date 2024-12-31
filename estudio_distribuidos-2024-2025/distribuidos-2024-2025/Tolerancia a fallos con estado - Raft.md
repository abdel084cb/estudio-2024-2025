![[Pasted image 20241229204621.png]]
El **Teorema CAP** establece que un sistema distribuido solo puede garantizar **dos de las tres propiedades** al mismo tiempo:

1. **Consistencia (C):** Todos los nodos ven el mismo estado de datos.
2. **Disponibilidad (A):** Siempre responde a las peticiones, aunque puedan no ser consistentes.
3. **Tolerancia a particiones (P):** Sigue funcionando pese a fallos, retrasos o particiones en la red.

### Consenso
* Objetivos
	* Consistencia
		* Aún con nodos caídos
	* Disponibilidad
		* Suprimir puntos de fallo único
	* Tolerancia a particiones de red
		* Mantener consistencia y disponibilidad aunque sea en una sola partición de red
	* No consideramos fallos bizantinos
* Aproximaciones
	* Simétrica
		* Sin líder
		* Mismo rol
		* Cliente contacta a cualquiera
	* Asimétrica
		* Con líder
		* Cliente solo interactúa con el líder
* Propiedades de un Algoritmo de consenso
	* Acuerdo
	* Terminación
	* Integridad
	* Validez
* Modelo de Máquina de Estados Replicadas
	* Cada estado representa una operación que se realiza
	* Todos los sv procesan la misma op en el mismo orden partiendo desde el mismo estado inicial
	* Todos los sv tienen una copia idéntica de la misma máquina de estados
	* Consistencia secuencial
### Raft
* Componentes de Raft
	* Elección
	* Operación normal (replicación de log)
		* Líder recibe peticiones de los clientes y las registra localmente
		* Replica su log a otros servidores
	* Corrección (safety)
* Arquitectura de Raft
	* RPC
		* AppendEntries
		* RequestVote
		* ...
* Mandatos (Terms)
	* ![[Pasted image 20241229210448.png]]

![[Pasted image 20241229210515.png]]
* Tiempos de expiración (sin recibir un latido) aleatorios y típicos entre 100 y 500
* **Temporizador**
	* Fundamental
	* Latidos periódicos
	* Cada seguidor tiene un temporizador que se desactiva tras recibir un msg del líder.
		* Si no recibe msg expira e inicia elección
* Latido
	* Procedimiento RPC AppendEntries vacío
		* mandato del líder (id)
		* mas información para la consistencia
![[Pasted image 20241229210922.png]]
* **Proceso de Elección de un seguidor**
	* mandato++
	* cambiar a candidato
	* votarse a sí mismo
	* Enviar PeticionVoto a los demás
		* Recibe votos de la mayoría
			* Se convierte en líder
			* Envía latidos a todos los demás
		* Recibe latido
			* Vuelve seguidor
		* Nadie gana
			* Inicia nueva elección
* **Cuando un proceso recibe una petición de voto**
	* Solo puede votar una vez por mandato
	* Se vota al primer candidato
	 * Opciones
		 * Mandato candidato < Mandato seguidor => voto denegado
		 * Ya ha votado => voto denegado
		 * No ha votado a nadie y Mandato candidato > ¿e igual? Mandato Seguidor => voto permitido
	* No puede haber mas de dos mayorías para mas de un candidato en el mismo mandato
* **Registro(log)**
	* entrada = (índice, mandato, operación)
	* commited si se ha almacenado por una mayoría de servidores
	* ![[Pasted image 20241229220032.png]]
* **Operación Normal (sin fallos)**
	* 1) cliente envía op al líder
	* 2) líder añade la op al registro
	* 3) líder manda AppendEntries a los seguidores (pueden ser varias operaciones simultáneas por RPC)
	* 4) una vez la/s entrada/s han sido comprometida/s 
		* líder pasa la op a su maquina de estados y devuelve el resultado al cliente
		* líder notifica a los seguidores de las entradas comprometidas en subsiguientes AppendEntries
		* los seguidores actualizan su maquina de estados
* **Seguidores caídos o lentos**
	* Líder reintenta RPC AppendEntries hasta lograr compromiso de la mayoría
	* Líder reintenta RPC AppendEntries hasta que todos los seguidores tienen el mismo registro
* **Un cambio de líder**
	* Puede conllevar inconsistencias
		* No se han replicado todas las entradas a los seguidores
* **Consistencia del Registro**
	* Si entradas de log en diferentes sv tienen mismo índice y mandato
		* Misma op
		* registros idénticos en todas las entradas anteriores
	* Si una entrada esta comprometida, todas las anteriores también lo están
* **Tras un cambio de líder**
	* Entradas ausentes en seguidores
	* Entradas irrelevantes respecto a líder
	* O ambas
* **Cambio de líder**
	* Líder antiguo pudo haber dejado inconsistencias
	* Al interactuar mediante AppendEntries con los seguidores se detectarán las inconsistencias
	* ![[Pasted image 20241229221222.png]]
	* Líder guarda índice siguiente para cada seguidor
	* Las múltiples caídas en un sistema Raft pueden dejar entradas en los logs de algunos nodos que aún no han sido comprometidas, es decir, no han alcanzado la replicación en una mayoría de los nodos. En estos casos, dichas entradas pueden no ser válidas porque no han sido respaldadas por un quórum. Esto ocurre cuando el líder que las propuso falla antes de completar la replicación, lo que puede resultar en inconsistencias temporales que deben ser corregidas por futuros líderes mediante la sincronización de logs.
* **Requisitos de corrección**
	* Commit
		* Una vez que una entrada es comprometida, ninguna maquina de estados debe aplicar un valor diferente para esa misma entrada
	* Propiedad de corrección en Raft
	* Si un líder decide que una entrada esta comprometida
		* Esa entrada debe estar presente en los registros de todos los líderes futuros
		* Esto asegura que una vez se compromete una entrada, no puede ser sobrescrita ni ignorada.
	* Como se garantiza la corrección en Raft
		* Los líderes nunca sobrescriben entradas de su log
		* Solo entradas del líder pueden comprometerse
		* Las entradas deben comprometerse antes de aplicarse a la máquina de estados
* **Seleccionar al mejor líder**
	* elegir candidatos con más % de contener todas las entradas comprometidas
	* (índice y mandato de última entrada de registro)
	* Un servidor niega su voto a candidato si el registro del servidor está mas completo
		* ![[Pasted image 20241229222438.png]]
* **Neutralizar líderes antiguos**
	* Mediante mandatos
		* También neutralizan candidatos
	* Si alguien se detecta desfasado pasa a seguidor automáticamente
* **Reparación de Registros de Entradas sin comprometer
	* nuevo líder puede intentar comprometer entradas de otros mandatos previos
		* Raft no lo permite
		* líder solo cuenta entradas registradas de su mandato
		* En Raft, cuando una entrada del mandato actual se compromete (es replicada en la mayoría de los nodos), esto garantiza automáticamente que todas las entradas previas en el log también estén comprometidas, incluso si no se verificaron explícitamente. Esto ocurre porque la Log Matching Property asegura que, si una entrada está comprometida, todas las entradas anteriores en los logs de la mayoría de los nodos son idénticas y están en el mismo orden. Esto significa que, al comprometer una entrada reciente, también se validan todas las operaciones previas en el log, garantizando consistencia.
* **Cliente**
	* Si cae el líder contacta a otro sv cualquiera, este le redirigirá al líder
	* El líder no responde al cliente hasta que la entrada se ha comprometido
	* ![[Pasted image 20241229223007.png]]
* **Cambios de configuración**
	* Raft permite cambiar dinámicamente el número de copias
		* Sin necesidad de parar máquinas
		* Por mantenimiento
		* Cambio en el grado de replicación
		* Hace falta utilizar una fase en que conviven mayoría antigua y mayoría nueva
			* Durante la transición, el clúster opera con **dos configuraciones simultáneas**: la configuración actual y la nueva.
			- Las decisiones requieren consenso en ambos conjuntos de nodos (antiguo y nuevo).
			- Una vez que todos los nodos aplican la nueva configuración, se elimina la antigua, completando el cambio.