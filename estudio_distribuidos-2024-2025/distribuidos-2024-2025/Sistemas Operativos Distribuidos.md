### Sistemas Operativos Distribuidos
![[Pasted image 20241230012702.png]]
* Scheduling
	* Compartir recursos: maximizar el uso (%CPU) de los recursos, garantizando el QoS

 **Importancia de los Sistemas Operativos Distribuidos**
1. **Uso eficiente de recursos**: Comparten recursos entre nodos, evitando desperdicio y maximizando el rendimiento.
    - **Sin ellos**: Los recursos quedarían subutilizados, generando mayores costos y menor eficiencia.
2. **Escalabilidad**: Facilitan el crecimiento agregando más nodos para manejar mayores cargas.
    - **Sin ellos**: Sería difícil expandir sistemas, enfrentando limitaciones de hardware y problemas de rendimiento.
3. **Tolerancia a fallos**: Garantizan alta disponibilidad y continuidad del servicio incluso ante fallos.
    - **Sin ellos**: Una falla en un nodo podría provocar interrupciones completas en el sistema.
4. **Distribución geográfica**: Ofrecen acceso global y minimizan la latencia al procesar datos más cerca de los usuarios.
    - **Sin ellos**: Los sistemas centralizados tendrían mayores latencias y menor capacidad para servir a usuarios globales.
5. **Modularidad**: Facilitan mantenimiento y actualizaciones sin afectar al sistema completo.
    - **Sin ellos**: El mantenimiento sería complejo y requeriría detener el servicio completo.
6. **Costo-efectividad**: Usan hardware estándar y distribuyen tareas para optimizar costos.
    - **Sin ellos**: Se requeriría hardware centralizado más costoso, aumentando los gastos operativos.
7. **Flexibilidad**: Integran diferentes plataformas y tecnologías para adaptarse a necesidades específicas.
    - **Sin ellos**: Los sistemas serían rígidos, limitando la integración de nuevas tecnologías.
 **Retos sin Sistemas Operativos Distribuidos**
- **Rendimiento limitado**: Los sistemas centralizados enfrentarían cuellos de botella al manejar grandes volúmenes de datos o usuarios.
- **Falta de confiabilidad**: La dependencia de un único punto central aumentaría el riesgo de fallas catastróficas.
- **Incompatibilidad tecnológica**: Sería más difícil combinar plataformas y recursos heterogéneos.
- **Imposibilidad de escalado global**: Los sistemas locales no podrían adaptarse a usuarios distribuidos geográficamente.
- **Altos costos operativos**: Sería necesario adquirir y mantener hardware especializado para cubrir la demanda.

### Cloud computing

* **Definición (NIST)**
	* La computación en la nube es un modelo que permite el acceso ubicuo, conveniente y bajo demanda a una red de recursos informáticos compartidos configurables (por ejemplo, redes, servidores, almacenamiento, aplicaciones y servicios) que pueden ser aprovisionados y liberados rápidamente con un esfuerzo mínimo de gestión o interacción con el proveedor del servicio. Este modelo de nube se compone de cinco características esenciales, tres modelos de servicio y cuatro modelos de implementación.
	* Características esenciales (NIST)
		* On-Demand self-service
			* Usuarios pueden provisionar recursos hardware
		* Broad network access
			* Acceso ubicuo desde cualquier dispositivo móvil
		* Resource pooling
			* Proveedores ofrecen recursos a múltiples clientes simultáneamente
		* Measured service
			* Uso de recursos/servicios se mide
		* Rapid elasticity
* **Elasticidad**
	* Elasticidad
		* Se varía de forma automática los recursos computacionales (aprovisionando y des-aprovisionando) para adaptarse a la carga de trabajo
	* Carga de trabajo
		* Operaciones sistema computacional sobre unos datos por unidad de tiempo
		* Operaciones involucran
			* recursos
				* CPU
				* almacenamiento
				* red de comunicación
		* Puede ser:
			* frecuencia regular o variable
			* predecible o impredecible
			* Batch vs Online (respuesta inmediata)
	* Escalabilidad
		* Horizontal
			* +/- número de recursos (máquinas físicas, virtuales, contenedores)
		* Vertical
			* +/- capacidad de recursos (memoria, CPU)
	* ![[Pasted image 20241230015411.png]]
		* No aprovisionar mas recursos de los necesarios
		* Si no hay recursos suficientes no se puede mantener QoS
	* **Ciclo de Vida del Componente Gestor de Recursos MAPE**
		* Un gestor de recursos es un componente clave en sistemas informáticos y de computación que se encarga de administrar y asignar eficientemente los recursos disponibles en un sistema. Estos recursos pueden incluir CPU, memoria, almacenamiento, ancho de banda, dispositivos de entrada/salida, procesos y usuarios, entre otros.
		* Monitorización
			* Obtener métricas
				* prestaciones
				* QoS
				* carga de trabajo
			* Debe tener poco overhead
			* preciso
			* en tiempo real muchas veces
			* tamaño de las métricas puede ser enorme
		* Análisis
			* como de lejos esta el sistema del objetivo
				* Posibles objetivos
					* Time deadline
					* Throughput
						* cantidad de trabajo que un sistema puede completar en un período de tiempo determinado
					* Energía
					* Coste económico
			* puede ser
				* reactivo
					* ¿es la capacidad computacional adecuada?
				* predictivo
					* ¿será?
		* Planificación
			* Acción o acciones para alcanzar objetivo de forma rápida
				* equilibrio entre acción demasiado fuerte y demasiado débil
		* Ejecución
			* desencadenamiento de las acciones planificadas
			* estos sistemas tienen inercia
				* es la tendencia que muestra un sistema a permanecer sin cambio durante un tiempo, una vez que se han lanzado las acciones
					* - máquinas no es instantáneo
					* tiempo de procesamiento una vez + capacidad computacional, se verá reflejado cuando haya terminado de procesarse
				* un controlador reactivo sufrirá inercia
					* Cuando se dice que un **controlador reactivo sufrirá inercia**, se está refiriendo a la **tendencia del controlador a tardar en ajustar su comportamiento o respuesta debido a cambios en el entorno o en el sistema**. Este fenómeno puede deberse a varios factores relacionados con la arquitectura del controlador o el contexto en el que opera.
