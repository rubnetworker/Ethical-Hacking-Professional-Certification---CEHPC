# Ethical Hacking

## Actividad 05. Escaneo con ZAP OWASP

### Ethical Hacking Professional Certification (CEHPC)

Módulo: Análisis de Vulnerabilidades
Nivel: Básico
Duración estimada: 60 minutos, con el entorno previamente preparado
Sistema operativo: Kali Linux
Herramienta: OWASP ZAP (Zed Attack Proxy)
Modalidad: Práctica individual, guiada o autodirigida

## 1. Introducción

OWASP ZAP (Zed Attack Proxy) es una herramienta de seguridad de aplicaciones web de código abierto, desarrollada por la comunidad OWASP (Open Worldwide Application Security Project). Está diseñada para ayudar a identificar vulnerabilidades de seguridad en aplicaciones web durante las actividades de desarrollo, evaluación y pruebas de penetración.

ZAP proporciona una interfaz gráfica que permite automatizar pruebas de seguridad, realizar escaneos manuales y examinar las comunicaciones entre un navegador y un servidor web.

Entre las vulnerabilidades y problemas de seguridad que puede ayudar a identificar se encuentran:

- SQL Injection: vulnerabilidades relacionadas con el tratamiento inseguro de datos enviados a consultas SQL.

- Cross-Site Scripting (XSS): situaciones en las que una aplicación permite la inclusión o ejecución de contenido activo no confiable en el navegador.

- Cross-Site Request Forgery (CSRF): escenarios en los que una aplicación puede aceptar acciones no deseadas realizadas en el contexto de una sesión autenticada.

- Configuraciones de seguridad incorrectas: ausencia de determinadas cabeceras HTTP, configuraciones inseguras y exposición de información técnica.

- Componentes vulnerables: tecnologías o bibliotecas que pueden presentar vulnerabilidades conocidas.

Durante esta actividad utilizarás OWASP ZAP para realizar un escaneo automatizado sobre una aplicación web de laboratorio. Posteriormente, examinarás las solicitudes HTTP generadas, las alertas de seguridad y los recursos encontrados durante la exploración.

Importante: La identificación de una alerta no significa necesariamente que exista una vulnerabilidad confirmada. Los resultados de las herramientas automatizadas deben interpretarse considerando sus evidencias y el contexto de la aplicación.

## 2. Objetivo de la actividad

Utilizar OWASP ZAP para realizar un escaneo automatizado de seguridad sobre una aplicación web autorizada, identificar las solicitudes generadas durante el análisis y consultar las posibles vulnerabilidades detectadas.

Al finalizar la actividad, habrás realizado las siguientes operaciones:

1. Verificar la disponibilidad de OWASP ZAP en Kali Linux.

2. Instalar la herramienta cuando no se encuentre disponible.

3. Iniciar y preparar OWASP ZAP.

4. Configurar el objetivo del escaneo.

5. Ejecutar un análisis automatizado.

6. Examinar las solicitudes HTTP realizadas.

7. Consultar y revisar las alertas de seguridad.

8. Examinar los recursos encontrados por Spider.

9. Guardar las evidencias y resultados obtenidos.

## 3. Alcance y condiciones de seguridad

La actividad se realizará exclusivamente sobre una aplicación web de laboratorio destinada a pruebas de seguridad.

Las operaciones permitidas comprenden el reconocimiento de recursos web, la exploración de enlaces, la ejecución de un escaneo automatizado y el análisis de sus resultados.

Debido a que ZAP puede enviar solicitudes especialmente diseñadas para identificar vulnerabilidades, el escaneo activo podría modificar información o afectar temporalmente la disponibilidad de aplicaciones vulnerables.

Por este motivo:

- Utiliza únicamente máquinas virtuales y aplicaciones expresamente autorizadas.

- No ejecutes escaneos sobre sitios web públicos, redes corporativas o sistemas ajenos sin autorización.

- Mantén los objetivos vulnerables en una red virtual aislada.

- No utilices datos personales, credenciales reales ni información confidencial.

- Evita ejecutar otras herramientas de ataque simultáneamente sobre el mismo objetivo.

- No amplíes el alcance del escaneo hacia otros equipos o servicios.

- Utiliza una máquina objetivo que pueda restaurarse mediante una instantánea (snapshot) si fuera necesario.

## 4. Herramientas y requisitos previos

### 4.1. Herramientas utilizadas

Kali Linux

Distribución de Linux orientada a la seguridad informática, que proporciona herramientas para reconocimiento, análisis de vulnerabilidades y pruebas de penetración.

OWASP ZAP

