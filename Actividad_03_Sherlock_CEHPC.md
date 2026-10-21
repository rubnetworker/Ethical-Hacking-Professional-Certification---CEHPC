# Actividad 03. Sherlock

## Ethical Hacking Professional Certification (CEHPC)

| Información | Detalle |
|---|---|
| **Duración estimada** | 50–60 minutos |
| **Nivel** | Básico |
| **Herramienta** | Shodan |
| **Herramienta principal:** | Sherlock  |
| **Tema:** | Reconocimiento pasivo y recopilación de información mediante OSINT |


## 1. Introducción

Sherlock es una herramienta de código abierto diseñada para buscar información sobre nombres de usuario en diversas redes sociales y plataformas en línea. Se utiliza comúnmente en pruebas de penetración, auditorías de seguridad y actividades de investigación para recopilar información sobre un objetivo específico.

En el contexto de Ethical Hacking, Sherlock se utiliza principalmente durante la fase de **reconocimiento pasivo**, que consiste en recopilar información disponible públicamente sin intentar acceder de manera no autorizada a los sistemas investigados.

Esta técnica forma parte de OSINT (*Open Source Intelligence*), también conocida como inteligencia de fuentes abiertas.

OSINT permite recopilar y analizar información procedente de fuentes públicas, como sitios web, motores de búsqueda, redes sociales, documentos y otras plataformas disponibles en Internet.

<img width="1672" height="941" alt="1 Infografía OSINT_ Fuentes Abiertas en Red" src="https://github.com/user-attachments/assets/cc51161a-3c51-4336-a724-45bccdd52f51" />


### 1.1. Funcionamiento de Sherlock

Sherlock automatiza la búsqueda de un mismo nombre de usuario en diferentes plataformas.

Por ejemplo, una persona podría utilizar el nombre de usuario usuario_ejemplo en diferentes servicios de Internet.

Sherlock realiza consultas para determinar si ese identificador podría estar registrado en plataformas compatibles.

La herramienta puede devolver resultados con una estructura similar a la siguiente:

```text
[*] Checking username usuario_ejemplo on:
[+] GitHub: https://github.com/usuario_ejemplo
[+] Reddit: https://www.reddit.com/user/usuario_ejemplo
[+] Pinterest: https://www.pinterest.com/usuario_ejemplo

[*] Search completed

```
<img width="1672" height="941" alt="2 Infografía_ Cómo funciona Sherlock OSINT" src="https://github.com/user-attachments/assets/ef8e6c84-917a-4873-a345-a2c6922734da" />

⚠️ **Nota:** Los resultados anteriores son ilustrativos y no representan una búsqueda real.
Sherlock busca coincidencias de **nombres de usuario**, no identifica directamente personas. Que dos perfiles compartan el mismo identificador no significa necesariamente que pertenezcan al mismo propietario.

### 1.2. Importancia de Sherlock en Ethical Hacking

Durante una evaluación de seguridad, el reconocimiento permite identificar información pública que podría ser útil para comprender la exposición digital de una persona u organización.

Por ejemplo, el uso repetido de un mismo nombre de usuario en distintas plataformas podría facilitar la correlación de perfiles públicos.

Esta información permite identificar posibles riesgos relacionados con la privacidad y comprender por qué es importante administrar la información que compartimos en Internet.

Sherlock no es una herramienta de explotación de vulnerabilidades ni permite, por sí misma, acceder a contraseñas o cuentas privadas.

## 2. Objetivos

El objetivo principal de utilizar Sherlock en Kali Linux es recopilar información sobre un objetivo específico a través de la búsqueda de perfiles de usuario en diferentes plataformas en línea.

Esta información puede ser útil para evaluar la postura de seguridad de un individuo o entidad, así como para comprender su superficie de exposición digital.

Al finalizar esta actividad, el participante será capaz de:

1.  Identificar la función de Sherlock dentro de una actividad de reconocimiento pasivo.
2.  Preparar el entorno de Kali Linux necesario para ejecutar la herramienta.
3.  Instalar Sherlock utilizando un procedimiento mediante pipx.
4.  Ejecutar búsquedas de nombres de usuario en diferentes plataformas.
5.  Interpretar los resultados obtenidos e identificar posibles coincidencias.
6.  Guardar evidencias de las búsquedas realizadas.
7.  Reconocer las limitaciones de Sherlock y su utilidad dentro de una evaluación de seguridad.

**Resultado esperado:** El participante ejecutará satisfactoriamente Sherlock en Kali Linux, realizará una búsqueda autorizada e identificará las plataformas en las que el nombre de usuario consultado podría encontrarse registrado.

## 3. Alcance

Sherlock tiene como alcance principal la búsqueda de nombres de usuario en redes sociales y plataformas en línea compatibles.

Durante esta actividad se realizarán las siguientes operaciones:

