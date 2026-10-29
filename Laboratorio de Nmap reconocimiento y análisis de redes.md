# Laboratorio de Nmap: reconocimiento y análisis de redes

> **Ethical Hacking Professional Certification (CEHPC)**  
> **Módulo 4:** Escaneo y Análisis de Red  
> **Temas:** 4.3 Introducción a Nmap y 4.4 Categorías de Nmap

| Característica | Descripción |
|---|---|
| Duración estimada | 150–180 minutos |
| Nivel | Básico–intermedio |
| Modalidad | Práctica guiada |
| Sistema operativo | Kali Linux |
| Herramienta | Nmap 7.98 |
| IP de Kali Linux | `192.168.56.103` |
| Segmento de laboratorio | `192.168.56.0/24` |
| Entorno | Red virtual de VirtualBox |


---

## 1. Introducción

**Nmap (Network Mapper)** es una herramienta de código abierto para descubrir dispositivos conectados a una red, identificar puertos abiertos, reconocer servicios y versiones de software e inferir sistemas operativos. En Ethical Hacking se utiliza principalmente en el reconocimiento activo y la enumeración de servicios.

Durante esta práctica se ejecutan técnicas de escaneo sobre una **red virtual controlada**, prestando atención a los protocolos, parámetros, estados de puertos y respuestas observadas.

> [!IMPORTANT]
> Los escaneos deben ejecutarse **únicamente sobre dispositivos y redes autorizados**. Las direcciones de este laboratorio son privadas y de ejemplo. Los resultados de los ejercicios posteriores al primero son ilustrativos, no mediciones realizadas sobre `192.168.56.101`.

## 2. Objetivos

**Objetivo general:** aplicar técnicas de reconocimiento activo mediante Nmap para descubrir hosts, identificar puertos y servicios, analizar características del sistema operativo e interpretar los resultados.

**Objetivos específicos:**

- Identificar dispositivos activos de un segmento IPv4.
- Diferenciar descubrimiento mediante ARP, ICMP, TCP y UDP.
- Ejecutar distintos métodos de escaneo TCP.
- Identificar servicios TCP y UDP.
- Reconocer versiones y características de sistemas operativos.
- Interpretar filtrado y respuestas ambiguas.
- Aplicar parámetros de temporización.
- Guardar evidencias para documentación técnica.

## 3. Entorno de laboratorio

| Elemento | Valor |
|---|---|
| Kali Linux | `192.168.56.103/24` |
| Segmento | `192.168.56.0/24` |
| Objetivo de ejemplo | `192.168.56.101` |
| Direcciones detectadas inicialmente | `.1`, `.100`, `.101`, `.102`, `.103` |

**La IP del host de prueba puede cambiar porque puede ser asignada por DHCP.** En adelante `192.168.56.X` representa la dirección real del dispositivo autorizado. Se utiliza `192.168.56.101` solo como ejemplo; sustitúyela si cambia. El sufijo `/24` se aplica al **segmento** en los barridos y no es necesario al escanear una única IP.

<img width="1672" height="941" alt="Entorno de laboratorio" src="https://github.com/user-attachments/assets/0b383869-5832-49a4-868e-5dd534b493cc" />



### 3.1 Verificar la interfaz de Kali

```bash
ip -br addr
```

Localiza la interfaz con dirección `192.168.56.103/24`. El campo `UP` indica que la interfaz está habilitada; `lo` es la interfaz de loopback.

### 3.2 Verificar la instalación de Nmap

```bash
nmap --version
nmap -h
man nmap
```

`--version` muestra la versión instalada; `-h` presenta las opciones resumidas; `man nmap` abre el manual. Presiona `q` para cerrarlo.

### 3.3 Preparar el directorio de evidencias

```bash
mkdir -p ~/CEHPC/Nmap/Evidencias
cd ~/CEHPC/Nmap/Evidencias
pwd
```

`mkdir -p` crea la carpeta si no existe, `cd` accede a ella y `pwd` muestra la ruta actual.

---

## 4. Ejercicio 1 — Descubrimiento básico de hosts