Herramienta utilizada para explorar aplicaciones web, inspeccionar tráfico HTTP/HTTPS y detectar posibles problemas de seguridad.

Navegador web

Firefox, Chromium u otro navegador disponible en Kali Linux. Se utilizará para verificar que la aplicación objetivo responda correctamente.

Aplicación web de laboratorio

Servidor o aplicación web vulnerable, alojada en una máquina virtual o entorno controlado, sobre la cual se realizarán las pruebas.

### 4.2. Requisitos del equipo

Antes de iniciar, verifica que dispones de:

- Kali Linux funcionando correctamente.

- Una cuenta de usuario con permisos para utilizar sudo.

- Acceso a Internet para instalar ZAP, si es necesario.

- Espacio libre suficiente para instalar la herramienta y guardar resultados.

- Una máquina virtual o aplicación web de laboratorio accesible desde Kali Linux.

- La dirección IP o URL de dicha aplicación.

### 4.3. Entorno de laboratorio

Se recomienda utilizar la siguiente configuración:

| Elemento | Función |
| --- | --- |
| Kali Linux | Equipo desde el cual se ejecutará ZAP |
| Aplicación web vulnerable | Objetivo del escaneo |
| Red Host-only o aislada | Comunicación entre los equipos de laboratorio |
| OWASP ZAP | Herramienta de análisis de aplicaciones web |

Ejemplo de direccionamiento:

| Dispositivo | Dirección IP |
| --- | --- |
| Kali Linux | 192.168.56.10 |
| Servidor web de laboratorio | 192.168.56.101 |

Estas direcciones son ilustrativas. Debes utilizar las direcciones asignadas a tu entorno.

La máquina objetivo debe disponer de un servicio web HTTP o HTTPS en funcionamiento. Una máquina con puertos abiertos, pero sin aplicación web, no es suficiente para completar esta actividad.

## 5. Uso de ZAP OWASP

### 5.1. Verificar si OWASP ZAP está instalado

Dependiendo de la versión, la imagen y los paquetes seleccionados durante la instalación de Kali Linux, OWASP ZAP puede encontrarse instalado o no.

Antes de descargar cualquier archivo, verifica si la herramienta ya está disponible.

Procedimiento

Paso 1. Inicia Kali Linux y accede al escritorio con tu usuario.

Paso 2. Abre el menú de aplicaciones de Kali Linux.

Paso 3. Utiliza la opción de búsqueda del menú y escribe: zap

🖼️ **ZAP OWASP_img 1**

Paso 4. Busca una aplicación identificada como OWASP ZAP, ZAP o zaproxy.

Paso 5. Si aparece la herramienta, selecciónala para iniciar su ejecución.

Paso 6. Si no aparece, abre una terminal utilizando el icono correspondiente o el método abreviado Ctrl + Alt + T, si está configurado en tu escritorio.

Paso 7. Ejecuta el siguiente comando:

```text
command -v zaproxy
```

Este comando busca el ejecutable zaproxy en las rutas configuradas del sistema operativo.

Si la herramienta está instalada y disponible, podrías obtener una respuesta como:

```text
/usr/bin/zaproxy
```

Paso 8. También puedes comprobar la instalación del paquete mediante:

```text
dpkg -s zaproxy
```

Si el paquete está instalado, normalmente aparecerá una línea similar a:

```text
Status: install ok installed
```

Resultado esperado: determinar si OWASP ZAP está disponible.

Si ZAP está instalado, continúa con la sección

### 5.3. Iniciar OWASP ZAP.

Si no está instalado, sigue el procedimiento de la sección siguiente.

### 5.2. Instalación de OWASP ZAP en Kali Linux

Kali Linux permite instalar OWASP ZAP mediante su administrador de paquetes APT.

Este es el método recomendado para esta actividad, ya que facilita la instalación de las dependencias necesarias.

Parte 1. Actualizar la información de los repositorios

Paso 1. Abre una terminal.

Paso 2. Ejecuta el siguiente comando:

```text
sudo apt update
```

Explicación del comando:

- sudo: permite ejecutar una instrucción con privilegios administrativos.

- apt: administrador de paquetes utilizado por Kali Linux.

- update: actualiza la información local sobre los paquetes disponibles en los repositorios configurados.

Paso 3. Introduce la contraseña de tu usuario si el sistema la solicita.

Mientras escribes la contraseña, es posible que no aparezcan caracteres en pantalla. Este comportamiento es normal en Linux.

Paso 4. Presiona Enter y espera a que finalice la actualización.

Resultado esperado: el sistema termina de consultar los repositorios y regresa al indicador de la terminal sin mostrar errores que impidan continuar.

