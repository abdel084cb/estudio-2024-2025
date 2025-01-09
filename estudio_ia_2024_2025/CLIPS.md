#### **1. `test`**

Evalúa una condición lógica o matemática en el lado derecho de una regla (después de `=>`).

- **Sintaxis:**
    
    ```clips
    (test <expression>)
    ```
    
- **Parámetros:**
    - `<expression>`: Una expresión lógica o matemática que evalúa a verdadero o falso.
- **Uso:** Permite ejecutar acciones solo si una condición es verdadera.

#### **2. Operadores básicos**

- **`?` (Variable):** Representa una variable que captura un solo valor de un slot.
    
    ```clips
    (persona (nombre ?nombre)) ; Captura el valor del slot `nombre`.
    ```
    
- **`$?` (Variable multivalor):** Representa una variable que captura múltiples valores de un slot multivalor.
    
    ```clips
    (persona (nombres $?nombres)) ; Captura todos los valores del slot `nombres`.
    ```
    
- **`?&` (Restricción múltiple):** Aplica múltiples condiciones al mismo tiempo.
    
    ```clips
    (persona (edad ?edad&:(> ?edad 18)&:(< ?edad 65))) ; Edad entre 18 y 65.
    ```
    

#### **3. `defrule`**

Define una regla en CLIPS. Una regla consiste en una parte condicional (antecedente) y una parte de acción (consecuente).

- **Sintaxis:**
    
    ```clips
    (defrule <rule-name>
      (<conditions>)
      =>
      (<actions>))
    ```
    
- **Parámetros:**
    - `<rule-name>`: Nombre de la regla.
    - `<conditions>`: Condiciones que deben cumplirse.
    - `<actions>`: Acciones a ejecutar si las condiciones son verdaderas.

#### **4. `deffacts`**

Permite definir un conjunto de hechos que se inicializan al ejecutar el comando `(reset)`.

- **Sintaxis:**
    
    ```clips
    (deffacts <fact-name>
      (<fact1>)
      (<fact2>))
    ```
    
- **Parámetros:**
    - `<fact-name>`: Nombre del grupo de hechos.
    - `<fact1>, <fact2>`: Hechos individuales.

#### **5. `modify`**

Actualiza un hecho existente, cambiando el valor de uno o más slots.

- **Sintaxis:**
    
    ```clips
    (modify <fact-index> <slot-name> <new-value>)
    ```
    
- **Parámetros:**
    - `<fact-index>`: El identificador del hecho que se desea modificar.
    - `<slot-name>`: El nombre del slot a cambiar.
    - `<new-value>`: El nuevo valor del slot.

#### **6. `create`**

Genera dinámicamente valores o listas en el lado derecho de una regla.

- **Sintaxis:**
    
    ```clips
    (create <value1> <value2> ...)
    ```
    
- **Uso:** Crear listas para slots multivalor o generar datos dinámicamente.

#### **7. `deftemplate`**

Define la estructura de un hecho que puede tener uno o más slots.

- **Sintaxis:**
    
    ```clips
    (deftemplate <template-name>
      (slot <slot-name1>)
      (slot <slot-name2>))
    ```
    
- **Parámetros:**
    - `<template-name>`: Nombre del template.
    - `<slot-name>`: Nombres de los slots.

#### **8. `assert`**

Inserta un hecho en el sistema.

- **Sintaxis:**
    
    ```clips
    (assert (<fact>))
    ```
    
- **Parámetros:**
    - `<fact>`: El hecho a insertar.

#### **9. `retract`**

Elimina un hecho del sistema.

- **Sintaxis:**
    
    ```clips
    (retract <fact-index>)
    ```
    
- **Parámetros:**
    - `<fact-index>`: El identificador del hecho que se desea eliminar.

#### **10. `focus`**

Cambia la agenda activa a un módulo específico.

- **Sintaxis:**
    
    ```clips
    (focus <module-name>)
    ```
    
- **Parámetros:**
    - `<module-name>`: Nombre del módulo que se desea activar.

#### **11. `printout`**

Imprime texto o valores en la consola.

- **Sintaxis:**
    
    ```clips
    (printout <destination> <text/value> ...)
    ```
    
- **Parámetros:**
    - `<destination>`: `t` (para la consola).
    - `<text/value>`: Texto o variables a imprimir.

#### **12. `$` (Variable multivalor)**

Captura múltiples valores en un slot multivalor.

- **Sintaxis:**
    
    ```clips
    (slot $?variable)
    ```
    

---

### **¿Otras funciones básicas que podrías necesitar?**

#### **`bind`**

Asocia un valor a una variable.

- **Sintaxis:**
    
    ```clips
    (bind ?variable <value>)
    ```
    
- **Uso:** Permite almacenar un valor en una variable para usarlo más adelante.

#### **`reset`**

Inicializa el entorno de CLIPS, activando los hechos definidos en `deffacts`.

- **Sintaxis:**
    
    ```clips
    (reset)
    ```
    

#### **`run`**

Ejecuta todas las reglas activas en la agenda.

- **Sintaxis:**
    
    ```clips
    (run)
    ```