**Categoría:** Host Discovery.  
**Objetivo:** identificar dispositivos activos dentro del segmento `192.168.56.0/24`.

### 4.1 Ejecutar el comando

```bash
sudo nmap -sn 192.168.56.0/24
```

| Elemento | Función |
|---|---|
| `sudo` | Ejecuta Nmap con privilegios administrativos. |
| `nmap` | Inicia la herramienta. |
| `-sn` | Descubre hosts sin escanear sus puertos. |
| `192.168.56.0/24` | Comprende 256 direcciones IPv4 del segmento. |

En una LAN Ethernet, Nmap con privilegios suele utilizar **ARP** para el descubrimiento IPv4.

### 4.2 Salida real proporcionada del laboratorio

```text
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sn 192.168.56.0/24
[sudo] password for kali:
Starting Nmap 7.98 ( https://nmap.org ) at 2026-10-28 03:11 -0400
Nmap scan report for 192.168.56.1
Host is up (0.00035s latency).
MAC Address: 0A:00:27:00:00:0C (Unknown)
Nmap scan report for 192.168.56.100
Host is up.
MAC Address: 08:00:27:AC:88:30 (Oracle VirtualBox virtual NIC)
Nmap scan report for 192.168.56.101
Host is up (0.00051s latency).
MAC Address: 08:00:27:6F:B4:FF (Oracle VirtualBox virtual NIC)
Nmap scan report for 192.168.56.102
Host is up (0.00047s latency).
MAC Address: 08:00:27:38:9D:E6 (Oracle VirtualBox virtual NIC)
Nmap scan report for 192.168.56.103
Host is up.
Nmap done: 256 IP addresses (5 hosts up) scanned in 6.43 seconds
```

### 4.3 Interpretación de la salida

- **`Starting Nmap 7.98 ... -0400`**: versión de Nmap, fecha, hora y desplazamiento horario que reportó el equipo.
- **`Nmap scan report for 192.168.56.101`**: comienza el reporte de esa IP.
- **`Host is up (0.00051s latency)`**: Nmap encontró evidencia de actividad; el valor equivale aproximadamente a **0.51 ms** de latencia observada.
- **`Host is up.`** sin latencia: se detectó el host pero no se mostró estimación temporal; **no** significa latencia cero.
- **`MAC Address: 08:00:27:6F:B4:FF (...)`**: dirección MAC detectada y fabricante inferido por su prefijo. No identifica por sí sola el sistema operativo.
- **`256 IP addresses (5 hosts up) scanned in 6.43 seconds`**: se consideraron 256 direcciones, se detectaron cinco hosts y el proceso tardó 6.43 segundos.

| IP | MAC detectada | Fabricante indicado | Latencia |
|---|---|---|---|
| `192.168.56.1` | `0A:00:27:00:00:0C` | Unknown | 0.35 ms |
| `192.168.56.100` | `08:00:27:AC:88:30` | Oracle VirtualBox | No reportada |
| `192.168.56.101` | `08:00:27:6F:B4:FF` | Oracle VirtualBox | 0.51 ms |
| `192.168.56.102` | `08:00:27:38:9D:E6` | Oracle VirtualBox | 0.47 ms |
| `192.168.56.103` | No reportada | Kali Linux | No reportada |

**Conclusión:** se identificaron cinco hosts. `192.168.56.103` corresponde a Kali. Los dispositivos `.100`, `.101` y `.102` presentan interfaces reconocidas como virtuales, pero este resultado **no demuestra** cuáles son sus servicios ni sus sistemas operativos.

Para los siguientes ejercicios se usará **`192.168.56.101` como ejemplo**, siempre que corresponda a un objetivo autorizado y siga teniendo esa IP.

---

## 5. Ejercicio 2 — Descubrimiento mediante ARP

**Objetivo:** comprobar la presencia de un host IPv4 de la red local mediante ARP.

### 5.1 Fundamento