Parte 2. Instalar OWASP ZAP

Paso 1. Ejecuta el siguiente comando:

```text
sudo apt install zaproxy
```

Paso 2. El sistema mostrará los paquetes que necesita descargar e instalar, junto con el espacio adicional que podría utilizar.

Paso 3. Si aparece una confirmación similar a:

```text
Do you want to continue? [Y/n]
```

escribe:

```text
Y
```

y presiona Enter.

Paso 4. Espera a que termine la descarga y la instalación.

Durante este proceso, Kali Linux instalará ZAP y resolverá las dependencias necesarias disponibles a través de APT.

Paso 5. Cuando la terminal vuelva a mostrar el indicador de comandos, verifica que no existan errores de instalación.

Parte 3. Verificar la instalación

Paso 1. Ejecuta:

```text
command -v zaproxy
```

Paso 2. Si aparece la ruta del ejecutable, continúa con la siguiente comprobación:

```text
java -version
```

ZAP utiliza Java. Las versiones modernas de la herramienta requieren un entorno Java compatible; en particular, ZAP requiere Java 17 o posterior.

Cuando se instala mediante el paquete de Kali Linux, las dependencias normalmente se resuelven automáticamente.

Paso 3. Ejecuta:

```text
zaproxy
```

Paso 4. Espera a que aparezca la pantalla inicial de OWASP ZAP.

🖼️ **ZAP OWASP_img 2**

Resultado esperado: la herramienta inicia y muestra su interfaz gráfica.

Si aparece una ventana de configuración inicial, continúa siguiendo las instrucciones de la sección 5.4.

Instalación alternativa

Si el paquete no está disponible en los repositorios configurados, puedes utilizar el instalador oficial de ZAP.

Paso 1. Abre el navegador de Kali Linux.

Paso 2. Ingresa a:

https://www.zaproxy.org/download/

Paso 3. Selecciona una distribución compatible con Linux.

Paso 4. Descarga el instalador desde el sitio oficial.

Paso 5. Si descargaste un instalador .sh, abre una terminal y dirígete a la carpeta donde se descargó el archivo:

```text
cd ~/Downloads
```

En sistemas con directorios localizados en español, utiliza la carpeta correspondiente.

Paso 6. Identifica el nombre del archivo descargado:

```text
ls -lh
```

Paso 7. Otorga permisos de ejecución al instalador, sustituyendo el nombre por el archivo real:

```text
chmod +x nombre-del-instalador.sh
```

Paso 8. Ejecuta:

```text
./nombre-del-instalador.sh
```

Paso 9. Sigue las instrucciones del asistente.

Utiliza únicamente archivos obtenidos del proyecto oficial y verifica los requisitos de Java antes de ejecutar el instalador.

Si se utilizó este método, el comando zaproxy podría no estar disponible en la terminal, dependiendo de la ubicación de instalación seleccionada.

### 5.3. Iniciar OWASP ZAP

Paso 1. Abre el menú de aplicaciones de Kali Linux.

Paso 2. Busca OWASP ZAP.

Paso 3. Selecciona la aplicación para ejecutarla.

También puedes iniciar ZAP desde una terminal con:

```text
Zaproxy
```

🖼️ **ZAP OWASP_img 3**

Paso 4. Espera mientras se cargan los módulos y complementos.

Durante el inicio podrías observar mensajes similares a:

```text
Loading extensions...
```

```text
Loading add-ons...
```

```text
Initializing ZAP...
```

🖼️ **ZAP OWASP_img 4**

Estos mensajes indican que la aplicación está cargando sus componentes.

Paso 5. No cierres la ventana de inicialización ni interrumpas el proceso.

Resultado esperado: aparece la interfaz gráfica principal de ZAP.

### 5.4. Configuración inicial de la sesión

Al iniciar, ZAP puede mostrar una ventana para configurar cómo se guardará la sesión.

Una sesión permite conservar información como sitios descubiertos, solicitudes, respuestas y alertas.

Procedimiento

Paso 1. Identifica la ventana relacionada con Persist Session.

🖼️ **ZAP OWASP_img 5**

Paso 2. Para conservar los resultados del laboratorio, selecciona la opción que permite guardar la sesión indicando un nombre y ubicación.

🖼️ **ZAP OWASP_img 6**

Paso 3. Asigna un nombre descriptivo, por ejemplo:

```text
CEHPC_Actividad05_ZAP
```

Paso 4. Selecciona una carpeta de trabajo donde puedas localizar posteriormente el archivo.

Paso 5. Confirma la configuración.

