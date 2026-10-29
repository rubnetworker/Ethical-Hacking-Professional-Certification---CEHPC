# Caso de estudio: evaluación de vulnerabilidades con CVSS v3.1



Actividad práctica para aplicar el **Common Vulnerability Scoring System (CVSS) versión 3.1** a escenarios documentados de vulnerabilidades. Contiene un ejemplo desarrollado y cuatro ejercicios para que el participante identifique las métricas base, calcule la puntuación y documente sus evidencias.

## Contenido

- Objetivo y preparación
- Instrucciones
- Ejemplo resuelto: SQL almacenado en MySQL
- Ejercicio 1: SSLv3 POODLE
- Ejercicio 2: VMware / Tomcat (inconsistencia de origen)
- Ejercicio 3: Cisco IOS e IOS XE
- Ejercicio 4: Google Chrome
- Entrega de evidencias
- Referencias y observaciones

## Objetivo y preparación

En este laboratorio demostraras como aplicar el estándar CVSS versión 3.1 para puntuar vulnerabilidades especificas

Los detalles de las vulnerabilidades y los ataques se obtuvieron principalmente de la base de datos naciones (NVD) en https://nvd.nist.gov/vuln. También se utilizaron fuentes adicionales cuando se requirieron mas detalles

Los modelos de puntuación asumen que los sistemas de destino están empleando una configuración vulnerable

**Nota:** todas las puntuaciones parten del supuesto de que el sistema de destino presenta la configuración vulnerable descrita. No se requiere explotar ningún sistema para desarrollar el ejercicio.

