### Diagrama de paquetes

No ha entrado nunca

### Diagrama de componentes

No ha entrado nunca

### Diagrama de despliegue
###### Propósito:
- Representar la **vista física del sistema** después de tomar decisiones de diseño.
###### Características principales:
1. **Usos**:
    - Mostrar la **descomposición en subsistemas**.
    - Modelar la **concurrencia** del sistema.
    - Relacionar **hardware y software** mediante mapeo.
2. **Estructura**:
    - Es un **grafo de nodos** conectados por asociaciones de comunicación.
    - **Nodo**:
        - Elemento físico en tiempo de ejecución.
        - Representa recursos computacionales (memoria + capacidad de procesamiento).
        - Se dibujan como **cajas 3D**.
    - **Conexiones**:
        - Representan asociaciones de comunicación entre nodos.
        - Pueden estereotiparse para indicar el tipo de conexión (e.g., `<<RS232>>`, `<<Ethernet 10T>>`).
###### Artefactos en los Nodos:
Exactamente, los artefactos representan los elementos necesarios para que un nodo funcione correctamente o para ejecutar la aplicación en ese nodo. Son componentes de software físicos o tangibles que se despliegan en los nodos, como archivos ejecutables, librerías, bases de datos o scripts de configuración. Sin los artefactos, los nodos serían simplemente infraestructura sin el software que necesitan para cumplir su propósito.

1. **Definición**:
    - Elementos físicos y reemplazables que existen en la **plataforma de implementación**.
    - Ejemplos: ejecutables, librerías, tablas, archivos, documentos.
3. **Propiedades**:
    - Pertenecen al mundo físico de los **bits**.
    - Representan el empaquetamiento físico de elementos lógicos como componentes, clases o interfaces.
4. **Representación**:
    - Se muestran como rectángulos con la palabra clave `<<artifact>>`.

![[Pasted image 20241224000309.png]]

![[Pasted image 20241224000338.png]]

En un diagrama de despliegue, los canales de comunicación representan la forma en que los nodos (dispositivos o recursos computacionales) se conectan entre sí para transmitir datos o información. Estos canales pueden ser etiquetados con estereotipos que indican el tipo de tecnología o protocolo utilizado.

 **Ejemplos de Canales de Comunicación**
1. **Protocolo de Red:**
    - `<<http>>`: Comunicación HTTP (Web).
    - `<<https>>`: Comunicación segura HTTP con cifrado.
    - `<<ftp>>`: Protocolo de transferencia de archivos.
    - `<<sftp>>`: FTP seguro.
    - `<<smtp>>`: Protocolo de envío de correos electrónicos.
    - `<<pop3>>`: Protocolo de recuperación de correos electrónicos.
    - `<<imap>>`: Acceso a correos electrónicos desde múltiples dispositivos.
    - `<<tcp/ip>>`: Protocolo de control de transmisión y Protocolo de Internet.
    - `<<udp>>`: Protocolo de datagramas de usuario.
    - `<<ws>>`: WebSocket para comunicación en tiempo real.
    - `<<mqtt>>`: Protocolo para IoT (Internet of Things).
    - `<<coap>>`: Protocolo de Aplicación Constrained para dispositivos IoT.
    - `<<soap>>`: Comunicación basada en servicios web.
    - `<<rest>>`: Arquitectura RESTful para servicios web.
2. **Protocolos de Hardware:**
    - `<<rs232>>`: Comunicación por puerto serie.
    - `<<usb>>`: Comunicación por USB.
    - `<<bluetooth>>`: Comunicación inalámbrica de corto alcance.
    - `<<zigbee>>`: Protocolo de comunicación para IoT de bajo consumo.
    - `<<nfc>>`: Comunicación de campo cercano.
    - `<<rfid>>`: Identificación por radiofrecuencia.
    - `<<modbus>>`: Protocolo de comunicación industrial.
    - `<<can>>`: Comunicación en redes de automoción.
3. **Protocolo de Almacenamiento:**
    - `<<nfs>>`: Sistema de archivos de red.
    - `<<smb>>`: Protocolo de compartición de archivos.
    - `<<iscsi>>`: Protocolo para almacenamiento en red.
    - `<<ftp-storage>>`: Transferencia de archivos para almacenamiento.
    - `<<cloud>>`: Acceso a recursos en la nube (AWS, Azure, Google Cloud).
4. **Protocolo de Seguridad:**
    - `<<vpn>>`: Red privada virtual.
    - `<<tls>>`: Protocolo de capa de transporte seguro.
    - `<<ssl>>`: Protocolo de capa de sockets seguros.
    - `<<kerberos>>`: Sistema de autenticación de red.
5. **Otros:**
    - `<<ethernet>>`: Comunicación a través de Ethernet.
    - `<<token-ring>>`: Red en anillo.
    - `<<p2p>>`: Comunicación entre pares.
    - `<<satellite>>`: Comunicación por satélite.
 **Artifacts en Diagramas de Despliegue**