🖼️ **ZAP OWASP_img 7**

Nota: Si la versión utilizada no solicita configurar una sesión al inicio, continúa con el procedimiento. La persistencia puede configurarse posteriormente desde las opciones de sesión.

### 5.5. Identificar los elementos de la interfaz

Antes de realizar el escaneo, identifica los apartados principales de ZAP.

| Elemento | Descripción |
| --- | --- |
| Quick Start | Permite iniciar rápidamente tareas de análisis. |
| Automated Scan | Configura un escaneo automatizado de una aplicación. |
| Sites | Muestra los sitios y recursos identificados. |
| History | Muestra las solicitudes y respuestas HTTP registradas. |
| Alerts | Presenta las alertas de seguridad detectadas. |
| Spider | Muestra información de la exploración de enlaces y recursos. |
| Active Scan | Presenta el estado y los resultados de pruebas activas. |
| Request | Permite observar detalles de las solicitudes HTTP. |
| Response | Permite observar las respuestas enviadas por el servidor. |

🖼️ **ZAP OWASP_img 8**

Los elementos pueden aparecer como pestañas, paneles o apartados según la versión instalada.

Punto de control: confirma que puedes identificar Quick Start, Sites y Alerts antes de continuar.

## 6. Preparación de la aplicación objetivo

Antes de ejecutar el escaneo, es necesario comprobar que la aplicación web está disponible.

6.1. Identificar la dirección IP de Kali Linux

Paso 1. Abre una terminal.

Paso 2. Ejecuta:

```text
ip -br -4 addr
```

Este comando muestra las interfaces de red y sus direcciones IPv4.

Podrías obtener un resultado similar a:

┌──(kali㉿kali)-[~]

└─$ ip -br -4 addr

lo               UNKNOWN        127.0.0.1/8

eth0             UP             192.168.56.103/24

eth1             UP             10.0.3.15/24

Paso 3. Identifica la interfaz de red utilizada para comunicarte con la máquina objetivo.

El nombre puede variar. Algunas instalaciones muestran eth0, mientras que otras utilizan nombres como ens33.

### 6.2. Identificar la dirección de la máquina objetivo

La dirección IP puede consultarse desde la configuración de la máquina virtual o directamente desde su sistema operativo.

Si la máquina objetivo utiliza Linux y dispones de acceso autorizado a su consola, ejecuta:

```text
ip -4 addr
```

Identifica la dirección IPv4 correspondiente a la interfaz conectada a la red de laboratorio.

Registra esa dirección para utilizarla en ZAP.

Ejemplo:

```text
192.168.56.101
```

6.3. Verificar la conectividad

Paso 1. Desde Kali Linux, ejecuta:

```text
ping -c 4 192.168.56.101
```

Sustituye la dirección por la IP real de tu máquina objetivo.

Explicación:

- ping comprueba la conectividad IP utilizando mensajes ICMP.

- -c 4 limita la prueba a cuatro solicitudes.

- 192.168.56.101 representa la dirección del servidor objetivo.

Paso 2. Observa si existen respuestas del servidor.

Un resultado posible es:

┌──(kali㉿kali)-[~]

└─$ ping -c 4 192.168.56.101

PING 192.168.56.101 (192.168.56.101) 56(84) bytes of data.

64 bytes from 192.168.56.101: icmp_seq=1 ttl=64 time=0.765 ms

64 bytes from 192.168.56.101: icmp_seq=2 ttl=64 time=0.975 ms

64 bytes from 192.168.56.101: icmp_seq=3 ttl=64 time=0.577 ms

64 bytes from 192.168.56.101: icmp_seq=4 ttl=64 time=0.814 ms

--- 192.168.56.101 ping statistics ---

4 packets transmitted, 4 received, 0% packet loss, time 3081ms

rtt min/avg/max/mdev = 0.577/0.782/0.975/0.141 ms

Paso 3. Abre el navegador web.

Paso 4. Introduce la dirección completa del servicio:

```text
http://192.168.56.101
```

Paso 5. Comprueba que se muestra la aplicación web del laboratorio.

🖼️ **ZAP OWASP_img 9**

Si el servidor utiliza un puerto distinto del 80, debes incluirlo en la dirección. Por ejemplo:

```text
http://192.168.56.101:8080
```

Resultado esperado: el navegador muestra la página web del objetivo.

Importante: Algunos sistemas bloquean ICMP. Por lo tanto, una prueba ping sin respuesta no significa necesariamente que el servidor web esté apagado. La comprobación principal consiste en verificar que el servicio web responda.

## 7. Configuración y ejecución del escaneo automatizado