ARP (*Address Resolution Protocol*) permite resolver una IPv4 local a una MAC. Un dispositivo puede responder a una solicitud ARP identificándose como el propietario de la IP; también existen situaciones especiales, como Proxy ARP.

### 5.2 Comando

```bash
sudo nmap -sn -PR 192.168.56.101
```

- `-sn`: no escanea puertos.
- `-PR`: solicita descubrimiento ARP en la red local.
- `192.168.56.101`: equipo autorizado de ejemplo.

### 5.3 Salida ilustrativa

```text
Nmap scan report for 192.168.56.101
Host is up (0.00051s latency).
MAC Address: 08:00:27:6F:B4:FF (Oracle VirtualBox virtual NIC)
Nmap done: 1 IP address (1 host up)
```

**Interpretación:** se encontró evidencia de un host que responde por esa IP. La MAC corresponde a la interfaz anunciada en la respuesta. ARP funciona en el segmento local IPv4, no como técnica de descubrimiento directo de hosts remotos a través de routers.

---

## 6. Ejercicio 3 — Descubrimiento mediante ICMP Echo

**Objetivo:** observar mensajes ICMP Echo Request y Echo Reply.

<img width="1774" height="887" alt="6 ICM ECO" src="https://github.com/user-attachments/assets/9b028a16-606c-451b-a6f5-3b6a7dcce8fc" />


### 6.1 Comando

```bash
sudo nmap -sn -PE --disable-arp-ping 192.168.56.101
```

- `-PE`: emplea ICMP Echo Request (tipo 8).
- `--disable-arp-ping`: evita que Nmap dé preferencia a ARP Ping en este ejercicio local.
- `-sn`: omite el escaneo de puertos.

**Secuencia esperada:** `Kali → ICMP Echo Request (tipo 8) → Objetivo → ICMP Echo Reply (tipo 0) → Kali`.

### 6.2 Posible salida con respuesta

```text
Nmap scan report for 192.168.56.101
Host is up (0.0012s latency).
Nmap done: 1 IP address (1 host up)
```

Si no existe respuesta concluyente, puede mostrarse:

```text
Note: Host seems down. If it is really up, but blocking
our ping probes, try -Pn
Nmap done: 1 IP address (0 hosts up)
```

**Interpretación:** una respuesta Echo permite inferir conectividad y actividad; la falta de respuesta **no demuestra** que el equipo esté apagado, pues ICMP puede estar filtrado o perdido.

---

## 7. Ejercicio 4 — Descubrimiento con TCP y UDP

**Objetivo:** comparar alternativas a ICMP.

### 7.1 TCP SYN Ping

```bash
sudo nmap -sn -PS22,80,443 --disable-arp-ping 192.168.56.101
```

`-PS` envía SYN a los puertos indicados. Una respuesta **SYN/ACK o RST** permite considerar activo al host.

### 7.2 TCP ACK Ping

```bash
sudo nmap -sn -PA80,443 --disable-arp-ping 192.168.56.101
```

`-PA` envía ACK; una respuesta **RST** puede confirmar actividad del host.

### 7.3 UDP Ping

```bash
sudo nmap -sn -PU40125 --disable-arp-ping 192.168.56.101
```

`-PU40125` envía una sonda UDP al puerto 40125.

| Respuesta | Interpretación |
|---|---|
| TCP SYN/ACK o RST ante SYN | Host activo. |
| TCP RST ante ACK | Host activo. |
| Respuesta UDP | Host activo. |
| ICMP Port Unreachable ante UDP | Host activo; el puerto UDP no acepta el datagrama. |
| Sin respuesta | Resultado no concluyente; posible filtrado, pérdida o inactividad. |

### 7.4 Salida posible

```text
Nmap scan report for 192.168.56.101
Host is up (0.0015s latency).
Nmap done: 1 IP address (1 host up)
```

**Interpretación:** la apariencia final puede ser similar para los tres comandos aunque los paquetes enviados sean distintos. Es normal que un equipo responda a una técnica y no a otra, según sus controles de red.

---

## 8. Ejercicio 5 — Escaneo básico de puertos TCP

**Objetivo:** identificar estados de puertos TCP en el objetivo.