Los artifacts representan partes físicas del sistema que se ejecutan o almacenan en los nodos. Son elementos tangibles en el nivel de implementación, como archivos, ejecutables, o documentos de configuración.
 **Ejemplos de Artifacts**
1. **Componentes de Software:**
    - `<<jar>>`: Archivo Java ejecutable o biblioteca (`aplicacionCliente.jar`).
    - `<<war>>`: Archivo para despliegue en servidores web (`planificador.war`).
    - `<<ear>>`: Archivo de aplicación empresarial.
    - `<<dll>>`: Librería dinámica en Windows.
    - `<<exe>>`: Archivo ejecutable.
    - `<<py>>`: Script Python.
    - `<<sh>>`: Script de shell.
    - `<<bin>>`: Archivo binario.
    - `<<so>>`: Librería compartida en Unix/Linux.
2. **Bases de Datos y Configuración:**
	* `<<exe>>` Se puede lanzar una base de datos con un ejecutable
    - `<<sql>>`: Script de base de datos.
    - `<<config>>`: Archivo de configuración (JSON, YAML, XML).
    - `<<ini>>`: Archivo de configuración inicializable.
    - `<<properties>>`: Archivo de propiedades para configuración en Java.
    - `<<jdbc>>`: Utilizada en sistemas Java para conectar con bases de datos relacionales.
4. **Documentos y Archivos:**
    - `<<pdf>>`: Documento PDF.
    - `<<docx>>`: Documento Word.
    - `<<xlsx>>`: Hoja de cálculo Excel.
    - `<<txt>>`: Archivo de texto plano.
    - `<<html>>`: Archivo HTML para web.
    - `<<css>>`: Hoja de estilos para web.
    - `<<js>>`: Script JavaScript.
5. **Archivos de Recursos:**
    - `<<png>>`, `<<jpg>>`: Archivos de imagen.
    - `<<svg>>`: Gráficos vectoriales.
    - `<<mp3>>`, `<<wav>>`: Archivos de audio.
    - `<<mp4>>`, `<<mkv>>`: Archivos de video.
    - `<<zip>>`, `<<tar.gz>>`: Archivos comprimidos.
6. **Elementos de Red:**
    - `<<log>>`: Archivo de registro del sistema.
    - `<<iso>>`: Imagen de disco.
    - `<<vm>>`: Máquina virtual (VirtualBox, VMWare).
7. **Otros:**
    - `<<artifact>>`: Elemento genérico que no entra en otras categorías.
    - `<<container>>`: Contenedor de servicios (Docker, Kubernetes).

###### **Tipos de nodos**
- **Servidor**: Representa un servidor físico o virtual.
- **PC Cliente**: Representa un dispositivo cliente.
- **Dispositivo Móvil**: Representa un teléfono o tablet.
- **Base de Datos**: Representa un nodo que gestiona datos.
- **Red o Gateway**: Representa dispositivos que manejan la comunicación en la red.

En un **diagrama de despliegue (UML)**, los nodos suelen representar **entidades físicas** en las que se ejecutan componentes o artefactos. Sin embargo, también pueden representar elementos virtuales dependiendo del contexto. Aquí tienes una explicación detallada:

 **Representación física de los nodos**

1. **Dispositivos físicos**:
    
    - Computadoras, servidores, dispositivos móviles, quioscos, etc.
    - Por ejemplo:
        - Un servidor físico donde se ejecuta una base de datos.
        - Una máquina cliente utilizada por el usuario.
2. **Infraestructura de red**:
    
    - En algunos casos, un nodo puede representar un router, un switch o cualquier dispositivo de red físico.

 **Representación virtual o lógica**

Aunque típicamente los nodos se asocian a hardware físico, en un entorno moderno también pueden representar:

1. **Máquinas virtuales**:
    
    - Como instancias en un entorno de nube (AWS, Azure, Google Cloud).
    - Por ejemplo: un nodo podría ser una instancia EC2 en AWS donde se despliegan aplicaciones.
2. **Contenedores**:
    
    - Un nodo podría representar un contenedor Docker o un clúster de Kubernetes.
    - Esto es común cuando se trabaja en arquitecturas modernas basadas en microservicios.
3. **Plataformas abstractas**:
    
    - Por ejemplo, un nodo podría representar un entorno como "Aplicación Web" o "Plataforma Móvil" para indicar el contexto donde se ejecutan los componentes.

### **Relación entre nodos y artefactos**

- Los **nodos físicos o virtuales** contienen los artefactos (programas, ejecutables, librerías, bases de datos, etc.) que se despliegan en ellos.
- Por ejemplo:
    - Un nodo físico podría contener un servidor web (`.war`), un ejecutable (`.exe`), o un script de inicialización.