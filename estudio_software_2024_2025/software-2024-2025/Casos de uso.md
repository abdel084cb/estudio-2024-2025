* Descripción de un flujo de eventos:
	* Cómo y cuándo empieza y acaba el caso de uso
	* Cuándo interactúa con los actores y qué objetos intercambia con ellos
	* Cada caso de uso tiene un flujo de eventos básico (principal) y, opcionalmente, uno o varios flujos alternativos

![[Pasted image 20241224033819.png]]

### Cuatro tipos de relación:
* Comunicación:
![[Pasted image 20241224034231.png]]
* <u>De Generalización :</u> 
	* El caso de uso hijo hereda la especificación del caso de uso padre.
	* El hijo puede añadir o redefinir el comportamiento del padre.
	* El hijo puede ser colocado en cualquier lugar donde aparezca el padre.
![[Pasted image 20241224034337.png]]

* <u>De Inclusión</u> : Un caso de uso base incorpora explícitamente el comportamiento de otro caso de uso (proveedor) en el lugar especificado en el caso base.
	* Se usa para evitar describir el mismo flujo de eventos repetidas veces. Este comportamiento se pone en un caso de uso aparte (que será incluido por un caso de uso base).
![[Pasted image 20241224034508.png]]

* <u>De extensión</u>
	- **Definición:** Permite que el comportamiento de un caso de uso base sea extendido opcionalmente con comportamiento adicional.
	* ***Modela Comportamiento Opcional:**
	    - Representa partes del sistema que el usuario percibe como opcionales.
	*  **Separación de Obligatorio y Opcional:**
	    - Distingue claramente el comportamiento obligatorio del opcional.
	*  **Condicionalidad:**
	    - Utilizado para modelar subflujos que se ejecutan bajo condiciones específicas.
	- **Puntos de Extensión:**
	    - Pueden añadirse como compartimentos en la elipse del caso de uso base para indicar dónde se integra la extensión.
	- **Notas Explicativas:**
	    - Se pueden usar notas para detallar las condiciones bajo las cuales un caso de uso extiende a otro.
![[Pasted image 20241224035002.png]]

![[Pasted image 20241224035019.png]]

![[Pasted image 20241224035037.png]]
![[Pasted image 20241224035059.png]]

![[Pasted image 20241224035112.png]]
### Recomendaciones: Utilidad de los Casos de Uso
#### Utilidad:
1. **Modelar Comportamiento:**
    - Describir qué hace un elemento, no cómo lo hace.
2. **Comunicación entre Partes:**
    - Permiten a expertos del dominio, usuarios finales y desarrolladores intercambiar opiniones.
3. **Guía de Uso:**
    - Comunican cómo debe usarse el sistema o componente.
4. **Pruebas del Sistema:**
    - Sirven como base para verificar el sistema implementado.
### Construcción de Diagramas de Casos de Uso
#### Pasos:
1. Identificar actores que interactúan con el sistema.
2. Organizar actores en roles generales y especializados.
3. Identificar las formas principales y excepcionales de interacción de los actores.
4. Organizar los comportamientos usando relaciones (`include`, `extend`).
5. Especificar cada caso de uso con texto y trazas de eventos.
#### Sugerencias:
- Cada caso de uso debe ser **distinto y atómico**.
- Factorizar:
    - **Comportamiento común** con `include`.
    - **Variantes de comportamiento** con `extend`.
- **Describir claramente** el flujo de eventos.
- Mostrar solo los casos de uso y actores **relevantes e importantes**.