- Instalación y ejecución de Sherlock en Kali Linux.
- Búsqueda de nombres de usuario propios o expresamente autorizados.
- Identificación de posibles perfiles públicos.
- Revisión e interpretación de los resultados obtenidos.
- Almacenamiento de evidencias de la actividad.

### 3.1. Consideraciones de seguridad y autorización

Esta práctica tiene fines exclusivamente educativos.

Para realizarla, utiliza preferentemente un nombre de usuario propio, una cuenta creada para prácticas o un identificador cuya investigación haya sido autorizada.

La actividad no contempla el acceso a cuentas privadas, la obtención de contraseñas, la modificación de información ni otras acciones fuera del reconocimiento público.

Los resultados deben tratarse como **posibles coincidencias**, no como una confirmación de identidad.

## 4. Herramientas Utilizadas

### 4.1. Sherlock

Sherlock es una herramienta de código abierto que permite buscar nombres de usuario en múltiples plataformas.

**Repositorio oficial:**

<https://github.com/sherlock-project/sherlock>

### 4.2. Kali Linux

Kali Linux es una distribución de Linux orientada a actividades de ciberseguridad, auditoría de sistemas y pruebas de penetración.

En esta actividad se utilizará Kali Linux para instalar Sherlock y ejecutar comandos desde una terminal.

**Sitio oficial:**

<https://www.kali.org/>

### 4.3. Terminal de Linux

La terminal es una interfaz que permite interactuar con el sistema operativo mediante instrucciones escritas denominadas *comandos*.

Durante la actividad se utilizará para instalar Sherlock, ejecutar búsquedas y guardar resultados.

### 4.4. Requisitos previos

Antes de comenzar, verifica que cuentas con:

- Una computadora física o virtual con Kali Linux funcionando.
- Conexión a Internet.
- Una cuenta de usuario en Kali Linux con permisos para instalar paquetes.
- Acceso a una terminal.
- Espacio disponible para instalar las herramientas necesarias.

**Importante:** Si todavía no tienes instalado Kali Linux, deberás preparar el entorno de trabajo antes de comenzar esta actividad.

## 5. Instalación

En esta sección se realizará la instalación de Sherlock en Kali Linux, utilizando la terminal del sistema operativo.

Sherlock está desarrollado en Python y puede instalarse mediante pipx, una herramienta que permite instalar aplicaciones Python en entornos aislados, evitando conflictos con las dependencias del sistema operativo.

Durante el procedimiento se preparará el entorno, se instalará Sherlock y se comprobará su funcionamiento antes de comenzar la actividad práctica.

<img width="1672" height="941" alt="3 Infografía_ Instalación de Sherlock en Kali Linux" src="https://github.com/user-attachments/assets/4da9357e-cd83-4711-ad39-5727b89f6fbd" />


### 5.1. Abrir la terminal de Kali Linux

**Paso 1.** Inicia Kali Linux e ingresa con tu usuario y contraseña.

**Paso 2.** Una vez que se muestre el escritorio, localiza el icono de la terminal en la barra de herramientas.

También puedes acceder mediante el menú de aplicaciones de Kali Linux y seleccionar **Terminal Emulator**.

**Paso 3.** Haz clic para abrir la terminal.

Se mostrará una ventana que permite introducir comandos del sistema operativo.

A partir de este momento, escribe cada comando como aparece en las instrucciones y presiona **Enter** para ejecutarlo.

**Resultado esperado:** La terminal estará abierta y lista para recibir comandos.

### 5.2. Verificar la conexión a Internet

Antes de instalar Sherlock, es necesario verificar que Kali Linux tenga conectividad a Internet.

**Paso 1.** En la terminal, ejecuta:

```bash
ping -c 4 github.com
```

**Explicación del comando:**

- **ping:** verifica la comunicación con otro sistema.

- **-c 4:** indica que se enviarán cuatro solicitudes.

- **github.com**: es el dominio utilizado para realizar la comprobación.

**Paso 2.** Espera a que finalice el comando.

**Resultado esperado:**

Si existe comunicación y el destino responde a las solicitudes ICMP, aparecerán mensajes similares a los siguientes:

```text
┌──(kali㉿kali)-[~]
└─$ ping -c 4 github.com

PING github.com (140.82.114.3) 56(84) bytes of data.
64 bytes from lb-140-82-114-3-iad.github.com (140.82.114.3): icmp_seq=1 ttl=53 time=70.2 ms
64 bytes from lb-140-82-114-3-iad.github.com (140.82.114.3): icmp_seq=2 ttl=53 time=69.8 ms
64 bytes from lb-140-82-114-3-iad.github.com (140.82.114.3): icmp_seq=3 ttl=53 time=69.4 ms
64 bytes from lb-140-82-114-3-iad.github.com (140.82.114.3): icmp_seq=4 ttl=53 time=69.6 ms

--- github.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3009ms
rtt min/avg/max/mdev = 69.427/69.757/70.234/0.299 ms
```

> **Nota:** Los valores pueden variar dependiendo de la red utilizada.