### 8.1 Comando

```bash
nmap 192.168.56.101
```

Nmap normalmente selecciona los **1000 puertos TCP más frecuentes**, no necesariamente los primeros 1000 numéricamente. El tipo de escaneo predeterminado depende de los privilegios y del entorno.

### 8.2 Salida ilustrativa (no verificada en el objetivo)

```text
Nmap scan report for 192.168.56.101
Host is up (0.0011s latency).
Not shown: 997 closed tcp ports
PORT    STATE SERVICE
21/tcp  open  ftp
22/tcp  open  ssh
80/tcp  open  http
Nmap done: 1 IP address (1 host up)
```

### 8.3 Interpretación

- **`Not shown: 997 closed tcp ports`**: 997 puertos cerrados se omiten de la tabla.
- **`21/tcp`**: puerto 21 del protocolo TCP.
- **`open`**: Nmap encontró evidencia de un servicio que acepta conexiones.
- **`ftp`**: nombre asociado al puerto; sin `-sV`, esto **no confirma** el software real.

| Estado | Significado |
|---|---|
| `open` | Hay un servicio que acepta conexiones o datagramas. |
| `closed` | Puerto accesible, pero sin servicio escuchando. |
| `filtered` | El filtrado impide determinar si está abierto o cerrado. |
| `unfiltered` | Alcanzable, aunque la técnica no distingue abierto/cerrado. |
| `open\|filtered` | Abierto o filtrado; resultado ambiguo. |
| `closed\|filtered` | Cerrado o filtrado; resultado ambiguo. |

---

## 9. Ejercicio 6 — TCP SYN, Connect y ACK

**Objetivo:** comparar mecanismos TCP y comprender sus diferentes resultados.

### 9.1 TCP SYN Scan

```bash
sudo nmap -sS -p 21,22,80,443 192.168.56.101
```

<img width="1774" height="887" alt="9 ICMP Scan a" src="https://github.com/user-attachments/assets/7fb0bbd2-b063-4336-acef-72ff0131562b" />



`-sS` envía SYN: un **SYN/ACK** permite inferir `open`, un **RST** normalmente indica `closed`; normalmente no se completa el *three-way handshake*.

**Ejemplo ilustrativo:**

```text
PORT    STATE  SERVICE
21/tcp  open   ftp
22/tcp  open   ssh
80/tcp  open   http
443/tcp closed https
```

### 9.2 TCP Connect Scan

```bash
nmap -sT -p 21,22,80,443 192.168.56.101
```

`-sT` utiliza funciones de conexión del sistema operativo y puede completar el establecimiento TCP (`SYN → SYN/ACK → ACK`). Puede producir estados similares a `-sS`.

### 9.3 TCP ACK Scan

```bash
sudo nmap -sA -p 21,22,80,443 192.168.56.101
```

**Ejemplo ilustrativo:**

```text
PORT    STATE      SERVICE
21/tcp  unfiltered ftp
22/tcp  unfiltered ssh
80/tcp  unfiltered http
443/tcp unfiltered https
```

**Importante:** `unfiltered` **no significa abierto**: ACK Scan permite analizar principalmente si el tráfico parece filtrado.

| Característica | `-sS` | `-sT` | `-sA` |
|---|---|---|---|
| Técnica | SYN | TCP Connect | ACK |
| Completa normalmente el handshake | No | Sí, si se acepta conexión | No |
| Distingue puertos abiertos | Sí | Sí | No |
| Analiza filtrado | Sí | Sí | Principal finalidad |

---

## 10. Ejercicio 7 — TCP NULL, FIN y Xmas

**Objetivo:** analizar resultados al cambiar las banderas TCP de las sondas.

### 10.1 NULL Scan

```bash
sudo nmap -sN -p 21,22,80,443 192.168.56.101
```

`-sN`: paquetes sin banderas TCP activadas.

### 10.2 FIN Scan

```bash
sudo nmap -sF -p 21,22,80,443 192.168.56.101
```

`-sF`: paquete con bandera FIN.