* **Modelos de servicio**
	* Software as a Service (SaaS)
		* se ofrece al consumidor utilizar aplicaciones del proveedor que se ejecutan en la nube
		* a través de varios dispositivos a través de una interfaz de cliente ligero
			* ejemplo: a través de navegador web
	* Platform ... (PaaS)
		* se proporciona la capacidad de desplegar aplicaciones en la infraestructura de la nube
	* Infrastructure (IaaS)
		* se suministra procesamiento, almacenamiento, redes y otros recursos informáticos
* **Modelos de despliegue**
	* Cloud
		* privado
		* comunitario
		* público
		* híbrido
* **Virtualización**
	* ejecución de una instancia virtual (no física) de un recurso computacional (CPU, almacenamiento o red) en una capa que se ha abstraído del hardware subyacente
	* Completa:
		* hypervisor provee servicio multiplexado total del hardware real
		* ![[Pasted image 20241230023953.png]]
	* de nivel sistema operativo (contenedores)
		* Se comparte núcleo de S.O pero se separan en diferentes instancias del sistema: servidores virtuales
	* emulación completa
		* Sistemas operativos y aplicaciones compilados para una arquitectura de procesador se ejecutan sobre otro procesador diferente
	* ![[Pasted image 20241230024741.png]]
### Kubernetes
![[Pasted image 20241230024858.png]]

![[Pasted image 20241230024913.png]]
![[Pasted image 20241230024948.png]]
* **Elementos básicos:**
	* **Pod**
		* Unidad de ejecución en Kubernetes
		* Puede contener 1 o múltiples contenedores con fuerte interrelación
			* Típicamente los contenedores del pod se ejecutan en la misma máquina (virtual o física)
			* Mas habitual 1 app - 1 pod - 1 contenedor
			* Sistema de ficheros compartido entre contenedores
			* Cada contenedor tiene su hw delimitado
		* Es la unidad de escalado
		* Cada POD tiene su IP única en el clúster
			* Se comparte entre sus contenedores
			* Los pods de un cluster se pueden comunicar entre ellos sin NAT
			* ![[Pasted image 20241230025340.png]]
	* **Servicio**
		* Expone nombre, puerto y IP estable para un grupo de Pods
		* Se provee a los Pods mediante un DNS o una variable de entorno
	* **Controladores**
		* Mantienen estado de aplicaciones
			* Monitorización
			* Análisis
			* Acción
	* **Ingress
		* ![[Pasted image 20241230025734.png]]
* **Tipos de aplicaciones**
	- Job 
		- Crea uno o más Pods y asegura que un número determinado de ellos termine con éxito. El trabajo se considera completado correctamente una vez que los Pods finalizan exitosamente. Rearranca Pods si fallan o se eliminan.
	- Daemon Set 
		- Garantiza que todos (o algunos) nodos ejecuten una copia de un Pod. Rearranca Pods si fallan o se eliminan. 
	- Replica Set 
		- Garantiza que un número específico de réplicas esté siempre en ejecución.
	* Deployment
		* Se declara un estado a alcanzar a un determinado ritmo
	* StatefulSet
		* Como deployment pero añade:
			* garantías de unicidad de Pods
			* orden de puesta en marcha y eliminación
	* Services
		* Conjunto lógico de Pods y política de acceso a ellos
			* IPs de los Pods desaparecen con ellos, pero el servicio necesita un punto de acceso estable eliminación
* **Mecanismos organizacionales**
	* Namespaces
		* agrupar recursos
		* cada uno con un nombre dentro de un namespace
		* engloba mayor parte de recursos salvo algunos básicos
	* Labels
		* clave valor ligadas a recursos en Kubernetes como Pods o nodos
		* método mas genérico para organizar grupos de recursos y acceder a ellos
### Scheduling en Kubernetes
* Decidir como y cuando se asignan Pods a Nodos
	* Por defecto
		* prioriza según funciones de priorización seleccionables
		* elige nodo con la prioridad más alta
	* Multi schedulers
		* se pueden seleccionar diferentes schedulers y seleccionarlos de forma explícita para cada pod
![[Pasted image 20241230030827.png]]
* **Administración de Kubernetes
	* kubectl
		* administrar clúster
		* diferentes comandos...