Si no recibes respuestas, verifica la configuración de red de Kali Linux. Ten en cuenta que algunos sistemas bloquean ICMP aunque exista acceso a Internet.

**Validación adicional:** Puedes comprobar el acceso HTTPS mediante:

```bash
curl -I https://github.com
```

Si recibes encabezados HTTP, la conexión HTTPS funciona. Si curl no está instalado, puedes realizar esta comprobación desde el navegador.

### 5.3. Actualizar el índice de paquetes

Para garantizar que Kali Linux consulte la información disponible en sus repositorios, actualizaremos el índice de paquetes.

**Paso 1.** Ejecuta:

```text
┌──(kali㉿kali)-[~]
└─$ sudo apt update
```

**Paso 2.** Si el sistema solicita una contraseña, introduce la contraseña de tu usuario y presiona Enter.

```text
┌──(kali㉿kali)-[~]
└─$ sudo apt update
[sudo] password for kali:
```

> **Nota:** Es normal que los caracteres de la contraseña no aparezcan mientras los escribes.

**Explicación del comando:**

- **sudo:** permite ejecutar el comando con privilegios administrativos.

- **apt:** es el administrador de paquetes de Kali Linux.

- **update:** actualiza la información de los paquetes disponibles en los repositorios configurados.

**Paso 3.** Espera a que finalice el proceso.

**Resultado esperado:** La terminal mostrará la información de los repositorios consultados y finalizará sin errores.

```text
┌──(kali㉿kali)-[~]
└─$ sudo apt update
[sudo] password for kali:
Get:1 http://kali.download/kali kali-rolling InRelease [34.0 kB]
Get:2 http://kali.download/kali kali-rolling/main amd64 Packages [21.6 MB]
Get:3 http://kali.download/kali kali-rolling/main amd64 Contents (deb) [54.0 MB]
Get:4 http://kali.download/kali kali-rolling/contrib amd64 Packages [104 kB]
Get:5 http://kali.download/kali kali-rolling/contrib amd64 Contents (deb) [184 kB]
Get:6 http://kali.download/kali kali-rolling/non-free amd64 Packages [168 kB]
Get:7 http://kali.download/kali kali-rolling/non-free amd64 Contents (deb) [887 kB]
Get:8 http://kali.download/kali kali-rolling/non-free-firmware amd64 Packages [16.3 kB]
Get:9 http://kali.download/kali kali-rolling/non-free-firmware amd64 Contents (deb) [42.5 kB]

Fetched 77.1 MB in 8s (10.2 MB/s)
2254 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

Este procedimiento únicamente actualiza el índice de paquetes; no actualiza todos los programas instalados.

### 5.4. Instalar pipx

Para instalar Sherlock utilizaremos pipx, que permite administrar aplicaciones desarrolladas en Python de manera independiente.

**Paso 1.** Ejecuta:

```bash
sudo apt install pipx -y
```

**Explicación del comando:**

- **sudo:** ejecuta la instalación con permisos administrativos.
- **apt install:** instala un paquete desde los repositorios de Kali Linux.
- **pipx:** es la herramienta que utilizaremos para instalar Sherlock.
- **-y:** acepta automáticamente las confirmaciones solicitadas por el administrador de paquetes.
**Paso 2.** Espera hasta que la instalación finalice.

```text
┌──(kali㉿kali)-[~]
└─$ sudo apt install pipx -y
[sudo] password for kali:

The following packages were automatically installed and are no longer required:
ghp-import mkdocs python3-joblib python3-mergedeep python3-pyyaml-env-tag
libjs-bootstrap5 mkdocs-get-deps python3-livereload python3-nltk
libjs-lunr node-popper2 python3-lunr python3-pathspec
Use 'sudo apt autoremove' to remove them.
Upgrading:
pipx

Summary:
Upgrading: 1, Installing: 0, Removing: 0, Not Upgrading: 2253
Download size: 890 kB
Space needed: 818 kB / 62.7 GB available

Get:1 http://kali.darklab.sh/kali kali-rolling/main amd64 pipx all 1.15.0-1 [890 kB]
Fetched 890 kB in 1s (767 kB/s)
(Reading database ... 422160 files and directories currently installed.)
Preparing to unpack .../archives/pipx_1.15.0-1_all.deb ...
Unpacking pipx (1.15.0-1) over (1.8.0-1) ...
Setting up pipx (1.15.0-1) ...
Processing triggers for kali-menu (2025.4.3) ...
Processing triggers for doc-base (0.11.2) ...
Processing 42 changed doc-base files...
Processing triggers for man-db (2.13.1-1) ...
```

**Paso 3.** Verifica que pipx esté instalado ejecutando:

```text
┌──(kali㉿kali)-[~]
└─$ pipx --version
1.15.0
```

**Resultado esperado:** Se mostrará el número de versión de pipx instalado.

### 5.5. Configurar pipx

Para que los comandos de las aplicaciones instaladas mediante pipx puedan ejecutarse desde la terminal, es necesario comprobar que su directorio de ejecutables esté incluido en la variable de entorno PATH.

**Paso 1.** Ejecuta:

```text
┌──(kali㉿kali)-[~]
└─$ pipx ensurepath
/home/kali/.local/bin is already in PATH.