### 10.3 Xmas Scan

```bash
sudo nmap -sX -p 21,22,80,443 192.168.56.101
```

`-sX`: banderas FIN, PSH y URG.

### 10.4 Salida ilustrativa

```text
PORT    STATE         SERVICE
21/tcp  open|filtered ftp
22/tcp  open|filtered ssh
80/tcp  open|filtered http
443/tcp closed        https
```

| Respuesta observada | Interpretación habitual en estas técnicas |
|---|---|
| RST | `closed` |
| Sin respuesta concluyente | `open\|filtered` |
| Determinados mensajes ICMP de error | `filtered` |

El estado `open|filtered` **no confirma** un puerto abierto. Estas técnicas también presentan limitaciones según el sistema operativo y su implementación TCP.

---

## 11. Ejercicio 8 — Escaneo UDP

**Objetivo:** identificar posibles servicios UDP y sus estados.

### 11.1 Comando

```bash
sudo nmap -sU -p 53,69,111,137,161 192.168.56.101
```

- `-sU`: escaneo UDP.
- `-p`: limita los puertos a DNS (53), TFTP (69), RPC (111), NetBIOS-NS (137) y SNMP (161), según sus asociaciones habituales.

### 11.2 Salida ilustrativa

```text
PORT    STATE         SERVICE
53/udp  open          domain
69/udp  open|filtered tftp
111/udp open          rpcbind
137/udp closed        netbios-ns
161/udp open|filtered snmp
```

- **`open`**: hubo respuesta compatible con un servicio UDP.
- **`closed`**: normalmente se obtuvo ICMP Port Unreachable.
- **`open|filtered`**: no es posible distinguir si el servicio está abierto o filtrado.

### 11.3 Ampliar la identificación

```bash
sudo nmap -sU -sV -p 53,69,111,137,161 192.168.56.101
```

`-sV` envía sondas de detección de versiones que pueden ayudar a identificar el producto y aclarar algunos resultados ambiguos.

---

## 12. Ejercicio 9 — Especificación de puertos

**Objetivo:** controlar la amplitud del escaneo TCP.

**Puerto individual:**

```bash
nmap -p 22 192.168.56.101
```

**Lista de puertos:**

```bash
nmap -p 21,22,23,80,443 192.168.56.101
```

**Rango de puertos:**

```bash
nmap -p 1-1024 192.168.56.101
```

**Todos los puertos TCP (1–65535):**

```bash
sudo nmap -sS -p- 192.168.56.101
```

### Interpretación

`-p` selecciona explícitamente puertos, mientras que `-p-` recorre todos los números de puerto TCP válidos para escaneo. Un escaneo completo puede descubrir servicios fuera del conjunto predeterminado.

Si todos los puertos elegidos están cerrados, puede aparecer:

```text
All 5 scanned ports on 192.168.56.101 are in ignored states.
Not shown: 5 closed tcp ports (reset)
```

Esto significa que los cinco puertos se clasificaron como cerrados y se omitieron de la tabla.

---

## 13. Ejercicio 10 — Servicios y versiones

**Objetivo:** identificar productos y versiones asociados a puertos accesibles.

### 13.1 Comando

```bash
sudo nmap -sV -p 21,22,80,3306 192.168.56.101
```

`-sV` activa sondas de detección de servicios y versiones.

### 13.2 Salida ilustrativa de un entorno vulnerable de entrenamiento

```text
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 2.3.4
22/tcp   open  ssh     OpenSSH 4.7p1 Debian
80/tcp   open  http    Apache httpd 2.2.8
3306/tcp open  mysql   MySQL 5.0.51a
```

**Interpretación:** en `80/tcp open http Apache httpd 2.2.8`, Nmap identificó respuestas compatibles con Apache HTTP Server 2.2.8 en TCP 80.

> [!NOTE]
> Una versión detectada no demuestra por sí sola que exista una vulnerabilidad explotable. La correlación requiere considerar parches, configuración y contexto.

---

## 14. Ejercicio 11 — Sistema operativo

