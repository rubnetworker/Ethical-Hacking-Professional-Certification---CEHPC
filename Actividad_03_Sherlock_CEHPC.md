# Ethical Hacking

## Actividad 03. Sherlock

**Ethical Hacking Professional Certification (CEHPC)**

| Característica | Descripción |
|---|---|
| **Duración estimada** | 45 a 60 minutos |
| **Nivel** | Básico |
| **Modalidad** | Presencial o autónoma |
| **Sistema operativo** | Kali Linux |
| **Herramienta principal** | Sherlock |
| **Tema** | Reconocimiento pasivo y recopilación de información mediante OSINT |

---

# 1. Introducción

Sherlock es una herramienta de código abierto diseñada para buscar información sobre nombres de usuario en diversas redes sociales y plataformas en línea. Se utiliza comúnmente en pruebas de penetración, auditorías de seguridad y actividades de investigación para recopilar información sobre un objetivo específico.

En Ethical Hacking, Sherlock se utiliza principalmente durante la fase de **reconocimiento pasivo**, que consiste en recopilar información disponible públicamente sin intentar acceder de manera no autorizada a los sistemas investigados.

Esta técnica forma parte de **OSINT (*Open Source Intelligence*)**, también conocida como inteligencia de fuentes abiertas. OSINT permite recopilar y analizar información procedente de fuentes públicas, como sitios web, motores de búsqueda, redes sociales, documentos y otras plataformas disponibles en Internet.

## 1.1. Funcionamiento de Sherlock

Sherlock automatiza la búsqueda de un mismo nombre de usuario en diferentes plataformas. Por ejemplo, una persona podría utilizar el identificador `usuario_ejemplo` en distintos servicios de Internet.

La herramienta consulta las plataformas compatibles para determinar si ese identificador podría estar registrado. Una salida ilustrativa sería:

```text
[*] Checking username usuario_ejemplo on:

[+] GitHub: https://github.com/usuario_ejemplo
[+] Reddit: https://www.reddit.com/user/usuario_ejemplo
[+] Pinterest: https://www.pinterest.com/usuario_ejemplo

[*] Search completed
```

> **Nota:** La salida anterior es ilustrativa y no corresponde a una búsqueda real. El formato exacto depende de la versión instalada.

Sherlock busca coincidencias de **nombres de usuario**, no identifica directamente personas. Que dos perfiles compartan un identificador no demuestra que pertenezcan al mismo propietario.

## 1.2. Importancia de Sherlock en Ethical Hacking

Durante una evaluación de seguridad, el reconocimiento permite identificar información pública útil para comprender la exposición digital de una persona u organización. La reutilización de un nombre de usuario en distintas plataformas podría facilitar la correlación de perfiles públicos.

Sherlock no es una herramienta de explotación de vulnerabilidades ni permite, por sí misma, acceder a contraseñas o cuentas privadas.

---

# 2. Objetivos

El objetivo principal de utilizar Sherlock en Kali Linux es recopilar información sobre un objetivo específico mediante la búsqueda de perfiles de usuario en diferentes plataformas en línea. Esta información puede ayudar a comprender la superficie de exposición digital y posibles riesgos para la privacidad.

Al finalizar esta actividad, el participante será capaz de:

1. Identificar la función de Sherlock en una actividad de reconocimiento pasivo.
2. Preparar Kali Linux para ejecutar la herramienta.
3. Instalar Sherlock mediante `pipx`.
4. Ejecutar búsquedas de nombres de usuario en diferentes plataformas.
5. Interpretar los resultados e identificar posibles coincidencias.
6. Guardar evidencias de las búsquedas realizadas.
7. Reconocer las limitaciones de Sherlock.

**Resultado esperado:** Ejecutar Sherlock en Kali Linux, realizar una búsqueda autorizada y reconocer las plataformas en las que el nombre de usuario podría encontrarse registrado.

---

# 3. Alcance

Sherlock tiene como alcance principal la búsqueda de nombres de usuario en redes sociales y plataformas compatibles.