⚠️ All pipx binary directories have been appended to PATH. If you are sure you want to proceed,

try again with the '--force' flag.
Otherwise pipx is ready to go! ✨ 🌟 ✨
```

Este comando configura la ruta necesaria para localizar los ejecutables instalados mediante pipx.

**Paso 2.** Cierra la terminal y abre una nueva.

Esto permite que los cambios de configuración se apliquen a la nueva sesión.

**Resultado esperado:** pipx habrá configurado la ruta de ejecutables y la terminal estará preparada para ejecutar las aplicaciones instaladas mediante esta herramienta.

### 5.6. Instalar Sherlock

Una vez preparado el entorno, instalaremos Sherlock utilizando el paquete oficial publicado para Python.

**Paso 1.** En la terminal, ejecuta:

```text
┌──(kali㉿kali)-[~]
└─$ pipx install sherlock-project
Installing Sherlock-project
```

**Explicación del comando:**

- **pipx:** ejecuta el administrador de aplicaciones Python.

- **install:** indica que se instalará una aplicación.

- **sherlock-project:** es el nombre del paquete correspondiente a Sherlock.

**Paso 2.** Espera hasta que finalice el proceso de instalación.

Durante esta operación, pipx descargará el paquete y sus dependencias necesarias.

```text
┌──(kali㉿kali)-[~]
└─$ pipx install sherlock-project
installed package sherlock-project 0.16.2, installed using Python 3.13.9
These apps are now available
- sherlock
done! ✨ 🌟 ✨
```

**Paso 3.** Comprueba que Sherlock esté instalado:

```bash
pipx list
```

**Resultado esperado:**

```text
┌──(kali㉿kali)-[~]
└─$ pipx list
venvs are in /home/kali/.local/share/pipx/venvs
apps are exposed on your $PATH at /home/kali/.local/bin
manual pages are exposed at /home/kali/.local/share/man
package sherlock-project 0.16.2, installed using Python 3.13.9
- sherlock

┌──(kali㉿kali)-[~]
└─$
```

La terminal mostrará las aplicaciones administradas mediante pipx. Entre ellas deberá aparecer sherlock-project, junto con su comando ejecutable sherlock.

### 5.7. Validar la instalación de Sherlock

Una vez instalado Sherlock, verificaremos que pueda ejecutarse correctamente.

**Paso 1.** En la terminal, introduce:

```bash
sherlock --help
```

**Paso 2.** Presiona Enter.

**Paso 3.** Observa la información presentada.

```text
┌──(kali㉿kali)-[~]
└─$ sherlock --help
usage: sherlock [-h] [--version] [--verbose] [--folderoutput FOLDEROUTPUT] [--output OUTPUT]
[--csv] [--xlsx] [--site SITE_NAME] [--proxy PROXY_URL] [--dump-response]
[--json JSON_FILE] [--timeout TIMEOUT] [--print-all] [--print-found] [--no-color]
[--browse] [--local] [--nsfw] [--txt] [--ignore-exclusions]
USERNAMES [USERNAMES ...]
Sherlock: Find Usernames Across Social Networks (Version 0.16.2)
positional arguments:
USERNAMES One or more usernames to check with social networks. Check similar
usernames using {?} (replace to '_', '-', '.').
options:
-h, --help show this help message and exit
--version Display version information and dependencies.
--verbose, -v, -d, --debug
Display extra debugging information and metrics.
--folderoutput, -fo FOLDEROUTPUT
If using multiple usernames, the output of the results will be saved to
this folder.
--output, -o OUTPUT If using single username, the output of the result will be saved to this
file.
--csv Create Comma-Separated Values (CSV) File.
--xlsx Create the standard file for the modern Microsoft Excel spreadsheet
(xlsx).
--site SITE_NAME Limit analysis to just the listed sites. Add multiple options to specify
more than one site.
--proxy, -p PROXY_URL
Make requests over a proxy. e.g. socks5://127.0.0.1:1080
--dump-response Dump the HTTP response to stdout for targeted debugging.
--json, -j JSON_FILE Load data from a JSON file or an online, valid, JSON file. Upstream PR
numbers also accepted.
--timeout TIMEOUT Time (in seconds) to wait for response to requests (Default: 60)
--print-all Output sites where the username was not found.
--print-found Output sites where the username was found (also if exported as file).
--no-color Don't color terminal output
--browse, -b Browse to all results on default browser.
--local, -l Force the use of the local data.json file.
--nsfw Include checking of NSFW sites from default list.
--txt Enable creation of a txt file
--ignore-exclusions Ignore upstream exclusions (may return more false positives)