En este procedimiento utilizarás la opción Automated Scan de OWASP ZAP.

### 7.1. Abrir Automated Scan

Paso 1. Regresa a la ventana de OWASP ZAP.

Paso 2. Localiza la pestaña Quick Start.

Paso 3. Selecciona la opción Automated Scan.

🖼️ **ZAP OWASP_img 10**

Paso 4. Identifica el campo URL to attack.

Este campo permite indicar la dirección de la aplicación que será analizada.

🖼️ **ZAP OWASP_img 11**

7.2. Configurar el objetivo

Paso 1. En el campo URL to attack, introduce la dirección de la aplicación.

Ejemplo:

```text
http://192.168.56.101
```

🖼️ **ZAP OWASP_img 12**

Paso 2. Verifica que la dirección comience con http:// o https://, según el protocolo utilizado por el servicio.

Paso 3. Comprueba que la dirección pertenece a la máquina de laboratorio autorizada.

Paso 4. Si la aplicación está alojada en una ruta específica, incluye la ruta correspondiente.

Ejemplo:

```text
http://192.168.56.101/aplicacion/
```

Paso 5. Si aparece una opción denominada Use traditional spider, mantenla habilitada para que ZAP pueda explorar los enlaces de la aplicación.

🖼️ **ZAP OWASP_img 13**

Paso 6. Si aparece Use ajax spider, utiliza la configuración indicada para el entorno. Esta opción es útil para aplicaciones que generan contenido dinámicamente con JavaScript, pero puede incrementar el tiempo de ejecución.

Para esta actividad básica es suficiente utilizar Traditional Spider. Si la opción AJAX Spider está habilitada, puedes desactivarla para simplificar la exploración inicial.

### 7.3. Iniciar el escaneo

Paso 1. Comprueba nuevamente que la dirección configurada corresponde al objetivo autorizado.

Paso 2. Localiza el botón Attack.

Paso 3. Haz clic en Attack.

🖼️ **ZAP OWASP_img 14**

Paso 4. Observa el indicador de progreso.

Durante la ejecución, ZAP puede realizar las siguientes operaciones:

1. Establecer comunicación con el servidor web.

2. Solicitar recursos de la aplicación.

3. Explorar enlaces y rutas mediante Spider.

4. Registrar las solicitudes y respuestas HTTP.

5. Ejecutar pruebas activas para identificar posibles vulnerabilidades.

6. Generar alertas de seguridad cuando encuentre determinados comportamientos o configuraciones.

Paso 5. Espera a que finalicen las tareas de exploración y escaneo activo.

Puedes observar el avance en las pestañas relacionadas con Spider y Active Scan.


🖼️ **ZAP OWASP_img 15**

Paso 6. No cierres ZAP mientras el análisis siga ejecutándose.

⚠️Se paciente, el análisis tomara varios minutos, puedes verificar la barra de avance

🖼️ **ZAP OWASP_img 16**

🚩 Si necesitas detenerlo porque introdujiste un objetivo incorrecto, utiliza el botón Stop o la opción correspondiente a detener el escaneo.

Resultado esperado: ZAP presenta la aplicación en Sites, registra solicitudes HTTP y permite consultar los resultados del análisis.

La duración depende del tamaño de la aplicación, sus respuestas, la configuración seleccionada y los recursos disponibles.

## 8. Visualización de las consultas realizadas por ZAP

Cuando ZAP interactúa con una aplicación web, registra las solicitudes realizadas y las respuestas recibidas.

Estas operaciones pueden examinarse desde History.

### 8.1. Acceder al historial

Paso 1. Localiza la pestaña History.

Paso 2. Selecciónala.

Paso 3. Observa la lista de solicitudes registradas durante el escaneo.

Entre las columnas que puedes encontrar se incluyen:

| Campo | Descripción |
| --- | --- |
| Method | Método HTTP utilizado para enviar la solicitud. |
| URL | Dirección del recurso solicitado. |
| Code | Código de respuesta del servidor. |
| Reason | Descripción asociada al código HTTP. |
| RTT | Tiempo de respuesta de la solicitud. |
| Highest Alert | Riesgo más alto de las alertas relacionadas con la solicitud, cuando corresponda. |

### 8.2. Interpretar las solicitudes HTTP

Durante el análisis puedes observar métodos como:

GET

Se utiliza habitualmente para solicitar información o recursos de un servidor.

POST

Se utiliza para enviar datos al servidor, por ejemplo, mediante formularios.

🖼️ **ZAP OWASP_img 17**

También es posible encontrar otros métodos HTTP según las características de la aplicación.