Durante esta actividad se realizarán las siguientes operaciones:

- Instalación y ejecución de Sherlock en Kali Linux.
- Búsqueda de nombres de usuario propios o expresamente autorizados.
- Identificación de posibles perfiles públicos.
- Revisión e interpretación de resultados.
- Almacenamiento de evidencias de la actividad.

## 3.1. Consideraciones de seguridad y autorización

Esta práctica tiene fines educativos. Utiliza preferentemente un identificador propio, una cuenta creada para prácticas o un nombre de usuario cuya investigación haya sido autorizada.

La actividad no contempla acceso a cuentas privadas, obtención de contraseñas, modificación de información, explotación de vulnerabilidades ni otras acciones fuera del reconocimiento público autorizado.

> **Importante:** Los resultados son posibles coincidencias, no confirmaciones de identidad.

---

# 4. Herramientas Utilizadas

## 4.1. Sherlock

Herramienta de código abierto que permite buscar nombres de usuario en múltiples plataformas.

**Repositorio oficial:** https://github.com/sherlock-project/sherlock

## 4.2. Kali Linux

Distribución de Linux orientada a actividades de ciberseguridad, auditoría de sistemas y pruebas de penetración.

**Sitio oficial:** https://www.kali.org/

## 4.3. Terminal de Linux

Interfaz que permite interactuar con el sistema operativo mediante instrucciones escritas, denominadas *comandos*. Se utilizará para instalar Sherlock, ejecutar búsquedas y guardar resultados.

## 4.4. Requisitos previos

- Computadora física o virtual con Kali Linux funcionando.
- Conexión a Internet.
- Usuario de Kali Linux con permisos para instalar paquetes.
- Acceso a una terminal.
- Espacio disponible para instalar las herramientas necesarias.

> Si todavía no tienes Kali Linux, prepara primero el entorno de trabajo mediante la guía de instalación correspondiente al curso.

---

# 5. Instalación

En este procedimiento se utilizará **un único método de instalación: `pipx`**. No es necesario clonar el repositorio ni instalar dependencias de Python manualmente.

## 5.1. Abrir la terminal de Kali Linux

**Paso 1.** Inicia Kali Linux con tu usuario y contraseña.

**Paso 2.** Localiza el icono de la terminal en el escritorio o abre **Terminal Emulator** desde el menú de aplicaciones.

**Paso 3.** Abre la terminal. Escribe cada comando como aparece y presiona **Enter** para ejecutarlo.

**Resultado esperado:** La terminal está abierta y lista para recibir comandos.

## 5.2. Verificar la conexión a Internet

**Paso 1.** Ejecuta:

```bash
ping -c 4 github.com
```

**Explicación:** `ping` comprueba la comunicación; `-c 4` envía cuatro solicitudes; `github.com` es el dominio de referencia.

**Paso 2.** Espera a que termine. Si el destino responde a ICMP, aparecerán líneas semejantes a:

```text
64 bytes from ...: icmp_seq=1 ttl=... time=...
64 bytes from ...: icmp_seq=2 ttl=... time=...
```

Los valores variarán. La ausencia de respuesta no demuestra por sí sola que no exista Internet, porque ICMP puede estar bloqueado.

**Paso 3.** Como comprobación de acceso HTTPS, ejecuta:

```bash
curl -I https://github.com
```

**Resultado esperado:** Se muestran encabezados HTTP. Si `curl` no está disponible, abre `https://github.com` desde el navegador. Si falla la conexión, revisa la red de Kali Linux antes de continuar.

## 5.3. Actualizar el índice de paquetes

**Paso 1.** Ejecuta:

```bash
sudo apt update
```

**Paso 2.** Introduce tu contraseña si se solicita. Es normal que no aparezcan caracteres al escribirla.

**Explicación:** `sudo` otorga privilegios administrativos, `apt` administra paquetes y `update` actualiza la información de los repositorios.

