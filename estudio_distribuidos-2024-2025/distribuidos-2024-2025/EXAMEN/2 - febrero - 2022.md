![[Pasted image 20250112181928.png]]
![[Pasted image 20250112181942.png]]
##### a)
![[Pasted image 20250112182432.png]]
##### b)
Eventos concurrentes con d buscamos la propiedad v1 || v2 => not(v1 <= v2) and not(v2 <= v1)
h no concurrente 
i concurrente
j no concurrente
k concurrente
l concurrente
m no concurrente
##### c)
Falso, aunque el PID ayuda a resolver desempates en los relojes escalares para establecer un orden total, utilizar relojes vectoriales no eliminaría la necesidad de enviar el identificador del proceso. Esto se debe a que los relojes vectoriales ofrecen un orden parcial (solo establecen causalidad y detectan concurrencia), pero no garantizan un orden total. Por lo tanto, aunque podríamos identificar la concurrencia, no podríamos establecer un orden completo para determinar qué proceso accede primero a la sección crítica. Además, los relojes vectoriales añaden mayor complejidad y sobrecarga en comparación con los relojes escalares.

![[Pasted image 20250112183814.png]]
### Ejercicio 3
##### 3.1
Falso, Raft garantiza que no pueden existir dos líderes en un mismo mandato. Esto se logra mediante su mecanismo de votación, en el cual cada nodo solo puede emitir un voto por mandato. Si dos nodos inician una elección en el mismo mandato, únicamente uno de ellos puede recibir la mayoría de los votos (quórum). Esto garantiza que solo uno de los nodos puede ser reconocido como líder en ese mandato. Si dos nodos reciben votos y no alcanzan la mayoría, ninguno se convierte en líder, y el mandato termina sin un líder elegido.
##### 3.2
Falso, Una vez que una entrada está comprometida (es decir, ha sido replicada en una mayoría de nodos y el líder ha notificado su compromiso), no puede ser modificada ni eliminada, incluso por el líder. Esto se debe a que Raft garantiza la propiedad de seguridad, que asegura que ninguna entrada comprometida pueda ser sobrescrita. Si el líder intenta enviar entradas conflictivas, los seguidores detectarán la discrepancia y rechazarán las entradas. Esto preserva la consistencia en el sistema. Además el líder no puede modificar su propio registro, solo modifica la de los followers.
##### 3.3
Falso. La propiedad de coincidencia de logs (Log Matching Property) en Raft asegura que si dos entradas en diferentes nodos tienen el mismo índice y mandato, entonces todas las entradas anteriores en ambos nodos también son idénticas. Esto significa que no puede haber discrepancias en entradas anteriores si las posteriores son idénticas. En caso de discrepancias, cuando un nuevo líder toma el control, sobrescribe las entradas conflictivas en los seguidores para garantizar la consistencia de los logs.
##### 3.4
Falso. En Raft, una entrada de registro que ha sido comprometida por un líder debe permanecer idéntica en los logs de todos los líderes futuros. Esto se debe a que:
1. Propiedad de Seguridad: Raft garantiza que cualquier entrada que esté comprometida no será sobrescrita ni modificada, incluso si ocurre un fallo del líder. Los líderes futuros siempre respetarán las entradas comprometidas previamente.
2. Consistencia a través del compromiso: Una entrada se considera comprometida solo después de haber sido replicada en la mayoría de los nodos del clúster. Esto asegura que la entrada es visible y accesible para los futuros líderes, ya que al menos una mayoría la conserva.
3. Además no se puede elegir un líder con el log desactualizado.
##### 3.5
Falso, debido a como se establecen las votaciones (mayoría = N/2 redondeo abajo + 1), entonces como máximo podría ocurrir que uno de los dos grupos se considere caído y no comprometa mas entradas.
- Mayoría necesaria para comprometer entradas: En Raft, una entrada solo puede ser comprometida si un quórum (mayoría) de nodos está de acuerdo. Si hay una partición de red, solo un grupo (el que tiene la mayoría) puede continuar comprometiendo entradas. El otro grupo minoritario queda inactivo y no puede comprometer nuevas entradas.
- Garantía de consistencia: Raft garantiza que una entrada comprometida es consistente entre todas las réplicas que alcanzan el consenso, incluso en presencia de fallos o particiones. Esto significa que no puede haber dos réplicas con entradas diferentes en el mismo índice si ambas están comprometidas.
- Consecuencia de una partición de red:
    - El grupo mayoritario puede seguir operando y comprometiendo nuevas entradas.
    - El grupo minoritario no puede comprometer entradas, ya que no alcanza la mayoría requerida.
    - Por lo tanto, no es posible que las entradas aplicadas al mismo índice en las máquinas de estados sean diferentes.