┌──(kali㉿kali)-[~]
```

**Resultado esperado:**

La terminal mostrará el menú de ayuda de Sherlock, incluyendo su sintaxis y las opciones disponibles.

Entre las opciones que pueden encontrarse están:

- **--help:** muestra información de ayuda.
- **--version:** muestra la versión de Sherlock.
- **--output:** permite especificar un archivo donde guardar los resultados.
- **--site:** permite limitar la búsqueda a plataformas específicas.
- **--timeout:** configura el tiempo de espera de las solicitudes.

Las opciones disponibles pueden variar según la versión instalada.

**Paso 4.** Consulta la versión de Sherlock:

```bash
sherlock --version
```

**Resultado esperado:** Se mostrará información de la versión instalada.

```text
┌──(kali㉿kali)-[~]
└─$ sherlock --version
Sherlock v0.16.2
```

Si ambos comandos se ejecutan correctamente, Sherlock estará listo para utilizarse.

### 5.8. Preparar el directorio de trabajo

Para mantener organizados los resultados de la actividad, crearemos una carpeta destinada a guardar las evidencias.

**Paso 1.** Ejecuta:

```bash
mkdir -p ~/CEHPC/Actividad03/evidencias
```

**Explicación del comando:**

- **mkdir:** permite crear directorios.

- **-p:** crea también los directorios intermedios necesarios.

- **~/CEHPC/Actividad03/evidencias:** indica dónde se almacenarán los archivos generados durante la práctica.

**Paso 2.** Comprueba que la carpeta exista:

```bash
ls ~/CEHPC/Actividad03
```

**Resultado esperado:**

> ┌──(kali㉿kali)-\[~\]
> └─\$ mkdir -p ~/CEHPC/Actividad03/evidencias
> ┌──(kali㉿kali)-\[~\]
> └─\$ ls ~/CEHPC/Actividad03
> evidencias

**Paso 3.** Ingresa al directorio:

```bash
cd ~/CEHPC/Actividad03/evidencias
```

**Paso 4.** Comprueba tu ubicación:

```bash
pwd
```

La terminal mostrará una ruta similar a:

**┌──(kali㉿kali)-\[~/CEHPC/Actividad03/evidencias\]**
**└─\$ pwd**
```bash
**/home/kali/CEHPC/Actividad03/evidencias**
```
El nombre del usuario puede variar.

### 5.9. Comprobar el funcionamiento de Sherlock

Antes de comenzar la búsqueda principal de la actividad, ejecutaremos una consulta de prueba para comprobar que Sherlock puede comunicarse con las plataformas compatibles.

**Paso 1.** Ejecuta el siguiente comando utilizando un identificador propio o expresamente autorizado:

```bash
sherlock usuario_ejemplo
```

Sustituye **usuario_ejemplo** por el nombre de usuario seleccionado.

**Paso 2.** Espera a que Sherlock finalice las consultas.

> ️Se paciente, pasaran varios minutos

**Paso 3.** Observa los resultados mostrados en la terminal.

**Resultado esperado:**

> Sherlock mostrará las plataformas en las que haya detectado posibles coincidencias y finalizará la ejecución.
>
> La cantidad de resultados dependerá del nombre de usuario, las plataformas disponibles y la conectividad.
>
> No es necesario encontrar un número determinado de perfiles para verificar que la herramienta funciona correctamente.
>
```text
Instalación completada:** Cuando Sherlock muestre su ayuda, indique su versión y ejecute la consulta de prueba sin errores, podrás continuar con el apartado **6. Ejercicio**.

┌──(kali㉿kali)-[~]
└─$ sherlock ru83n