**Resultado esperado:** El proceso termina sin errores. Este comando actualiza el **índice de paquetes**, no todos los programas del sistema.

## 5.4. Instalar pipx

**Paso 1.** Ejecuta:

```bash
sudo apt install pipx -y
```

**Explicación:** `apt install` instala el paquete `pipx`; `-y` acepta las confirmaciones del administrador de paquetes.

**Paso 2.** Verifica la instalación:

```bash
pipx --version
```

**Resultado esperado:** Aparece un número de versión de `pipx`.

## 5.5. Configurar pipx

**Paso 1.** Ejecuta:

```bash
pipx ensurepath
```

Este comando ayuda a incorporar el directorio de ejecutables de `pipx` a la variable de entorno `PATH`.

**Paso 2.** Cierra la terminal y abre una nueva para aplicar cualquier cambio en la configuración del entorno.

**Resultado esperado:** El entorno está preparado para localizar los ejecutables instalados con `pipx`.

## 5.6. Instalar Sherlock

**Paso 1.** Ejecuta:

```bash
pipx install sherlock-project
```

**Explicación:** `pipx` administra aplicaciones Python, `install` instala una aplicación y `sherlock-project` identifica el paquete de Sherlock.

**Paso 2.** Espera a que termine la instalación. No es necesario ejecutar `sudo` con este comando.

**Paso 3.** Comprueba los paquetes instalados:

```bash
pipx list
```

**Resultado esperado:** Aparece `sherlock-project` y su comando disponible `sherlock`.

> Si `pipx` indica que Sherlock ya está instalado, no necesitas repetir la instalación. Continúa con la validación.

## 5.7. Validar la instalación

**Paso 1.** Ejecuta:

```bash
sherlock --help
```

**Resultado esperado:** Se muestra el menú de ayuda y las opciones compatibles con la versión instalada.

**Paso 2.** Consulta la versión:

```bash
sherlock --version
```

**Resultado esperado:** Aparece la información de versión. Si la ejecución indica que la opción no está disponible, utiliza `sherlock --help` como comprobación principal y revisa la versión del paquete con `pipx list`.

## 5.8. Preparar el directorio de trabajo

**Paso 1.** Crea la carpeta para evidencias:

```bash
mkdir -p ~/CEHPC/Actividad03/evidencias
```

**Explicación:** `mkdir` crea directorios y `-p` permite crear los directorios intermedios que falten.

**Paso 2.** Comprueba que exista:

```bash
ls ~/CEHPC/Actividad03
```

**Resultado esperado:** Aparece `evidencias`.

**Paso 3.** Entra a la carpeta:

```bash
cd ~/CEHPC/Actividad03/evidencias
```

**Paso 4.** Consulta tu ubicación:

```bash
pwd
```

**Resultado esperado:** Una ruta similar a `/home/kali/CEHPC/Actividad03/evidencias`. El nombre del usuario puede ser diferente.

## 5.9. Comprobar el funcionamiento de Sherlock

**Paso 1.** Ejecuta una consulta con un identificador propio o autorizado, sustituyendo el texto de ejemplo:

```bash
sherlock usuario_ejemplo
```

**Paso 2.** Espera hasta que termine el proceso y revisa la terminal.

**Resultado esperado:** Sherlock completa sus consultas y muestra posibles coincidencias, si existen. No es indispensable encontrar resultados positivos para validar la ejecución.

**Instalación completada:** Si Sherlock muestra su ayuda y finaliza una consulta sin errores, continúa con el ejercicio.

---

# 6. Ejercicio

## 6.1. Búsqueda de nombres de usuario mediante Sherlock

En esta actividad se utilizará Sherlock para buscar un identificador propio o autorizado en las plataformas compatibles.

El formato de ejecución es:

```bash
sherlock nombre_usuario
```

> **Importante:** Sherlock busca **nombres de usuario**. Utiliza un identificador como `usuario123` en lugar de un nombre completo con espacios.

### Paso 1. Seleccionar el nombre de usuario