Códigos de respuesta frecuentes

| Código | Significado |
| --- | --- |
| 200 | La solicitud se procesó correctamente. |
| 301 | El recurso tiene una redirección permanente. |
| 302 | El servidor indica una redirección temporal. |
| 403 | El servidor rechaza el acceso al recurso. |
| 404 | El recurso solicitado no fue encontrado. |
| 500 | El servidor encontró un error interno. |

Los códigos anteriores describen respuestas HTTP. Por sí solos no permiten confirmar vulnerabilidades.

### 8.3. Examinar una solicitud

Paso 1. Selecciona una de las entradas mostradas en History.

Paso 2. Localiza el apartado Request.

🖼️ **ZAP OWASP_img 18**

Paso 3. Observa la información de la solicitud HTTP.

Ejemplo ilustrativo:

🖼️ **ZAP OWASP_img 19**

Paso 4. Selecciona el apartado Response.

Paso 5. Identifica el código HTTP y las cabeceras enviadas por el servidor.

Ejemplo:

```text
HTTP/1.1 200 OK
```

```text
Content-Type: text/html

```

Paso 6. Repite la observación con otras solicitudes para familiarizarte con los registros generados.

Resultado esperado: reconocer los métodos HTTP, las direcciones solicitadas y las respuestas obtenidas durante la exploración.

## 9. Análisis de vulnerabilidades mediante Alerts

La sección Alerts permite examinar los problemas de seguridad identificados por ZAP.

Las alertas representan posibles vulnerabilidades, configuraciones inseguras o información relevante encontrada durante el análisis.

### 9.1. Acceder a las alertas

Paso 1. Localiza la pestaña Alerts.

Paso 2. Selecciónala.

Paso 3. Observa las alertas disponibles.

🖼️ **ZAP OWASP_img 20**

Paso 4. Si las alertas están organizadas por categorías, expande la clasificación correspondiente para observar sus detalles.

Paso 5. Selecciona una de las alertas para mostrar su información.

🖼️ **ZAP OWASP_img 21**

### 9.2. Identificar el nivel de riesgo

ZAP utiliza categorías para identificar la severidad de las alertas.

| Nivel | Interpretación |
| --- | --- |
| High | Problema potencial de seguridad de severidad alta. |
| Medium | Problema potencial de severidad media. |
| Low | Problema potencial de severidad baja. |
| Informational | Información relevante que no necesariamente representa una vulnerabilidad. |

La clasificación depende del tipo de hallazgo y de la evaluación que realiza ZAP.

Una alerta de severidad alta no significa automáticamente que el sistema pueda ser comprometido. La confirmación requiere revisar su evidencia y comprobar las condiciones bajo las cuales fue identificada.

### 9.3. Revisar los detalles de una alerta

Paso 1. Selecciona una alerta.

Paso 2. Localiza el nombre de la vulnerabilidad o problema identificado.

Paso 3. Examina su nivel de riesgo.

Paso 4. Revisa el nivel de confianza indicado por la herramienta, si está disponible.

El nivel de confianza representa qué tan seguro está ZAP de haber identificado correctamente la condición reportada. No es equivalente a la severidad del problema.

Paso 5. Examina la descripción técnica.

Paso 6. Identifica la URL o recurso relacionado con el hallazgo.

Paso 7. Revisa el campo Evidence, cuando aparezca.

Este campo puede mostrar información utilizada por ZAP para generar la alerta.

Paso 8. Revisa la sección Solution o su equivalente.

Esta sección contiene recomendaciones generales de mitigación.

Paso 9. Si aparece una referencia CWE, CVE u otra clasificación, registra su identificador para facilitar la consulta técnica posterior.

🖼️ **ZAP OWASP_img 22**

### 9.4. Ejemplo de interpretación

Supongamos que ZAP genera una alerta con las siguientes características:

Alert: X-Content-Type-Options Header Missing

Risk: Low

Confidence: Medium

URL: http://192.168.56.101/

Este resultado indica que ZAP detectó la ausencia de una cabecera HTTP de seguridad en la respuesta analizada.

No indica que la aplicación haya sido comprometida.

La revisión técnica consiste en identificar el recurso afectado, observar la evidencia disponible y consultar las recomendaciones asociadas.

Resultado esperado: identificar al menos una alerta y examinar sus detalles, si el objetivo presenta hallazgos.

Si el escaneo no genera alertas, registra ese resultado. No debes modificar los resultados ni considerar que necesariamente existió un error.

## 10. Exploración de recursos mediante Spider

Spider es una función de ZAP utilizada para identificar recursos de una aplicación web mediante la exploración de enlaces y referencias disponibles.