[*] Checking username ru83n on:
[+] 9GAG: https://www.9gag.com/u/ru83n
[+] Bluesky: https://bsky.app/profile/ru83n.bsky.social
[+] CashApp: https://cash.app/$ru83n
[+] Chess: https://www.chess.com/member/ru83n
[+] Codecademy: https://www.codecademy.com/profiles/ru83n
[+] Discord: https://discord.com
[+] Dribbble: https://dribbble.com/ru83n
[+] Duolingo: https://www.duolingo.com/profile/ru83n
[+] F3.cool: https://f3.cool/ru83n/
[+] Flickr: https://www.flickr.com/people/ru83n
[+] Flipboard: https://flipboard.com/@ru83n
[+] Freelancer: https://www.freelancer.com/u/ru83n
[+] Freesound: https://freesound.org/people/ru83n/
[+] GitHub: https://www.github.com/ru83n
[+] HudsonRock: https://cavalier.hudsonrock.com/api/json/v2/osint-tools/search-by-username?username=ru83n
[+] Hugging Face: https://huggingface.co/ru83n
[+] IFTTT: https://www.ifttt.com/p/ru83n
[+] Imgur: https://imgur.com/user/ru83n
[+] Itch.io: https://ru83n.itch.io/
[+] kaskus: https://www.kaskus.co.id/@ru83n
[+] Kick: https://kick.com/ru83n
[+] Kongregate: https://www.kongregate.com/accounts/ru83n
[+] Memrise: https://www.memrise.com/user/ru83n/
[+] Monkeytype: https://monkeytype.com/profile/ru83n
[+] MyMiniFactory: https://www.myminifactory.com/users/ru83n
[+] NitroType: https://www.nitrotype.com/racer/ru83n
[+] Periscope: https://www.periscope.tv/ru83n/
[+] Pokemon Showdown: https://pokemonshowdown.com/users/ru83n
[+] Redbubble: https://www.redbubble.com/people/ru83n
[+] Replit.com: https://replit.com/@ru83n
[+] RuneScape: https://apps.runescape.com/runemetrics/app/overview/player/ru83n
[+] Scratch: https://scratch.mit.edu/users/ru83n
[+] SoundCloud: https://soundcloud.com/ru83n
[+] Star Citizen: https://robertsspaceindustries.com/citizens/ru83n
[+] Steam Community (User): https://steamcommunity.com/id/ru83n/
[+] TikTok: https://www.tiktok.com/@ru83n
[+] Telegram: https://t.me/ru83n
[+] Tellonym.me: https://tellonym.me/ru83n
[+] TradingView: https://www.tradingview.com/u/ru83n/
[+] Trakt: https://www.trakt.tv/users/ru83n
[+] Venmo: https://account.venmo.com/u/ru83n
[+] Warrior Forum: https://www.warriorforum.com/members/ru83n.html
[+] Wikipedia: https://en.wikipedia.org/wiki/Special:CentralAuth/ru83n?uselang=qqx
[+] Xbox Gamertag: https://xboxgamertag.com/search/ru83n
[+] YouTube: https://www.youtube.com/@ru83n
[+] geocaching: https://www.geocaching.com/p/default.aspx?u=ru83n
[+] osu!: https://osu.ppy.sh/users/ru83n
[+] Pinterest: https://www.pinterest.com/ru83n/
[+] BabyRu: https://www.baby.ru/u/ru83n

[*] Search completed with 49 results

Go deeper than a username. Explore public profiles and export your findings.

