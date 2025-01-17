### Clases
* **Constructor y destructor**
	* ClaseHola( ) C( )
	* DestructorClaseHola D( )
* **No hace falta poner in, out**
	* Operación(parámetro : tipo) : tipoDevuelto
* **Para enviar datos a otra clase, esta necesita un atributo para recibirlos**
* **Públicas +, Privadas -**
* **Modular y poner nombres mas descriptivos
* `A: List<integer>`

### Secuencia
* **Se pueden poner funciones que devuelven en los diagramas de secuencia obtenerPosicion():parametro, `[parametro == true]`

### Diagrama de estados
* **BD**
	* ![[Pasted image 20250117153930.png]]
* La guarda evalúa el estado **antes de que la acción asociada se ejecute**,
	*  Si tienes `eliminarUno[iluminados > 1]`:
	    - La transición solo puede ocurrir si `iluminados > 1` **antes de ejecutar la acción.**
	    - La acción `eliminarUno()` reducirá el valor de `iluminados`, pero este cambio **no afecta la evaluación de la guarda en esta transición.**
	- Si tienes `eliminarUno[iluminados == 1]` para apagar la farola:
	    - La farola se apagará únicamente si, **antes de ejecutar `eliminarUno()`, el valor de `iluminados` es exactamente 1.**
	    - Después de ejecutar la acción, `iluminados` será 0, y el sistema puede estar en un estado donde la farola ya esté apagada.

### Pruebas caja blanca
* Grafos
	* regiones = aristas - nodos + 2 = nodos predicado +1
* Bucles
	* Superior = externo
	* Inferior = interno

### Diagrama de actividades
* Poner que cada calle sea un actor...
* No puedes poner dos flechas encima de un cuadrado, usar un rombo para juntar flujos
* No confundas fin de flujo con fin de diagrama