Durante la exploración, ZAP puede descubrir páginas, archivos, rutas y otros recursos relacionados con la aplicación.

No todos los recursos identificados corresponden a directorios físicos del servidor.

### 10.1. Acceder a Spider

Paso 1. Localiza la pestaña Spider en la parte inferior de la interfaz.

Paso 2. Selecciónala.

Paso 3. Observa los resultados asociados con la exploración realizada.

Dependiendo de la versión de ZAP, podrás visualizar información relacionada con el progreso, las solicitudes y las direcciones descubiertas.

### 10.2. Revisar los recursos identificados

Paso 1. Observa las direcciones URL registradas.

Paso 2. Identifica las rutas que pertenecen a la aplicación objetivo.

Ejemplos ilustrativos:

🖼️ **ZAP OWASP_img 23**

Paso 3. Comprueba que las rutas corresponden al objetivo autorizado.

Paso 4. Examina el método HTTP asociado con cada recurso, cuando esté disponible.

Paso 5. Identifica los códigos de respuesta obtenidos.

### 10.3. Consultar los recursos en Sites

Paso 1. Localiza el panel Sites.

Paso 2. Identifica la dirección IP o nombre del servidor analizado.

Paso 3. Haz clic en el control que permite expandir los recursos del servidor.

Paso 4. Observa la estructura de rutas descubiertas.

Paso 5. Selecciona alguno de los recursos para revisar la información asociada.

Resultado esperado: visualizar los recursos que ZAP pudo descubrir mediante las técnicas de exploración utilizadas.

Importante: Spider no garantiza descubrir todos los recursos de la aplicación. Algunos pueden requerir autenticación, interacción con formularios o mecanismos dinámicos de navegación.

🖼️ **ZAP OWASP_img 24**

### 11. Guardar los resultados y evidencias

Al finalizar el escaneo, conserva las evidencias necesarias para demostrar que la actividad se realizó correctamente.

### 11.1. Evidencias requeridas

Prepara las siguientes capturas de pantalla:

| Evidencia | Contenido |
| --- | --- |
| 01 | Interfaz principal de OWASP ZAP en funcionamiento. |
| 02 | Dirección configurada para el escaneo. |
| 03 | Solicitudes HTTP registradas en History. |
| 04 | Alertas de seguridad mostradas en Alerts. |
| 05 | Recursos identificados mediante Spider o Sites. |

Si alguna sección no presenta resultados, captura el estado correspondiente.

### 11.2. Organizar las evidencias

Paso 1. Abre una terminal.

Paso 2. Crea una carpeta para almacenar la actividad:

```text
mkdir -p ~/CEHPC/Actividad05_ZAP/Evidencias
```

Paso 3. Accede a la carpeta principal:

```text
cd ~/CEHPC/Actividad05_ZAP
```

Paso 4. Guarda las capturas de pantalla en Evidencias.

Puedes asignar nombres como:

- 01_ZAP_Iniciado.png

- 02_Escaneo_Configurado.png

- 03_History.png

- 04_Alerts.png

- 05_Spider.png

11.3. Exportar un reporte

Si tu instalación de ZAP dispone de la función de generación de reportes:

Paso 1. Abre el menú Report.

Paso 2. Localiza la opción Generate Report o una equivalente.

Paso 3. Selecciona la plantilla de reporte HTML disponible.

Paso 4. Comprueba que el informe incluya únicamente el objetivo de laboratorio autorizado.

Paso 5. Selecciona la carpeta de destino.

Paso 6. Genera y guarda el reporte.

Resultado esperado: disponer de un archivo HTML que puedas abrir posteriormente para consultar los resultados del análisis.

La ubicación exacta de las opciones de reporte puede variar según la versión y los complementos instalados.

## 12. Solución de problemas frecuentes

### Problema 1. OWASP ZAP no aparece en Kali Linux

Posible causa: la herramienta no está instalada o no existe un acceso directo en el menú.

Solución:

Abre una terminal y ejecuta:

```text
command -v zaproxy
```

Si no aparece una ruta, comprueba la instalación con:

```text
dpkg -s zaproxy
```

Si el paquete no está instalado, ejecuta:

```text
sudo apt update
```

```text
sudo apt install zaproxy
```

Problema 2. El sistema indica que no encuentra el paquete zaproxy

Posible causa: el índice de paquetes no está actualizado o los repositorios no están configurados correctamente.

Solución:

Primero ejecuta:

```text
sudo apt update
```

Después comprueba la disponibilidad del paquete:

```text
apt-cache policy zaproxy
```