##### 3.6
Falso, no hay que confundir el consenso con la funcionalidad que nos proporcionan los controladores. ReplicaSet se encarga de que haya siempre un número determinado de replicas de Pods corriendo. No tiene nada que ver con el consenso cosa que se implementaría con Raft o Paxos por ejemplo.
- ReplicaSet en Kubernetes:
    - Función principal: Garantiza que siempre haya un número especificado de réplicas de un pod en ejecución. Si un pod falla o es eliminado, ReplicaSet crea uno nuevo para mantener el estado deseado.
    - No implementa consenso: No utiliza mecanismos como Raft o Paxos para coordinar réplicas o garantizar consistencia entre nodos. Su función se centra exclusivamente en la disponibilidad y el escalado de pods.
- Confusión con el término "consenso"**:
    - El consenso en sistemas distribuidos, como en Raft o Paxos, implica que un grupo de nodos acuerde un valor o estado, incluso en presencia de fallos.
    - ReplicaSet no gestiona acuerdos entre réplicas ni garantiza consistencia en estados. Su rol es más operativo, manteniendo el número de pods en ejecución, sin aplicar lógica de consenso distribuido.
##### 3.7
Verdadero, esta afirmación es correcta. A continuación, se explica por qué:
1. **StatefulSet**:
    - Es un controlador en Kubernetes que gestiona la creación y el mantenimiento de pods con **identidad estable**.
    - Cada réplica dentro de un StatefulSet tiene un **nombre DNS único y predecible**, basado en su índice ordinal. Por ejemplo: `pod-0`, `pod-1`, etc.
    - Incluso si una réplica falla, al ser recreada mantiene su identidad (mismo nombre y dirección DNS).
2. **Recurso Service asociado**:
    - Cuando un StatefulSet se configura con un **Headless Service** (Service sin IP), Kubernetes asigna un **nombre DNS único** para cada pod.
    - Este nombre permite a otros pods o servicios comunicarse con réplicas específicas del StatefulSet.
3. **Resiliencia frente a fallos**:
    - Si una réplica falla, Kubernetes recrea el pod correspondiente con el mismo nombre y dirección DNS.
    - Esto es útil en sistemas donde las réplicas necesitan identidad estable, como bases de datos distribuidas o aplicaciones que mantienen estado.
##### 3.8
Falso, Kerberos no utiliza firmas digitales basadas en criptografía asimétrica para autenticar a sus servidores. En su lugar, Kerberos emplea un sistema basado en **tickets**:
1. **Ticket Granting Ticket (TGT)**: Utilizado para obtener acceso a otros servicios en el dominio Kerberos.
2. **Ticket de Servicio (TS)**: Permite la comunicación segura entre el cliente y el servicio solicitado.
3. **Clave Simétrica**: Los tickets y las comunicaciones en Kerberos están protegidos utilizando criptografía simétrica.
##### 3.9
Falso, las **transacciones distribuidas** generalmente garantizan una **consistencia estricta** (o secuencial), no causal. Esto se debe a que las transacciones distribuidas suelen implementarse utilizando el modelo **ACID** (Atomicidad, Consistencia, Aislamiento, Durabilidad), que busca asegurar que todas las operaciones sean vistas de forma consistente y en el mismo orden en todos los nodos del sistema.

Por otro lado, la **consistencia causal** es más relajada y se limita a preservar relaciones de causalidad entre operaciones, permitiendo más flexibilidad en el orden de las operaciones. Esto no cumple con los estrictos requisitos de las transacciones distribuida
##### 3.10
Verdadero, la **comunicación de grupo atómica** y las **transacciones distribuidas** comparten principios similares en términos de garantizar atomicidad. En una comunicación de grupo atómica:
1. **Entrega atómica**: Un mensaje enviado a un grupo de procesos es entregado a todos los miembros o a ninguno.
2. **Consistencia**: Todos los miembros del grupo ven los mensajes en el mismo orden.
Esto se asemeja a una transacción distribuida, donde una operación afecta a todos los participantes de forma consistente (se realiza completamente o no se realiza en absoluto, manteniendo un estado consistente en todos los nodos). Sin embargo, las transacciones distribuidas suelen incluir otros elementos como aislamiento, mientras que la comunicación de grupo atómica está más enfocada en la difusión confiable de mensajes.