Elige un nombre de usuario propio o expresamente autorizado. No es necesario que esté registrado en todas las plataformas.

### Paso 2. Verificar la disponibilidad de Sherlock

Abre una terminal y ejecuta:

```bash
sherlock --help
```

Si se presenta el menú de ayuda, continúa.

### Paso 3. Ejecutar la búsqueda

Sustituye `usuario_ejemplo` por el identificador seleccionado:

```bash
sherlock usuario_ejemplo
```

Presiona **Enter**. Sherlock iniciará la consulta de plataformas compatibles.

### Paso 4. Esperar a que finalice el proceso

No cierres la terminal. La duración dependerá de la conexión a Internet y de la disponibilidad de los sitios consultados.

### Paso 5. Identificar los resultados

Una salida ilustrativa es:

```text
[*] Checking username usuario_ejemplo on:

[+] GitHub: https://github.com/usuario_ejemplo
[+] Reddit: https://www.reddit.com/user/usuario_ejemplo
[+] Pinterest: https://www.pinterest.com/usuario_ejemplo

[*] Search completed
```

**Nota:** Los enlaces son ejemplos de formato, no coincidencias verificadas. La presentación puede variar entre versiones.

### Paso 6. Interpretar los resultados

| Elemento | Significado |
|---|---|
| **Plataforma** | Servicio en el que se detectó una posible coincidencia. |
| **Dirección URL** | Enlace asociado al identificador consultado. |
| **Resultado positivo** | Sherlock detectó indicios de que el identificador existe. |
| **Resultado negativo** | No se detectó el identificador con el método empleado. |
| **Error de consulta** | No fue posible determinar el resultado de una plataforma. |

Una coincidencia positiva no demuestra que la cuenta pertenezca a una persona determinada. Una ausencia de resultados tampoco garantiza que el identificador no exista. Algunas plataformas bloquean consultas automatizadas o cambian sus mecanismos de respuesta.

### Paso 7. Analizar una búsqueda de referencia

Para reconocer la estructura de los resultados se considera el identificador de ejemplo:

```text
angelortia
```

La sintaxis de consulta sería:

```bash
sherlock angelortia
```

Una ejecución de referencia ha mostrado coincidencias asociadas a plataformas como 8tracks, Academia.edu, Docker Hub, Fiverr, G2G, Twitter, Virgool, WhoNix Forum, ebio.gg y Metacritic.

**No es necesario reproducir las mismas coincidencias.** La disponibilidad de perfiles y los mecanismos de búsqueda cambian con el tiempo. Estas referencias no acreditan que todos los perfiles pertenezcan a la misma persona.

### Paso 8. Guardar los resultados

**Paso 1.** Comprueba que existe el directorio de evidencias:

```bash
mkdir -p ~/CEHPC/Actividad03/evidencias
```

**Paso 2.** Ejecuta una nueva búsqueda con salida a un archivo:

```bash
sherlock usuario_ejemplo --output ~/CEHPC/Actividad03/evidencias/resultados.txt
```

Reemplaza `usuario_ejemplo` por el identificador autorizado.

**Paso 3.** Comprueba los archivos generados:

```bash
ls -l ~/CEHPC/Actividad03/evidencias/
```

**Paso 4.** Si `resultados.txt` existe, visualízalo:

```bash
cat ~/CEHPC/Actividad03/evidencias/resultados.txt
```

**Resultado esperado:** Aparece el contenido de resultados guardado por Sherlock. Si no hay coincidencias, el archivo podría estar vacío según el comportamiento de la versión.

### Paso 9. Documentar las evidencias

Conserva:

1. **Instalación:** captura del comando `sherlock --help` y su salida.
2. **Ejecución:** captura del comando de búsqueda utilizado.
3. **Resultados:** captura de las coincidencias encontradas o de la finalización sin coincidencias.
4. **Archivo:** `resultados.txt`, si fue generado.