**Objetivo:** inferir características del sistema operativo mediante *fingerprinting* TCP/IP.

### 14.1 Comando

```bash
sudo nmap -O 192.168.56.101
```

### 14.2 Salida ilustrativa

```text
Device type: general purpose
Running: Linux 2.6.X
OS details: Linux 2.6.9 - 2.6.33
Network Distance: 1 hop
```

| Campo | Interpretación |
|---|---|
| `Device type` | Categoría de dispositivo inferida. |
| `Running` | Familia de sistema operativo probable. |
| `OS details` | Versiones candidatas de la huella. |
| `Network Distance` | Saltos de red estimados hasta el host. |

Si las condiciones no son adecuadas, Nmap puede advertir:

```text
OSScan results may be unreliable because we could not
find at least 1 open and 1 closed port
```

**Interpretación:** la inferencia de sistema operativo es probabilística y puede ser menos confiable sin suficientes respuestas distintivas.

**Escaneo combinado:**

```bash
sudo nmap -sV -O 192.168.56.101
```

---

## 15. Ejercicio 12 — Temporización y rendimiento

**Objetivo:** comparar plantillas de velocidad y reintentos.

**Temporización conservadora:**

```bash
sudo nmap -sS -T2 -p 1-100 192.168.56.101
```

**Temporización agresiva para redes confiables:**

```bash
sudo nmap -sS -T4 -p 1-100 192.168.56.101
```

**Limitar retransmisiones adicionales:**

```bash
sudo nmap -sS -T3 --max-retries 2 -p 1-100 192.168.56.101
```

### Salida final ilustrativa

```text
Nmap done: 1 IP address (1 host up) scanned in 3.42 seconds
```

`scanned in 3.42 seconds` indica la duración total del comando. La duración real depende de pérdidas, latencia, filtros y cantidad de puertos. Una configuración demasiado rápida puede reducir la fiabilidad de ciertos resultados.

---

## 16. Ejercicio 13 — Filtrado y motivos de respuesta

**Objetivo:** relacionar los estados de los puertos con las respuestas de red.

### 16.1 Escaneo SYN con motivos

```bash
sudo nmap -sS --reason -p 22,80,443 192.168.56.101
```

**Salida ilustrativa:**

```text
PORT    STATE    SERVICE REASON
22/tcp  open     ssh     syn-ack
80/tcp  open     http    syn-ack
443/tcp filtered https   no-response
```

`--reason` explica por qué se asignó un estado.

| Motivo | Significado |
|---|---|
| `syn-ack` | Se recibió TCP SYN/ACK. |
| `reset` | Se recibió TCP RST. |
| `no-response` | No hubo respuesta concluyente. |
| `admin-prohibited` | Un mensaje ICMP indica prohibición administrativa. |

### 16.2 Comparación con ACK Scan

```bash
sudo nmap -sA --reason -p 22,80,443 192.168.56.101
```

**Salida ilustrativa:**

```text
PORT    STATE      SERVICE REASON
22/tcp  unfiltered ssh     reset
80/tcp  unfiltered http    reset
443/tcp filtered   https   no-response
```

`filtered` sugiere filtrado en la trayectoria, pero no demuestra por sí solo qué equipo o regla de seguridad intervino.

---

## 17. Ejercicio 14 — Almacenamiento de resultados

**Objetivo:** generar archivos reproducibles de evidencia.

### 17.1 Acceder a la carpeta

```bash
cd ~/CEHPC/Nmap/Evidencias
```

### 17.2 Ejecutar y guardar resultados

```bash
sudo nmap -sV -O -p 21,22,80,3306 -oA escaneo_final 192.168.56.101
```

| Opción | Función |
|---|---|
| `-sV` | Detecta servicios y versiones. |
| `-O` | Intenta identificar el sistema operativo. |
| `-p` | Selecciona puertos. |
| `-oA escaneo_final` | Guarda tres formatos de salida con ese nombre base. |

**Archivos generados:**