**Recursos:**
- [Calculadora CVSS v3.1 de FIRST](https://www.first.org/cvss/calculator/3.1)
- [National Vulnerability Database (NVD)](https://nvd.nist.gov/vuln)

## Instrucciones

1. Lee la descripción de la vulnerabilidad y el escenario de ataque.
2. Revisa el comentario de cada una de las **ocho métricas base**.
3. Selecciona los valores correspondientes en la calculadora de FIRST.
4. Comprueba la puntuación objetivo indicada en el documento.
5. Registra el vector CVSS, redacta tu justificación y guarda una captura de pantalla como evidencia.

> **Ética y alcance:** trabaja solo con los escenarios documentados o con sistemas propios/autorizados. Este caso se enfoca en la **evaluación de severidad**, no en ejecutar ataques.

## Ejemplo resuelto: inyección de SQL almacenado en MySQL

**CVE:** [CVE-2013-0375](https://nvd.nist.gov/vuln/detail/CVE-2013-0375)  
**Puntuación base esperada:** **6.4**

### Vulnerabilidad

Una vulnerabilidad en la base de datos del servidor MySQL podría permitir a un usuario autenticado y remoto inyectar código SQL que se ejecuta con privilegios elevados en una base de datos del servidor MySQL remota. Un ataque exitoso podría permitir la lectura o modificación de cualquier dato de la base de datos MySQL remota. La vulnerabilidad se produce debido a una validación insuficiente de los datos proporcionados por el usuario, ya que se replican en instancias remotas de MySQL Server.

### Escenario de ataque

Un atacante necesita una cuenta en la base de datos MySQL de destino con el privilegio de modificar los identificadores proporcionados por el usuario, como los nombres de las tablas. La cuenta debe estar en una base de datos configurada para replicar datos en una o más bases de datos MySQL remotas. Un ataque consiste en iniciar sesión con la cuenta y modificar un identificador a un nuevo valor que contiene un carácter de comillas y un fragmento de SQL malicioso. Posteriormente, este SQL se replicará y ejecutará en uno o más sistemas remotos, como un usuario con muchos privilegios. El SQL malicioso se inyecta en sentencias SQL de una manera que evita la ejecución de sentencias SQL arbitrarias.

### Métricas base y justificación

| Métrica CVSS v3.1 | Valor | Comentarios del caso |
|---|---|---|
| **Attack Vector** | `Network` | El atacante se conecta a la base de datos MySQL explotable a través de una red |
| **Attack Complexity** | `Low` | La replicación debe estar habilitada en la base de datos de destino. Siguiendo las instrucciones y descripción del ataque asumimos que el sistema está configurado de esta manera |
| **Privileges Required** | `Low` | El atacante necesita una cuenta con la capacidad de cambiar los identificadores proporcionados por el usuario, como los nombres de las tablas. Los usuarios básicos no obtienen este privilegio de forma predeterminada, pero no se considera un privilegio suficientemente confiable como para garantizar que esta métrica sea Alta. |
| **User Interaction** | `None` | No se requiere interacción del usuario ya que la replicación ocurre automáticamente. |
| **Scope** | `Changed` | El componente vulnerable es la base de datos del servidor MySQL en la que el atacante inicia sesión para realizar el ataque. El componente afectado es una base de datos (o bases de datos) del servidor MySQL remoto en la que esta base de datos se replica. |
| **Confidentiality** | `Low` | El SQL inyectado se ejecuta con altos privilegios y puede acceder a información a la que el atacante no debería tener acceso. Aunque esto se ejecuta en una base de datos (o bases de datos) remotas, es posible extraer la información como parte de la declaración SQL. El SQL malicioso se inyecta en declaraciones SQL que forman parte de la funcionalidad de replicación, evitando que el atacante ejecute declaraciones SQL arbitrarias. |
| **Integrity** | `Low` | El SQL inyectado se ejecuta con un alto nivel de privilegios y puede modificar información a la que el atacante no debería tener acceso. El SQL malicioso se inyecta en declaraciones SQL que forman parte de la funcionalidad de replicación, evitando que el atacante ejecute declaraciones SQL arbitrarias. |
| **Availability** | `None` | Aunque el código inyectado se ejecuta con altos privilegios, la naturaleza de este ataque evita que se ejecuten sentencias SQL arbitrarias que podrían afectar la disponibilidad de las bases de datos MySQL. |

**Vector del ejemplo:** `CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:C/C:L/I:L/A:N`

### Captura de referencia
<img width="624" height="216" alt="cvss" src="https://github.com/user-attachments/assets/e87c8b74-7e47-4dc3-91a9-d45e1f1a1aa5" />

---
Puedes descargar el archivo Word  en caso de que desees anotar tus repuestas aquí [Caso de estudio  Para El participante.zip](https://github.com/user-attachments/files/34108694/Caso.de.estudio.Para.El.participante.zip)


 
## Ejercicio 1. SSLv3 POODLE (CVE-2014-3566)

**Puntuación base objetivo: 3.1**  
**Herramienta:** [Calculadora CVSS v3.1 de FIRST](https://www.first.org/cvss/calculator/3.1)

**Referencia:** [CVE-2014-3566](https://nvd.nist.gov/vuln/detail/CVE-2014-3566)

### Vulnerabilidad

El protocolo SSL 3.0, como se usa en OpenSSL a través de 1.0.1i y otros productos, utiliza relleno CBC no determinista, lo que hace que sea más fácil para los atacantes intermedios obtener datos de texto sin formato a través de un ataque de padding-oracle, también conocido como "POODLE" (Padding Oracle en el cifrado heredado degradado).

### Escenario de ataque

Un escenario de ataque típico es que una víctima ha visitado un servidor web y su navegador web ahora contiene una cookie que un atacante desea robar. Para un ataque exitoso, el atacante debe poder modificar el tráfico de red entre la víctima y este servidor web, y tanto la víctima como el sistema deben estar dispuestos a utilizar SSL 3.0 para el cifrado.

Un ataque típico comienza cuando el atacante engaña a la víctima para que visite un sitio web que contiene un código malicioso que luego se ejecuta en el navegador web de la víctima. Las restricciones de la Política de Mismo Origen (SOP) en los navegadores web evitan que este código acceda directamente a la cookie que el atacante está tratando de robar, pero HTTP solicita que el código envíe al servidor web automáticamente agregue la cookie, y este comportamiento se usa en el ataque .

El código malicioso envía una solicitud HTTP que adivina el valor del primer byte de la cookie y coloca este byte en una ubicación específica. El atacante modifica la solicitud HTTP cifrada de modo que este byte se utiliza como valor de relleno. Si el servidor acepta la solicitud modificada, el valor adivinado era correcto; si no, el código adivina un valor diferente en una nueva solicitud. Este proceso se repite hasta que se divulga toda la cookie.

### Nota de evaluación del documento

Nota : La puntuación CVSS v3.1 a continuación se adhiere a las pautas para puntuar vulnerabilidades en bibliotecas de software de la Guía del usuario de CVSS v3.1. La puntuación se basa en el peor escenario de implementación razonable y se supone, por ejemplo, que una biblioteca SSL normalmente estará vinculada a la acapa de red (AV: N).

### Completa las métricas

| Métrica CVSS v3.1 | Valor | Comentarios del caso |
|---|---|---|
| **Attack Vector** | ✍️ Por completar | Tenga en cuenta que el ataque puede tener lugar en cualquier punto entre la víctima y el servidor web a través del cual se enruta el tráfico de la red |
| **Attack Complexity** | ✍️ Por completar | Este es un ataque de hombre en el medio y, por lo tanto, complejo para el atacante. |
| **Privileges Required** | ✍️ Por completar | Un atacante no necesita privilegios para montar un ataque. |
| **User Interaction** | ✍️ Por completar | Se debe engañar a la víctima para que ejecute un código malicioso en su navegador web. |
| **Scope** | ✍️ Por completar | El componente vulnerable es el servidor web porque responde de manera insegura a los errores de relleno de una manera que se puede utilizar para datos cifrados por fuerza bruta. El componente afectado también es el servidor web porque la información de las cookies divulgada es parte de su autoridad de autorización. |
| **Confidentiality** | ✍️ Por completar | El ataque revela información de cookies a la que el atacante no debería tener acceso |
| **Integrity** | ✍️ Por completar | No aplica |
| **Availability** | ✍️ Por completar | No aplica |

### Registro de resultados — Ejercicio 1

- **Vector CVSS v3.1:** `CVSS:3.1/AV:__/AC:__/PR:__/UI:__/S:__/C:__/I:__/A:__`
- **Puntuación calculada:** ______
- **Justificación del resultado:** ______
- **Captura de pantalla:** guardar como `evidencias/ejercicio-1.png`.

<!-- Una vez añadida la captura al repositorio, quitar el comentario de la línea siguiente:
![Resultado del ejercicio 1](evidencias/ejercicio-1.png)
-->

---

## Ejercicio 2. Escape de invitado a host de VMware (CVE-2012-1516): caso con inconsistencia

**Puntuación base objetivo: 4.2**  
**Herramienta:** [Calculadora CVSS v3.1 de FIRST](https://www.first.org/cvss/calculator/3.1)

**Referencia del título:** [CVE-2012-1516](https://nvd.nist.gov/vuln/detail/CVE-2012-1516)

> **Advertencia sobre el documento original:** el encabezado y la descripción inicial se refieren a una vulnerabilidad de **VMware**, pero el apartado de ataque y las ocho pistas de puntuación describen un escenario de **Apache Tomcat con un analizador XML**. No son el mismo caso. Se conserva esta discrepancia para que pueda revisarse con el instructor **antes de asignar un vector como respuesta definitiva**. La puntuación **4.2** es la indicada por el material, no una validación independiente del CVE de VMware.

### Vulnerabilidad (VMware, tal como aparece en el documento)

Debido a una falla en la función del controlador para los comandos de llamada a procedimiento remoto (RPC), es posible manipular punteros de datos dentro del proceso de máquina virtual ejecutable (VMX). Esta vulnerabilidad puede permitir que un usuario de una máquina virtual invitada bloquee el proceso de VMX y provoque una denegación de servicio (DoS) en el host o que potencialmente ejecute código en el host.

### Escenario de ataque (Tomcat, tal como aparece en el documento)

Esta vulnerabilidad de Tomcat permite que una aplicación web haga referencia a un analizador XML en lugar de utilizar el analizador XML Apache predeterminado. El atacante debe eliminar todas las aplicaciones web existentes, incluidas las del servidor / aplicaciones web, luego instalar una aplicación web con un analizador XML almacenado en WEB-INF / lib. Esto hará que Tomcat use el nuevo analizador XML para procesar todos los archivos web.xml, context.xml y tld de otras aplicaciones web. Si ese analizador XML no estándar se reemplaza por uno malicioso, el contenido del XML de la aplicación web de la víctima puede ser revelado, el JSP resultante podría estar dañado (si es que se compiló) o posiblemente incluso armado para futuros ataques.

Hay 2 formas diferentes de manifestar este ataque. Primero, un usuario privilegiado local podría simplemente reemplazar el analizador XML que no es Apache con una variante maliciosa. La segunda es que un atacante puede utilizar la ingeniería social y la interacción del usuario para inyectar el analizador XML malicioso en el sistema. Marcaremos para el primero.

### Completa las métricas (pistas correspondientes a Tomcat)

| Métrica CVSS v3.1 | Valor | Comentarios del caso |
|---|---|---|
| **Attack Vector** | ✍️ Por completar | Se requiere acceso de usuario local para leer / modificar archivos de configuración de Tomcat. |
| **Attack Complexity** | ✍️ Por completar | No se necesitan conocimientos especiales para afectar la integridad del analizador XML. |
| **Privileges Required** | ✍️ Por completar | El usuario requiere altos privilegios para poder modificar los archivos de configuración de Tomcat. |
| **User Interaction** | ✍️ Por completar | No aplica |
| **Scope** | ✍️ Por completar | Suponiendo aplicaciones web simples que no mantienen una autoridad de autorización separada. |
| **Confidentiality** | ✍️ Por completar | Se pueden exponer los archivos xml y tld de Webapp. |
| **Integrity** | ✍️ Por completar | Se pierde la integridad del analizador XML, lo que posiblemente da como resultado un JSP dañado. |
| **Availability** | ✍️ Por completar | El resultado razonable detrás de la modificación del analizador XML es hacer que ciertas aplicaciones web no estén disponibles. |

### Registro de resultados — Ejercicio 2

- **Vector CVSS v3.1:** `CVSS:3.1/AV:__/AC:__/PR:__/UI:__/S:__/C:__/I:__/A:__`
- **Puntuación calculada:** ______
- **Justificación del resultado:** ______
- **Captura de pantalla:** guardar como `evidencias/ejercicio-2.png`.

<!-- Una vez añadida la captura al repositorio, quitar el comentario de la línea siguiente:
![Resultado del ejercicio 2](evidencias/ejercicio-2.png)
-->

---

## Ejercicio 3. Omisión de restricciones de autorización en Cisco IOS / IOS XE

**Puntuación base objetivo: 7.2**  
**Herramienta:** [Calculadora CVSS v3.1 de FIRST](https://www.first.org/cvss/calculator/3.1)

**Identificador mencionado por el material:** `CSCtr91106`.

### Vulnerabilidad

Cisco IOS 12.2 a 12.4 y 15.0 a 15.2 e IOS XE 2.1.xa 2.6.xy 3.1.xS antes de 3.1.2S, 3.2.xS a 3.4.xS antes de 3.4.2S, 3.5.xS antes de 3.5.1S y 3.1 .xSG y 3.2.xSG antes de 3.2.2SG, cuando la autorización AAA está habilitada, permite que los usuarios autenticados remotos eludan las restricciones de acceso previstas y ejecuten comandos a través de una (1) sesión HTTP o (2) HTTPS, también conocida como ID de error CSCtr91106

### Escenario de ataque

La vulnerabilidad permite a un atacante eludir las restricciones de autorización de comandos asignadas a su cuenta de usuario específica y ejecutar comandos que están disponibles para el nivel de rol/privilegio para el que está asignado el usuario. Por ejemplo, un usuario que está en un grupo que está asignado al nivel de privilegio 15 (administrador), pero que estaba restringido a ejecutar un solo comando a través de AAA (RADIUS / TACACS) podría aprovechar la vulnerabilidad para ejecutar cualquier otro comando disponible para un usuario administrador sin restricciones. en el nivel de privilegio 15.

### Completa las métricas

| Métrica CVSS v3.1 | Valor | Comentarios del caso |
|---|---|---|
| **Attack Vector** | ✍️ Por completar | Los ataques se ejecutan a través de la API de red. |
| **Attack Complexity** | ✍️ Por completar | No se requieren condiciones especializadas ni conocimientos avanzados. |
| **Privileges Required** | ✍️ Por completar | Si bien son posibles varias variantes, suponga el peor de los casos de vulnerabilidad de explotación de administrador cautivo. |
| **User Interaction** | ✍️ Por completar | No se requiere interacción adicional del usuario para explotar. |
| **Scope** | ✍️ Por completar | La vulnerabilidad permite eludir la autorización, pero el impacto está contenido en el alcance original del componente vulnerable. |
| **Confidentiality** | ✍️ Por completar | La explotación exitosa podría resultar en un compromiso completo del dispositivo objetivo, lo que da como resultado un impacto completo (alto) en la confidencialidad del dispositivo. |
| **Integrity** | ✍️ Por completar | La explotación exitosa podría resultar en un compromiso completo del dispositivo objetivo, lo que resulta en un impacto completo (alto) en la integridad del dispositivo. |
| **Availability** | ✍️ Por completar | La explotación exitosa podría resultar en un compromiso completo del dispositivo objetivo, lo que da como resultado un impacto completo (alto) en la disponibilidad del dispositivo |

### Registro de resultados — Ejercicio 3

- **Vector CVSS v3.1:** `CVSS:3.1/AV:__/AC:__/PR:__/UI:__/S:__/C:__/I:__/A:__`
- **Puntuación calculada:** ______
- **Justificación del resultado:** ______
- **Captura de pantalla:** guardar como `evidencias/ejercicio-3.png`.

<!-- Una vez añadida la captura al repositorio, quitar el comentario de la línea siguiente:
![Resultado del ejercicio 3](evidencias/ejercicio-3.png)
-->

---

## Ejercicio 4. Omisión de sandbox en Google Chrome (CVE-2012-5376)

**Puntuación base objetivo: 9.6**  
**Herramienta:** [Calculadora CVSS v3.1 de FIRST](https://www.first.org/cvss/calculator/3.1)

**Referencia:** [CVE-2012-5376](https://nvd.nist.gov/vuln/detail/CVE-2012-5376)

### Vulnerabilidad

La implementación de comunicación entre procesos (IPC) en Google Chrome antes de la versión 22.0.1229.94 permite a los atacantes remotos eludir las restricciones de sandbox previstas y escribir en archivos arbitrarios aprovechando el acceso a un proceso de renderizado

### Escenario de ataque

Google Chrome utiliza una arquitectura multiproceso en la que cada pestaña del navegador puede ejecutar un proceso de renderizado separado que se comunica con otros procesos de Chrome utilizando el IPC. Al persuadir a una víctima para que visite un sitio web especialmente diseñado, un atacante remoto podría aprovechar esta vulnerabilidad para escribir archivos arbitrarios en el sistema operativo.

### Completa las métricas

| Métrica CVSS v3.1 | Valor | Comentarios del caso |
|---|---|---|
| **Attack Vector** | ✍️ Por completar | La víctima debe visitar un sitio web malicioso que pueda existir fuera de la red local. |
| **Attack Complexity** | ✍️ Por completar | El atacante no necesita realizar ningún reconocimiento especial para este ataque. |
| **Privileges Required** | ✍️ Por completar | El atacante no necesita ningún permiso para realizar este ataque, el atacante permite que la víctima realice la acción en nombre del atacante. |
| **User Interaction** | ✍️ Por completar | La víctima debe hacer clic en un enlace especialmente diseñado proporcionado por el atacante. |
| **Scope** | ✍️ Por completar | Partiendo del supuesto de que el atacante está saliendo del entorno de espacio aislado controlado de Chrome, el componente vulnerable es Google Chrome y el componente afectado es el sistema operativo en el que se ejecuta Chrome. |
| **Confidentiality** | ✍️ Por completar | En el peor de los casos, Chrome se ejecuta con privilegios administrativos. El atacante puede sobrescribir la configuración del sistema y otorgarle acceso a cualquier dato o acceso privilegiado administrativo en el sistema. |
| **Integrity** | ✍️ Por completar | El peor de los casos es que Chrome se ejecuta con privilegios administrativos. El atacante puede sobrescribir cualquier archivo, incluidos los archivos importantes del sistema. |
| **Availability** | ✍️ Por completar | En el peor de los casos, Chrome se ejecuta con privilegios administrativos. El atacante puede provocar un bloqueo del sistema al sobrescribir archivos específicos del sistema o denegar el acceso de un usuario mediante la reconfiguración del sistema. |

### Registro de resultados — Ejercicio 4

- **Vector CVSS v3.1:** `CVSS:3.1/AV:__/AC:__/PR:__/UI:__/S:__/C:__/I:__/A:__`
- **Puntuación calculada:** ______
- **Justificación del resultado:** ______
- **Captura de pantalla:** guardar como `evidencias/ejercicio-4.png`.

<!-- Una vez añadida la captura al repositorio, quitar el comentario de la línea siguiente:
![Resultado del ejercicio 4](evidencias/ejercicio-4.png)
-->

---

## Entrega de evidencias

Se recomienda organizar el repositorio de la siguiente manera:

```text
caso-estudio-cvss/
├── README.md
├── assets/
│   └── cvss-ejemplo.png
└── evidencias/
    ├── ejercicio-1.png
    ├── ejercicio-2.png
    ├── ejercicio-3.png
    └── ejercicio-4.png
```

Las imágenes de `evidencias/` **deben ser generadas por el participante** y no están incluidas en este repositorio inicial. Una vez disponibles, descomenta la línea Markdown correspondiente a cada ejercicio para mostrarlas.

### Lista de verificación

- [ ] Ejercicio 1: métricas, vector, puntuación, justificación y captura.
- [ ] Ejercicio 2: métricas, vector, puntuación, justificación y captura.
- [ ] Ejercicio 3: métricas, vector, puntuación, justificación y captura.
- [ ] Ejercicio 4: métricas, vector, puntuación, justificación y captura.

## Referencias y observaciones

- [FIRST — Calculadora CVSS v3.1](https://www.first.org/cvss/calculator/3.1)
- [FIRST — Especificación CVSS v3.1](https://www.first.org/cvss/v3.1/specification-document)
- [NIST — NVD](https://nvd.nist.gov/vuln)

**Fidelidad al material:** las descripciones, objetivos de puntuación y pistas se preservan del documento proporcionado. Se regularizaron títulos, tildes, redacción instrumental y estructura para GitHub; las respuestas de los ejercicios se mantienen sin resolver. Se identifica expresamente la inconsistencia de VMware/Tomcat en el ejercicio 2.