Si no aparece una versión candidata, revisa que Kali Linux tenga configurados sus repositorios oficiales y que exista conectividad a Internet.

No agregues repositorios de distribuciones diferentes para intentar resolver el problema.

Problema 3. ZAP no inicia correctamente

Posibles causas:

Dependencias incompletas.

Java incompatible.

Recursos insuficientes.

Problemas en la instalación.

Solución:

Comprueba Java:

```text
java -version
```

Después intenta iniciar ZAP desde la terminal:

```text
zaproxy
```

Examina los mensajes de error para identificar la causa.

Si la instalación se realizó con APT, puedes comprobar las dependencias mediante:

```text
sudo apt --fix-broken install
```

Problema 4. El escaneo no comienza

Posibles causas:

- Dirección URL incorrecta.

- Aplicación objetivo apagada.

- Puerto incorrecto.

- Problemas de conectividad.

- Servidor web no disponible.

Solución:

Comprueba que la URL incluya el protocolo correcto.

Por ejemplo:

```text
http://192.168.56.101
```

Después intenta abrir la dirección en el navegador.

Si la aplicación no responde, revisa la configuración de red y el servicio web del objetivo antes de volver a ejecutar el escaneo.

Problema 5. Spider no encuentra recursos

Posibles causas:

- La aplicación contiene pocos enlaces.

- Las rutas requieren autenticación.

- La navegación depende de JavaScript.

- La aplicación no responde correctamente.

- La configuración de alcance excluye determinados recursos.

Solución:

Comprueba que la aplicación pueda abrirse desde el navegador.

Verifica que Traditional Spider esté habilitado y que la URL inicial sea correcta.

Si la aplicación utiliza navegación dinámica, consulta la disponibilidad de AJAX Spider. No es obligatorio activarlo para completar la exploración básica.

Problema 6. No aparecen alertas

Posibles causas:

- El análisis activo no ha finalizado.

- No se detectaron problemas mediante las reglas ejecutadas.

- La aplicación tiene pocos recursos disponibles.

- Algunas reglas o complementos no están habilitados.

Solución:

Comprueba el estado de Active Scan.

Revisa el historial para confirmar que ZAP realizó solicitudes.

Si el escaneo finalizó correctamente, pero no se generaron alertas, conserva ese resultado como evidencia.

La ausencia de alertas no demuestra que una aplicación esté completamente libre de vulnerabilidades.

Problema 7. Los resultados son diferentes a los ejemplos

Los resultados pueden cambiar por:

- Versión de ZAP.

- Complementos instalados.

- Configuración del escaneo.

- Sistema operativo utilizado.

- Aplicación web analizada.

- Servicios y vulnerabilidades disponibles en el objetivo.

Solución:

Comprueba que el procedimiento se ejecutó correctamente y que estás analizando el objetivo asignado.

No es necesario obtener exactamente el mismo número de solicitudes, recursos o alertas para completar la actividad.

## 13. Finalización de la actividad

La actividad se considera finalizada cuando se han completado las siguientes operaciones:

- Verificación o instalación de OWASP ZAP.

- Inicio correcto de la herramienta.

- Comprobación de conectividad con la aplicación web.

- Configuración de la dirección objetivo.

- Ejecución del escaneo automatizado.

- Consulta de las solicitudes HTTP.

- Revisión de Alerts.

- Revisión de Spider y Sites.

- Almacenamiento de las evidencias.

- Generación del reporte, si la función está disponible.

Antes de cerrar, comprueba que no existan escaneos activos en ejecución. Guarda la sesión cuando corresponda y cierra OWASP ZAP.

Si se utilizó una máquina vulnerable, puedes apagarla o restaurarla al estado inicial del laboratorio según las indicaciones del entorno.

Resultado de la actividad

Mediante OWASP ZAP habrás realizado un análisis automatizado de una aplicación web de laboratorio, observado las comunicaciones HTTP generadas, consultado los recursos descubiertos y examinado los posibles problemas de seguridad identificados.

La información obtenida puede utilizarse como evidencia técnica durante las actividades de análisis de vulnerabilidades y elaboración de informes de resultados.

Referencias técnicas

- OWASP ZAP: https://www.zaproxy.org/

- Descarga de ZAP: https://www.zaproxy.org/download/

- Documentación de OWASP ZAP: https://www.zaproxy.org/docs/

- Kali Linux: https://www.kali.org/

- Paquete ZAP para Kali Linux: https://www.kali.org/tools/zaproxy/

- OWASP Web Security Testing Guide: https://owasp.org/www-project-web-security-testing-guide/