- `escaneo_final.nmap`: salida normal para lectura humana.
- `escaneo_final.xml`: salida estructurada para integración con herramientas.
- `escaneo_final.gnmap`: formato grepable heredado.

### 17.3 Consultar e identificar evidencias

```bash
ls -lh escaneo_final.*
cat escaneo_final.nmap
head -n 20 escaneo_final.xml
sha256sum escaneo_final.*
```

`ls -lh` muestra tamaños y permisos; `cat` presenta el archivo normal; `head` revisa el comienzo del XML; `sha256sum` genera huellas para comprobar integridad posteriormente.

---

## 18. Ejercicio integrador

**Objetivo:** ejecutar un proceso completo de descubrimiento, enumeración y documentación sobre **un dispositivo autorizado** del laboratorio.

### 18.1 Actualizar la lista de hosts

```bash
sudo nmap -sn 192.168.56.0/24
```

Confirma la IP actual: **DHCP puede haber cambiado el último octeto `X`**.

### 18.2 Definir una variable para el objetivo

```bash
TARGET=192.168.56.101
echo "$TARGET"
```

El resultado del segundo comando será `192.168.56.101` si mantuviste el ejemplo. **Reemplaza** el valor si tu equipo autorizado tiene otra IP.

### 18.3 Reconocimiento general TCP

```bash
sudo nmap -sS -sV -O "$TARGET"
```

Realiza SYN Scan de los puertos predeterminados, intenta identificar servicios/versiones e inferir el sistema operativo.

### 18.4 Reconocimiento UDP dirigido

```bash
sudo nmap -sU -sV -p 53,69,111,137,161 "$TARGET"
```

Analiza cinco puertos UDP y trata de identificar servicios.

### 18.5 Análisis de filtrado

```bash
sudo nmap -sA --reason -p 21,22,80,443 "$TARGET"
```

Muestra estados de ACK Scan y motivos que los sustentan; **no** confirma puertos abiertos.

### 18.6 Guardar evidencia final

```bash
cd ~/CEHPC/Nmap/Evidencias
sudo nmap -sS -sV -O -oA reconocimiento_completo "$TARGET"
ls -lh reconocimiento_completo.*
```

### 18.7 Documentación de resultados

Registra **únicamente** valores observados en tus propias salidas:

| IP objetivo | Puerto | Protocolo | Estado | Servicio | Versión |
|---|---|---|---|---|---|
| `192.168.56.X` | Por registrar | TCP/UDP | Por registrar | Por registrar | Por registrar |

Incluye en tu informe una explicación de los estados observados, las limitaciones de las técnicas y las recomendaciones para revisar servicios innecesarios o desactualizados.

---

## 19. Conclusiones

El reconocimiento activo permite observar de forma estructurada los sistemas y servicios accesibles en una red. **Nmap no convierte automáticamente un puerto abierto en una vulnerabilidad confirmada**: las evidencias deben interpretarse en función de las técnicas utilizadas, el comportamiento de los protocolos, los controles de filtrado y el contexto del sistema.

La competencia central de esta práctica es transformar las respuestas técnicas de Nmap en información útil para analizar y mejorar la postura de seguridad, con autorización y trazabilidad de los resultados.

## 20. Referencias

- [Nmap — Sitio oficial](https://nmap.org/)
- [Nmap Reference Guide](https://nmap.org/book/man.html)
- [Nmap — Host Discovery](https://nmap.org/book/man-host-discovery.html)
- [Nmap — Port Scanning Techniques](https://nmap.org/book/man-port-scanning-techniques.html)
- [Nmap — Service and Version Detection](https://nmap.org/book/man-version-detection.html)
- [Nmap — Output Formats](https://nmap.org/book/man-output.html)
- [NIST SP 800-115 — Technical Guide to Information Security Testing and Assessment](https://csrc.nist.gov/pubs/sp/800/115/final)

---

> **Nota sobre las salidas:** solo la salida del **Ejercicio 1** proviene de la ejecución real compartida. Todas las demás son ejemplos explicativos; los resultados efectivos dependerán del equipo autorizado seleccionado, sus servicios, firewall y configuración de red.
