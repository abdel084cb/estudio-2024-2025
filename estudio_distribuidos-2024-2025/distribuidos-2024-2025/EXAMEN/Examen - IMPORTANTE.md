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