No publiques en GitHub evidencias que contengan datos personales sin permiso. Para compartir la actividad, utiliza identificadores ficticios y resultados de ejemplo, o elimina los datos sensibles de las capturas.

## 6.2. Problemas frecuentes y soluciones

### Problema 1. `sherlock: command not found`

**Causa probable:** La herramienta no está instalada o la ruta del ejecutable no se encuentra en `PATH`.

**Solución:**

```bash
pipx list
```

Si no aparece `sherlock-project`, ejecuta:

```bash
pipx install sherlock-project
```

Si ya aparece instalado, ejecuta:

```bash
pipx ensurepath
```

Cierra y abre la terminal; luego comprueba:

```bash
sherlock --help
```

### Problema 2. `Permission denied` durante la instalación

**Causa probable:** La operación requiere permisos administrativos.

Para instalar `pipx` mediante `apt`, utiliza:

```bash
sudo apt install pipx -y
```

Introduce la contraseña solicitada. La instalación de Sherlock mediante `pipx` debe realizarse normalmente **sin** `sudo`:

```bash
pipx install sherlock-project
```

### Problema 3. No es posible descargar paquetes

**Mensajes posibles:**

```text
Temporary failure in name resolution
Could not resolve host
```

**Solución:** Comprueba la conectividad:

```bash
ping -c 4 github.com
```

Si no responde, intenta también la prueba HTTPS de la sección 5.2. Verifica DNS, conectividad de Kali Linux y la configuración del adaptador de red de la máquina virtual.

### Problema 4. Sherlock no encuentra usuarios

**Posibles causas:** El identificador no existe en las plataformas compatibles, está mal escrito, los servicios no respondieron o la herramienta requiere una actualización.

Comprueba que Sherlock funciona:

```bash
sherlock --help
```

Si está instalado mediante `pipx`, puedes actualizarlo con:

```bash
pipx upgrade sherlock-project
```

La ausencia de coincidencias no implica necesariamente un error de instalación.

### Problema 5. Los resultados son diferentes al ejemplo

Los perfiles y las respuestas de las plataformas cambian. No es necesario obtener el mismo número de resultados ni las mismas URLs. Comprueba que la consulta finalice y revisa las coincidencias que proporcione tu versión.

## 6.3. Finalización de la actividad

La actividad se considera completada cuando el participante:

1. Preparó el entorno de Kali Linux.
2. Instaló Sherlock mediante `pipx`.
3. Comprobó el funcionamiento mediante `sherlock --help`.
4. Ejecutó una búsqueda autorizada.
5. Identificó e interpretó los resultados.
6. Guardó los resultados en un archivo cuando estuvieron disponibles.
7. Conservó las evidencias de la ejecución.

### Resultado final esperado

La carpeta de trabajo tendrá una estructura similar a:

```text
/home/kali/
└── CEHPC/
    └── Actividad03/
        └── evidencias/
            └── resultados.txt
```

También puedes guardar en `evidencias` las capturas de pantalla. No es indispensable encontrar un número determinado de perfiles para completar correctamente la práctica.

## 6.4. Conclusiones

Sherlock es una herramienta de código abierto que facilita la recopilación de información pública relacionada con nombres de usuario en diversas plataformas de Internet.

Durante esta actividad se preparó Kali Linux, se instaló Sherlock, se ejecutaron búsquedas y se interpretaron posibles coincidencias.

La práctica permitió comprender cómo la reutilización de un identificador puede contribuir a la correlación de perfiles y por qué los resultados automatizados requieren validación: pueden existir falsos positivos, información desactualizada o respuestas incompletas.

En Ethical Hacking, los hallazgos de Sherlock pueden incorporarse a una investigación OSINT más amplia, siempre dentro de un alcance autorizado y con un tratamiento responsable de la información.

---

## Referencias técnicas

- [Sherlock Project — Repositorio oficial](https://github.com/sherlock-project/sherlock)
- [Kali Linux — Documentación oficial](https://www.kali.org/docs/)
- [pipx — Documentación](https://pipx.pypa.io/)
