### Pruebas dinámicas
Las **pruebas dinámicas** son un tipo de prueba de software que se centra en evaluar el **comportamiento del sistema en ejecución**.

**Pruebas de caja negra**: Son pruebas que se centran en evaluar el **comportamiento externo** del software, sin considerar su implementación interna o estructura de código. Solo se analizan las entradas y salidas del sistema para verificar que se comporta según los requisitos especificados

**Pruebas de caja blanca**: Son pruebas que se centran en evaluar el **funcionamiento interno** del sistema. Implican analizar y probar directamente la estructura, el flujo y la lógica del código fuente.
#### Pruebas de caja blanca
##### Prueba de caminos:
1. **Dibujar el grafo de flujo asociado**:
   - A partir del diseño (diagrama de actividad) o del código fuente, se construye el grafo de flujo correspondiente.
2. **Calcular la complejidad ciclomática**:
   - Determinar el número máximo de caminos linealmente independientes en el grafo de flujo.
3. **Determinar el conjunto básico de caminos**:
   - Identificar los caminos linealmente independientes que deben ser evaluados.
4. **Preparar casos de prueba**:
   - Diseñar casos de prueba que obliguen a la ejecución de cada camino identificado en el conjunto básico.

###### Paso 1
![[Pasted image 20241225032317.png]]
![[Pasted image 20241225031959.png]]

Dicho esto, teniendo el siguiente código:
![[Pasted image 20241225032047.png]]

Se construye el siguiente grafo:
![[Pasted image 20241225032116.png]]
###### Paso 2
- La **complejidad ciclomática** de un grafo de flujo (V(G)) establece el número de caminos independientes.
1. **Número de regiones**:
   - Contar las regiones del grafo de flujo.
2. **Fórmula basada en aristas y nodos**:
   - V(G) = A - N + 2
     - Donde:
       - **A**: Número de aristas.
       - **N**: Número de nodos.
3. **Fórmula basada en nodos predicado**:
   - V(G) = P + 1
     - Donde:
       - **P**: Número de nodos predicado (nodos que representan decisiones o bifurcaciones).

Dicho esto, siguiendo el anterior ejemplo:
![[Pasted image 20241225032657.png]]

###### Paso 3 y Paso 4
**3. Selecciona caminos independientes**:
- Un camino independiente es aquel que introduce al menos una arista o nodo nuevo no cubierto por los caminos previamente seleccionados.
- Empieza con el camino más simple, como del nodo inicial al nodo final sin tomar bifurcaciones.
- Añade caminos que pasen por bifurcaciones y nuevos bucles.
- Cada nuevo camino debe incluir una **arista o nodo nuevo** que no haya sido recorrido por los caminos anteriores.

**4. Preparar casos de prueba para cada camino**:
- Para cada camino independiente que identificaste, crea un caso de prueba que fuerce al programa a ejecutar ese camino.
- Un caso de prueba está compuesto por:
    - **Entrada(s):** Datos que se pasan al sistema para probarlo.
    - **Salida(s) esperada(s):** El resultado esperado según el camino que debe ejecutarse.
    - **Camino al que corresponde**

Dicho esto, siguiendo con el ejemplo anterior:
![[Pasted image 20241225033242.png]]
##### Prueba de bucles
* Hay cuatro tipos de bucles:
	* Simples
	* Anidados
	* Concatenados
	* No estructurados
![[Pasted image 20241225044127.png]]
###### Bucles simples y anidados

**Simples:**
Se deben aplicar las siguientes pruebas:
- **Pasar por alto el bucle:** No realizar ninguna iteración.
- **Pasar una sola vez el bucle:** Ejecutar el cuerpo del bucle una sola vez.
- **Pasar dos veces el bucle:** Ejecutar el cuerpo del bucle dos veces consecutivas.
- **Hacer un número medio de iteraciones (m) (con m < n):** .
- **Hacer n-1 y n iteraciones por el bucle (donde n es máximo número posible de iteraciones para el bucle)**

 **Anidados**:
Para probar bucles anidados se debe seguir un enfoque escalonado, comenzando desde el bucle más interno hacia el más externo:
* Realizar las pruebas de bucle simple al **bucle más interior** estableciendo los **demás bucles en sus valores mínimos**
* **Avanzar hacia fuera** confeccionando pruebas para el siguiente bucle manteniendo todos los **externos con valores mínimos y los internos con valores medios**
* **Continuar hasta terminar de probar bucles**
![[Pasted image 20241225044927.png]]
Dicho esto, tenemos el siguiente ejemplo:
![[Pasted image 20241225045015.png]]
Cuya solución es:
*Nota: hay que tener en cuenta que no hay número máximo de iteraciones por ejemplo en el bucle interno puesto que al ser enteros los parámetros podemos poner un número negativo infinito.*
*Nota: Al no haber n, elegir m es arbitrario (simplemente sentido común), en otro caso elegir un valor m menor que n. Normalmente dividir entre 2 y ya, pero parece ser que los profesores no le dan mucha importancia a m, simplemente se aseguran de que es menor*
![[Pasted image 20241225050018.png]]

![[Pasted image 20241225045042.png]]

###### Bucles concatenados

* **Concatenados:**
	* Se pueden probar igual que los bucles simples si son independientes entre sí
	* y siguiendo la técnica de los bucles anidados si existe cualquier relación entre los diferentes bucles concatenados
	* Por ejemplo, si hay dos bucles concatenados y se usa el contador del bucle 1 como valor inicial del bucle 2, entonces los bucles no son independientes -> se aplicará el enfoque para bucles anidados

Dicho esto, tenemos un ejemplo como bucles independientes:
*Nota: los do-while no se pueden saltar*
![[Pasted image 20241225050443.png]]
![[Pasted image 20241225050508.png]]

Y otro como bucles anidados:
![[Pasted image 20241225050528.png]]
###### Bucles no estructurados
Estos se deben rediseñar, no son deseables.
#### Pruebas de caja negra
##### Particiones de equivalencia
* La realización de casos de prueba por medio de particiones de equivalencia consta de dos pasos:
	1. Identificación de las clases de equivalencia
	2. Definición de los casos de prueba

###### Identificación de las clases de equivalencia
- **Definición:**  
  Se identifican dividiendo cada condición de entrada en clases válidas e inválidas.
 * **Directrices para definir clases:**
	1. **Rangos de valores:**  
	   - Clase válida: Dentro del rango (ej. 1 <= valor <= 999).  
	   - Clases inválidas: Fuera del rango (valor < 1 o valor > 999).  
	2. **Valor específico:**  
	   - Clase válida: Valor requerido (ej. tamaño del código = 5).  
	   - Clases inválidas: Fuera del valor (tamaño < 5, tamaño > 5).  
	3. **Conjunto de valores:**  
	   - Clase válida: Cada valor del conjunto (ej. AUTOBÚS, TAXI, etc.).  
	   - Clase inválida: Cualquier valor fuera del conjunto (ej. PATINES).  
	4. **Condiciones booleanas:**  
	   - Clase válida: Cumple la condición (ej. el carácter es una letra).  
	   - Clase inválida: No cumple la condición (ej. el carácter no es una letra).

![[Pasted image 20241225055920.png]]
###### Definición de los casos de prueba
1. Asignar un número único a cada clase de equivalencia.
2. Crear casos de prueba que cubran todas las clases de equivalencia válidas, priorizando cubrir varias en un mismo caso.
3. Crear casos de prueba para cubrir cada clase de equivalencia inválida, uno por cada clase.

Dicho esto, tenemos el siguiente ejemplo
![[Pasted image 20241225060515.png]]
![[Pasted image 20241225060612.png]]
![[Pasted image 20241225060635.png]]
##### Árboles/tablas de decisión
* Las condiciones de entrada y las acciones a realizar permiten diseñar casos de prueba
	* Condiciones de entrada --> Valores de entrada
	* Acciones a realizar (reglas de decisión) --> Resultados esperados

Dicho esto, tenemos el siguiente ejemplo:

![[Pasted image 20241225061906.png]]