![[Pasted image 20250112193734.png]]![[Pasted image 20250112193813.png]]
### Ejercicio 4
##### 4.1
Las 3 nuevas operaciones realizadas no son encargadas al líder desconectado por obvias razones. Lo que ocurre es que los otros procesos iniciarán una elección, siendo candidato o candidatos aquellos que hayan dado timeout al no recibir latidos del líder. Esto ocurre hasta que se elija un nuevo líder (probablemente solo habrá una elección). Este nuevo líder comenzará a manejar las nuevas operaciones, replicándolas en los seguidores y asegurándose de alcanzar un quórum para comprometerlas. Posteriormente, cuando el viejo líder se reconecte, este intentará enviar latidos al resto del grupo. Sin embargo, estos latidos serán rechazados porque provienen de un término inferior. Finalmente, cuando el viejo líder reciba un latido del nuevo líder con un término más alto, reconocerá su autoridad y pasará al estado de follower. Si el viejo líder tenía entradas no comprometidas en su registro, estas serán sobrescritas por el nuevo líder para garantizar consistencia en todos los nodos. De esta manera, el grupo Raft vuelve a un estado funcional y consistente.

##### 4.2
Un servicio de almacenamiento que utiliza el algoritmo de Raft para tolerancia a fallos tiene diferencias significativas en prestaciones, tanto en términos de ancho de banda como de latencia, comparado con el mismo servicio implementado en una sola máquina sin tolerancia a fallos:
1. **Ancho de banda**:
    - **Raft**: Dado que Raft replica todas las operaciones en varios nodos, el ancho de banda necesario es mayor. Cada operación debe ser enviada al líder, replicada en los seguidores, y los seguidores deben confirmar al líder que han recibido y registrado la operación. Esto implica múltiples comunicaciones en red para cada operación, aumentando significativamente el uso del ancho de banda.
    - **Sola máquina**: El servicio no requiere replicación, por lo que el uso de ancho de banda se limita a la comunicación entre el cliente y el servicio. Esto lo hace mucho más eficiente en términos de ancho de banda.
2. **Latencia**:
    - **Raft**: La latencia de las operaciones es mayor, ya que para comprometer una operación (hacerla persistente), el líder debe asegurarse de que al menos una mayoría (quórum) de nodos haya registrado la operación. Este proceso añade retrasos debido a la comunicación en red y la coordinación entre nodos. Además, cualquier fallo en los nodos puede añadir más latencia si es necesario realizar una elección de líder.
    - **Sola máquina**: La latencia es mínima, ya que no hay necesidad de replicación o coordinación entre nodos. Las operaciones se completan directamente en la máquina que ejecuta el servicio.
3. **Fiabilidad y tolerancia a fallos**:
    - **Raft**: A cambio de mayores costos en ancho de banda y latencia, el servicio garantiza tolerancia a fallos. Incluso si varios nodos fallan (siempre que quede una mayoría funcional), el sistema puede continuar operando de forma consistente.
    - **Sola máquina**: Si la máquina única falla, el servicio se detiene por completo, ya que no hay mecanismos de redundancia o tolerancia a fallos.
En resumen, un sistema basado en Raft sacrifica eficiencia (ancho de banda y latencia) para ofrecer una mayor fiabilidad y tolerancia a fallos, mientras que un sistema en una sola máquina ofrece mejor rendimiento, pero a costa de ser vulnerable a fallos.

##### 4.3
```go
package main

import (
	"fmt"
	"time"
)

// Función que maneja los latidos
func trackHeartbeats(heartbeatChan <-chan string, responseChan chan<- int, timeout time.Duration) {
	ticker := time.NewTicker(50 * time.Millisecond)
	missedBeats := 0
	for {
		select {
		case <-heartbeatChan:
			// Reiniciamos los latidos perdidos al recibir uno
			responseChan <- missedBeats
			missedBeats = 0
		case <-ticker.C:
			// Incrementamos el contador de latidos perdidos cada 50ms
			missedBeats++
		}
	}
}

func main() {
	heartbeatChan := make(chan string)
	responseChan := make(chan int)

	go trackHeartbeats(heartbeatChan, responseChan, 50*time.Millisecond)

	// Simulamos el envío de latidos
	go func() {
		for {
			time.Sleep(100 * time.Millisecond) // Latidos enviados cada 100ms
			heartbeatChan <- "latido"
			fmt.Println("Latido enviado")
		}
	}()

	// Escuchamos las respuestas de latidos perdidos
	for missedBeats := range responseChan {
		fmt.Printf("Latidos perdidos: %d\n", missedBeats)
	}
}
```