Try OSINTSearch: https://osintsearch.org
```

## 6. Ejercicio

### 6.1. Búsqueda de nombres de usuario mediante Sherlock

En esta actividad utilizaremos Sherlock para buscar un nombre de usuario en diferentes redes sociales y plataformas de Internet.

La búsqueda se realizará mediante la terminal de Kali Linux, utilizando un identificador propio o expresamente autorizado.

Para ejecutar Sherlock utilizaremos el siguiente formato:

```bash
sherlock nombre_usuario
```

**Importante:** Sherlock está diseñado para buscar nombres de usuario. Por este motivo, se recomienda emplear un identificador como usuario123, en lugar de un nombre completo que contenga espacios.

**Paso 1. Seleccionar el nombre de usuario**

Para comenzar, selecciona un nombre de usuario propio o expresamente autorizado.

Por ejemplo, si utilizas el identificador usuario_ejemplo en alguna red social, puedes emplearlo durante la práctica.

No es necesario que el identificador exista en todas las plataformas.

**Paso 2. Abrir la terminal**

Si cerraste la terminal después de la instalación, vuelve a abrirla.

Comprueba que Sherlock se encuentra disponible ejecutando:

```bash
sherlock --help
```

Si aparece el menú de ayuda, puedes continuar con el siguiente paso.

**Paso 3. Ejecutar la búsqueda**

Escribe el siguiente comando y reemplaza usuario_ejemplo por el identificador seleccionado:

```bash
sherlock usuario_ejemplo
```

Presiona Enter para iniciar la búsqueda.

**Explicación del comando:**

- **sherlock:** ejecuta la herramienta de búsqueda.

- **usuario_ejemplo:** indica el nombre de usuario que se desea localizar.

Sherlock consultará las plataformas compatibles para identificar posibles coincidencias.

**Paso 4. Esperar a que finalice el proceso**

Durante la ejecución, Sherlock puede mostrar información sobre las plataformas que está consultando.

El tiempo necesario dependerá de la conexión a Internet, del número de plataformas consultadas y de su disponibilidad.

No cierres la terminal mientras se realiza la búsqueda.

Cuando el comando finalice, podrás revisar los resultados obtenidos.

**Paso 5. Identificar los resultados**

En determinadas versiones y configuraciones de Sherlock, los resultados positivos pueden aparecer con una estructura similar a:

```text
[*] Checking username usuario_ejemplo on:
[+] GitHub: https://github.com/usuario_ejemplo
[+] Reddit: https://www.reddit.com/user/usuario_ejemplo
[+] Pinterest: https://www.pinterest.com/usuario_ejemplo
[*] Search completed
```

Los resultados anteriores son ilustrativos.

Observa que cada posible coincidencia contiene información sobre la plataforma consultada y una dirección URL asociada.

<img width="1672" height="941" alt="4 Resultados de Sherlock en Kali Linux" src="https://github.com/user-attachments/assets/5223b1b8-aff7-4e71-afaa-affd4391e9c2" />


**Paso 6. Interpretar los resultados**

Sherlock permite identificar posibles coincidencias de nombres de usuario, pero los resultados requieren interpretación.

| Elemento                | Significado                                                                               |
|-------------------------|-------------------------------------------------------------------------------------------|
| Nombre de la plataforma | Servicio en el que se detectó una posible coincidencia.                                   |
| Dirección URL           | Enlace asociado con el nombre de usuario consultado.                                      |
| Resultado positivo      | Indica que Sherlock detectó una posible existencia del identificador.                     |
| Resultado negativo      | Indica que Sherlock no detectó el identificador mediante el método de consulta utilizado. |
| Error de consulta       | Indica que no fue posible determinar el resultado de una plataforma.                      |

**Consideraciones importantes:**

Una coincidencia positiva no significa necesariamente que el perfil pertenezca a la persona investigada.

Asimismo, un resultado negativo no garantiza que el nombre de usuario no exista en esa plataforma.

Algunos servicios pueden bloquear consultas automatizadas, modificar sus interfaces o presentar errores temporales.

#### Paso 7. Analizar una búsqueda de referencia

Para observar cómo Sherlock presenta los resultados, utilizaremos como referencia el nombre de usuario:

**angelortia**

El comando correspondiente es:

```bash
sherlock angelortia
```

Una búsqueda de este identificador ha mostrado resultados asociados a plataformas como:

- 8tracks
- Academia.edu
- Docker Hub
- Fiverr
- G2G
- Twitter
- Virgool
- WhoNix Forum
- ebio.gg
- Metacritic

Estas coincidencias son referencias de una ejecución previa y pueden variar o dejar de aparecer.

**No es necesario obtener exactamente las mismas coincidencias**, ya que los perfiles disponibles, las plataformas y los mecanismos de búsqueda pueden cambiar con el tiempo.

La finalidad de este ejemplo es permitirte reconocer la estructura de los resultados de Sherlock.

No se debe asumir que los perfiles encontrados pertenecen a una misma persona únicamente porque comparten el nombre de usuario.

#### Paso 8. Guardar los resultados

Para documentar una actividad de reconocimiento, es recomendable guardar la información obtenida.

Sherlock puede generar un archivo de resultados mediante la opción --output.

**Paso 1.** Comprueba que existe el directorio para las evidencias:

```bash
mkdir -p ~/CEHPC/Actividad03/evidencias
```

**Paso 2.** Ejecuta una nueva búsqueda indicando el archivo de salida:

```bash
sherlock usuario_ejemplo --output ~/CEHPC/Actividad03/evidencias/resultados.txt
```

Reemplaza usuario_ejemplo por el identificador autorizado.

**Paso 3.** Espera a que finalice la ejecución.

**Paso 4.** Comprueba que se ha generado el archivo:

```bash
ls -l ~/CEHPC/Actividad03/evidencias/
```

**Paso 5.** Visualiza su contenido:

```bash
cat ~/CEHPC/Actividad03/evidencias/resultados.txt
```

El comando cat permite mostrar el contenido de un archivo de texto en la terminal.

**Resultado esperado:** Se mostrará la información guardada por Sherlock correspondiente a los resultados de la búsqueda. El archivo puede estar vacío si no se encontraron coincidencias, dependiendo del comportamiento de la versión utilizada.

#### Paso 9. Documentar las evidencias

Para considerar finalizada la actividad, conserva las siguientes evidencias:

#### Evidencia 1. Instalación de Sherlock

Una captura de pantalla de la terminal mostrando el resultado de:

```bash
sherlock --help
```

#### Evidencia 2. Ejecución de la búsqueda

Una captura de pantalla en la que se observe el comando utilizado para consultar el identificador.

#### Evidencia 3. Resultados obtenidos

Una captura de pantalla con las coincidencias encontradas, si las hubiera, o con la finalización de la búsqueda cuando no existan resultados.

#### Evidencia 4. Archivo de resultados

El archivo resultados.txt generado durante el procedimiento.

Cuando los resultados contengan información personal, deberán almacenarse de forma privada y compartirse únicamente con las personas autorizadas.

### 6.2. Problemas frecuentes y soluciones

Durante la instalación o ejecución de Sherlock pueden presentarse algunos inconvenientes. Los siguientes procedimientos permiten resolver los problemas más comunes.

#### Problema 1. El comando sherlock no se reconoce

**Mensaje posible:**

sherlock: command not found

**Causa probable:** Sherlock no se instaló correctamente o la carpeta donde se encuentra el ejecutable no está incluida en la variable de entorno PATH.

**Solución:**

Ejecuta:

```bash
pipx list
```

Comprueba que aparezca sherlock-project.

Si no está instalado:

```bash
pipx install sherlock-project
```

Si aparece instalado, ejecuta:

```bash
pipx ensurepath
```

Cierra la terminal, abre una nueva y vuelve a ejecutar:

```bash
sherlock --help
```

#### Problema 2. Error de permisos al instalar paquetes

**Mensaje posible:**

```text
Permission denied
```

**Causa probable:** El usuario no tiene los permisos necesarios para realizar la operación.

**Solución:**

Si el problema ocurre durante una operación con apt, verifica que hayas incluido sudo.

Por ejemplo:

```bash
sudo apt install pipx -y
```

Introduce la contraseña del usuario cuando el sistema la solicite.

Para instalar aplicaciones Python mediante pipx, utiliza el comando como usuario normal, sin sudo, salvo que exista una razón administrativa específica.

#### Problema 3. No se pueden descargar archivos desde Internet

**Mensajes posibles:**

```text
Temporary failure in name resolution

Could not resolve host
```

**Causa probable:** Existe un problema de conectividad o resolución DNS.

**Solución:**

Comprueba la conectividad:

```bash
ping -c 4 github.com
```

Si falla la resolución del nombre, verifica que Kali Linux tenga una conexión de red activa y servidores DNS configurados.

Si trabajas mediante una máquina virtual, revisa también la configuración de su adaptador de red.

En caso de utilizar VMware o VirtualBox, comprueba que la máquina tenga conectividad mediante el modo de red configurado para el entorno de trabajo.

#### Problema 4. Sherlock no encuentra usuarios

**Situación:** La herramienta termina su ejecución, pero no muestra coincidencias.

**Posibles causas:**

- El identificador consultado no se encuentra registrado en las plataformas compatibles.

- El nombre de usuario fue escrito incorrectamente.

- Algunas plataformas no respondieron a las consultas.

- La versión de Sherlock requiere una actualización.

**Solución:**

Comprueba que el nombre de usuario esté correctamente escrito.

Puedes consultar la ayuda:

```bash
sherlock --help
```

Si instalaste Sherlock mediante pipx, actualiza la herramienta con:

```bash
pipx upgrade sherlock-project
```

Después, vuelve a realizar la búsqueda.

**Importante:** La ausencia de resultados no significa necesariamente que Sherlock funcione incorrectamente.

#### Problema 5. Los resultados son diferentes a los del ejemplo

**Situación:** Los resultados de Sherlock no coinciden con las plataformas mencionadas durante el ejercicio.

**Causa probable:** Los datos disponibles en las plataformas cambian constantemente. Además, las versiones de Sherlock pueden utilizar diferentes mecanismos de búsqueda.

**Solución:**

No es necesario obtener exactamente las mismas coincidencias.

Comprueba que Sherlock haya realizado la consulta, terminado su ejecución y mostrado los resultados correspondientes a la versión utilizada.

### 6.3. Finalización de la actividad

La actividad se considera completada satisfactoriamente cuando el participante logra:

1.  Preparar el entorno de Kali Linux.
2.  Instalar Sherlock mediante pipx.
3.  Comprobar el funcionamiento de la herramienta utilizando su ayuda.
4.  Ejecutar una búsqueda de un nombre de usuario autorizado.
5.  Identificar e interpretar los resultados obtenidos.
6.  Guardar los resultados de la ejecución en un archivo.
7.  Conservar las evidencias del procedimiento realizado.

#### Resultado final esperado

Al finalizar, deberás disponer de una carpeta con las evidencias correspondientes a la actividad.

La estructura será similar a:

```text
/home/kali/

└── CEHPC/

└── Actividad03/

└── evidencias/

└── resultados.txt
```

Las capturas de pantalla también podrán almacenarse en la carpeta evidencias.

No es indispensable encontrar un número determinado de perfiles para completar la práctica.

Lo importante es que la herramienta funcione correctamente y que puedas interpretar los resultados que proporciona.

### 6.4. Conclusiones

Sherlock es una herramienta de código abierto que facilita la recopilación de información pública relacionada con nombres de usuario en diversas plataformas de Internet.

Durante esta actividad se realizó su instalación en Kali Linux, se ejecutaron búsquedas de nombres de usuario y se revisó la información obtenida.

La práctica permitió comprender cómo un mismo identificador puede aparecer en diferentes servicios y cómo esta información contribuye al reconocimiento pasivo mediante OSINT.

También se identificaron algunas limitaciones de las herramientas automatizadas de reconocimiento, especialmente la posibilidad de obtener falsos positivos, resultados incompletos o información desactualizada.

En un proceso profesional de Ethical Hacking, los resultados de Sherlock pueden formar parte de una investigación más amplia, siempre dentro de un alcance autorizado.

**La información obtenida durante el reconocimiento debe utilizarse de manera responsable, documentarse adecuadamente y analizarse antes de establecer cualquier conclusión sobre un individuo o una organización.**

## Referencias técnicas

**Sherlock Project — Repositorio oficial**  
<https://github.com/sherlock-project/sherlock>

**Kali Linux — Documentación oficial**  
<https://www.kali.org/docs/>

**Python pipx — Documentación**  
<https://pipx.pypa.io/>
