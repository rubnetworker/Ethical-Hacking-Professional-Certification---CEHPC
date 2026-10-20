# Actividad 02. Shodan

**Ethical Hacking Professional Certification (CEHPC)**

| Información | Detalle |
|---|---|
| **Duración estimada** | 50–60 minutos |
| **Nivel** | Básico |
| **Herramienta** | Shodan |
| **Modalidad** | Práctica individual, presencial o autodirigida |

---

## 1. Introducción

Shodan es un motor de búsqueda especializado en identificar dispositivos y servicios conectados a Internet. A diferencia de los motores de búsqueda convencionales, como Google, que se enfocan principalmente en páginas web y documentos, Shodan recopila e indexa información técnica de sistemas accesibles desde Internet.

Entre los dispositivos que pueden encontrarse mediante Shodan destacan:

- Servidores y equipos de cómputo.
- Routers y dispositivos de infraestructura de red.
- Cámaras IP y sistemas de videovigilancia.
- Dispositivos IoT (*Internet of Things*).
- Servidores web, bases de datos y servicios de acceso remoto.

Shodan fue creado por John Matherly en 2009 y se ha convertido en una herramienta utilizada por investigadores de seguridad, profesionales de TI y especialistas en ciberseguridad.

### 1.1. ¿Cómo funciona Shodan?

Shodan recopila información mediante procesos automatizados de exploración de servicios disponibles en Internet. Durante este proceso obtiene datos como puertos, protocolos y respuestas enviadas por los sistemas.

Estas respuestas, conocidas como *banners*, pueden contener información sobre el software, su versión y determinadas características del servicio.

Posteriormente, Shodan almacena e indexa los datos recopilados para que los usuarios puedan consultarlos mediante filtros de búsqueda.

Por ejemplo, un administrador de seguridad puede utilizar Shodan para investigar si su organización tiene servicios de administración remota expuestos públicamente.

### 1.2. Conceptos técnicos fundamentales

| Concepto | Descripción |
|---|---|
| Dirección IP | Identificador lógico que permite localizar un dispositivo en una red. |
| Puerto | Identificador numérico utilizado para distinguir servicios de comunicación. |
| Protocolo | Conjunto de reglas que permiten la comunicación entre dispositivos. |
| Banner | Información que un servicio puede proporcionar cuando recibe una conexión. |
| RDP | Protocolo utilizado para acceder remotamente al escritorio de un equipo. |
| IoT | Dispositivos físicos conectados a redes que pueden recopilar o intercambiar información. |
| Reconocimiento pasivo | Recopilación de información sin interactuar directamente con los sistemas investigados. |
| Superficie de ataque | Conjunto de puntos potenciales mediante los cuales un sistema podría recibir ataques. |

> [!IMPORTANT]
> Identificar un dispositivo mediante Shodan no significa que sea vulnerable. Una exposición representa información disponible desde Internet, mientras que una vulnerabilidad requiere un análisis adicional para confirmarse.

---

## 2. Objetivos

El objetivo principal de esta actividad es utilizar Shodan como herramienta de reconocimiento pasivo para identificar servicios y dispositivos expuestos a Internet, interpretar la información disponible y comprender sus implicaciones de seguridad.

Al finalizar la actividad, serás capaz de:

1. Comprender el funcionamiento básico de Shodan.
2. Acceder a la plataforma y realizar consultas mediante su buscador.
3. Utilizar filtros para localizar determinados servicios y dispositivos.
4. Identificar registros asociados con el protocolo Remote Desktop Protocol (RDP).
5. Interpretar información técnica como direcciones IP, puertos, protocolos y sistemas operativos.
6. Realizar búsquedas relacionadas con cámaras web y dispositivos IoT.
7. Reconocer posibles riesgos de seguridad asociados con la exposición de servicios.
8. Documentar los resultados de una actividad de reconocimiento pasivo.

---

## 3. Alcance

Shodan permite realizar diferentes actividades relacionadas con la evaluación de seguridad de sistemas y dispositivos conectados a Internet.

### 3.1. Identificación de dispositivos potencialmente vulnerables

Permite localizar información de dispositivos que podrían presentar configuraciones inseguras, software desactualizado o servicios expuestos innecesariamente.

### 3.2. Análisis de seguridad de infraestructura

Facilita la identificación de activos expuestos a Internet que pueden formar parte de la superficie de ataque de una organización.

### 3.3. Investigación de dispositivos IoT

Permite consultar información relacionada con dispositivos como cámaras IP, sensores, sistemas de automatización y otros equipos conectados a Internet.

### 3.4. Monitoreo de redes

Ayuda a identificar cambios en la exposición de dispositivos y servicios a partir de la información recopilada en distintos momentos.

### 3.5. Consideraciones éticas y de seguridad

Durante esta actividad realizarás consultas sobre información previamente indexada por Shodan.

Debes considerar las siguientes reglas:

- Realiza únicamente las consultas indicadas.
- No intentes autenticarte en sistemas o servicios de terceros.
- No ejecutes herramientas de explotación contra los dispositivos identificados.
- No intentes obtener contraseñas ni acceder a información privada.
- No accedas a transmisiones de videovigilancia de terceros.
- No compartas públicamente direcciones IP ni información sensible localizada durante el ejercicio.
- Toda prueba activa debe realizarse únicamente sobre sistemas propios o expresamente autorizados.

El propósito de esta actividad es aprender a identificar e interpretar información relacionada con la exposición de servicios, no intentar obtener acceso a dispositivos.

---

## 4. Herramientas utilizadas

### 4.1. Shodan

Shodan es una plataforma de búsqueda de dispositivos y servicios conectados a Internet que permite consultar la información que ha recopilado e indexado.

**Sitio web:** [https://www.shodan.io](https://www.shodan.io)

#### Requisitos para realizar la actividad

Necesitarás:

- Una computadora con acceso a Internet.
- Un navegador web actualizado, como Chrome, Firefox o Edge.
- Acceso al sitio web de Shodan.
- Una cuenta personal en Shodan, si alguna función utilizada requiere autenticación.
- Un medio para registrar observaciones y guardar capturas de pantalla.

No es necesario instalar Kali Linux ni utilizar herramientas de escaneo adicionales.

### 4.2. Preparación del entorno

1. **Paso 1.** Enciende tu computadora y verifica que tenga acceso a Internet.
2. **Paso 2.** Abre tu navegador web.
3. **Paso 3.** Escribe la dirección [https://www.shodan.io](https://www.shodan.io) en la barra del navegador.
4. **Paso 4.** Espera a que cargue la página principal.
5. **Paso 5.** Identifica el cuadro de búsqueda, que será el elemento principal para realizar las consultas.
6. **Paso 6.** Si la plataforma solicita iniciar sesión, utiliza una cuenta propia. Si no tienes una, revisa las opciones de registro disponibles.
7. **Paso 7.** Comprueba que puedes acceder a la interfaz de búsqueda.

#### Verificación del entorno

Antes de continuar, comprueba que:

- [ ] Puedes abrir la página de Shodan.
- [ ] Identificas el cuadro donde se introducen las búsquedas.
- [ ] Tu cuenta, en caso de ser requerida, permite consultar los resultados necesarios.

> [!NOTE]
> Algunas funciones de Shodan, incluidos determinados filtros, resultados y capturas, pueden estar sujetas a limitaciones según el tipo de cuenta. Si una función no está disponible, podrás analizar los ejemplos explicados en esta actividad y completar la interpretación técnica correspondiente.

---

## 5. Ejercicio

### 5.1. Ejercicio 1. Identificación de servidores RDP expuestos en Internet

**Duración estimada:** 20–25 minutos.

#### Objetivo

Utilizar Shodan para localizar registros de equipos que ofrecen el servicio Remote Desktop Protocol (RDP) y analizar la información técnica disponible.

#### Contexto técnico

Remote Desktop Protocol (RDP) es un protocolo desarrollado por Microsoft que permite establecer sesiones de escritorio remoto.

Mediante este servicio, un usuario autorizado puede conectarse a un equipo remoto para interactuar con su entorno gráfico.

RDP utiliza habitualmente el puerto TCP **3389**.

Cuando este servicio está expuesto directamente a Internet, puede representar un riesgo si se combina con configuraciones inseguras, credenciales débiles, vulnerabilidades o controles de acceso insuficientes.

No obstante, **tener el puerto 3389 accesible no demuestra que un equipo sea vulnerable**.

#### Parte 1. Realización de la búsqueda

1. **Paso 1.** Abre el navegador web y entra a [Shodan](https://www.shodan.io).
2. **Paso 2.** Ubica el cuadro principal de búsqueda.
3. **Paso 3.** Introduce la siguiente consulta, respetando su sintaxis:

   ```text
   screenshot.label:desktop has_screenshot:1 -screenshot.label:blank country:"MX" city:"Mexico City" product:"Remote Desktop Protocol"
   ```

4. **Paso 4.** Presiona la tecla **Enter**.
5. **Paso 5.** Espera a que Shodan procese la consulta y muestre los resultados disponibles.
6. **Paso 6.** Observa el área de resultados. Si está disponible, identifica el contador que indica cuántos registros coinciden con los filtros.
7. **Paso 7.** Registra la cantidad de resultados obtenidos junto con la fecha de la consulta.

#### Parte 2. Comprensión de la consulta

La búsqueda combina diferentes filtros que permiten limitar los resultados.

| Filtro | Función |
|---|---|
| `screenshot.label:desktop` | Busca registros con capturas clasificadas como escritorio. |
| `has_screenshot:1` | Limita la búsqueda a registros con captura disponible. |
| `-screenshot.label:blank` | Excluye registros cuyas capturas estén clasificadas como vacías. |
| `country:"MX"` | Limita los resultados a México. |
| `city:"Mexico City"` | Filtra los registros que Shodan asocia con Ciudad de México. |
| `product:"Remote Desktop Protocol"` | Busca registros identificados con el servicio RDP. |

8. **Paso 8.** Observa cómo cada filtro contribuye a restringir el conjunto de resultados.
9. **Paso 9.** Identifica los filtros relacionados con la ubicación geográfica, las capturas de pantalla y el servicio de red.
10. **Paso 10.** Registra la función que cumple cada grupo de filtros en la consulta.

#### Parte 3. Interpretación de los resultados

Como ejemplo de referencia, considera una consulta histórica en la que se identificaron **1,399 registros** asociados con el protocolo RDP en Ciudad de México.

> **Ejemplo de resultados:** 1,399 registros RDP. Esta cifra es histórica y **no** representa una cantidad actual.

11. **Paso 11.** Compara esa cantidad de referencia con el número que muestra tu consulta.
12. **Paso 12.** Comprueba si obtuviste una cantidad mayor, menor o si la plataforma no permite mostrar el contador.
13. **Paso 13.** Registra tu observación.

Las diferencias pueden deberse a actualizaciones del índice, cambios en los dispositivos conectados, filtros o limitaciones de acceso.

#### Parte 4. Análisis de un registro RDP

Los resultados de Shodan pueden proporcionar información sobre los servicios identificados.

Entre los campos más relevantes se encuentran:

| Campo | Qué debes identificar |
|---|---|
| IP Address | Dirección IP pública asociada al registro. |
| Port | Número de puerto donde Shodan detectó el servicio. |
| Protocol/Product | Protocolo o producto identificado. |
| Country | País asociado al registro. |
| City | Ciudad reportada por la plataforma. |
| Organization | Organización asociada con la dirección IP. |
| ISP | Proveedor de servicios de Internet. |
| ASN | Número identificador de un sistema autónomo de Internet. |
| Operating System | Sistema operativo, cuando Shodan logra identificarlo. |

14. **Paso 14.** Selecciona un registro de la lista de resultados, cuando tu cuenta permita visualizar sus detalles.
15. **Paso 15.** Examina únicamente la información técnica que Shodan haya indexado.
16. **Paso 16.** Localiza el apartado donde se muestra la dirección IP del dispositivo.
17. **Paso 17.** Identifica el puerto relacionado con el servicio RDP. Habitualmente encontrarás el puerto TCP 3389, aunque pueden existir configuraciones con puertos distintos.
18. **Paso 18.** Observa los campos de ubicación, organización y proveedor de Internet, si están disponibles.
19. **Paso 19.** Identifica si existe información relacionada con el sistema operativo.
20. **Paso 20.** Completa el siguiente registro de observaciones, utilizando datos generales y evitando publicar identificadores sensibles de terceros.

| Elemento | Resultado de tu investigación |
|---|---|
| Fecha de consulta | |
| País identificado | |
| Ciudad identificada | |
| Servicio encontrado | |
| Puerto identificado | |
| Información del sistema operativo disponible | |
| Riesgo potencial identificado | |

#### Parte 5. Identificación del sistema operativo

Un registro de Shodan puede mostrar información relacionada con el sistema operativo del dispositivo, por ejemplo, una referencia a **Windows Server 2008**.

Este sistema operativo es relevante para una evaluación de seguridad porque las versiones antiguas pueden haber finalizado su periodo de soporte y requieren una revisión especial de actualizaciones y controles de protección.

21. **Paso 21.** Revisa la información del registro seleccionado.
22. **Paso 22.** Identifica si Shodan muestra el nombre o la versión de un sistema operativo.
23. **Paso 23.** Si la información está disponible, anota el nombre del sistema operativo.
24. **Paso 24.** Si no se muestra, registra «No identificado».
25. **Paso 25.** Relaciona la versión identificada con sus posibles implicaciones de seguridad y registra una observación técnica breve.

#### Resultado esperado

Al finalizar este ejercicio deberás ser capaz de interpretar una consulta de Shodan orientada a RDP, reconocer los filtros utilizados y describir los principales elementos técnicos de un registro.

#### Recomendaciones de seguridad

Para reducir la exposición de servicios RDP, una organización puede considerar controles como:

- Evitar la publicación directa de RDP cuando no sea necesario.
- Utilizar una VPN o un mecanismo seguro de acceso remoto.
- Implementar autenticación multifactor cuando corresponda.
- Restringir el acceso mediante firewalls y listas de direcciones autorizadas.
- Mantener los sistemas operativos y servicios actualizados.
- Supervisar los intentos de autenticación y conexiones remotas.

---

### 5.2. Ejercicio 2. Búsqueda de cámaras web expuestas

**Duración estimada:** 15–20 minutos.

#### Objetivo

Utilizar Shodan para localizar información indexada relacionada con cámaras web y comprender los riesgos de privacidad y seguridad asociados con su exposición a Internet.

#### Contexto técnico

Las cámaras IP son dispositivos que permiten capturar y transmitir imágenes mediante redes informáticas.

Estos dispositivos se utilizan en hogares, oficinas, instalaciones industriales y sistemas de videovigilancia.

Al igual que otros dispositivos IoT, pueden ofrecer servicios de administración, interfaces web y mecanismos de transmisión de video.

Una configuración incorrecta podría permitir que determinada información técnica o visual quede expuesta a usuarios externos.

#### Parte 1. Búsqueda de cámaras web

1. **Paso 1.** Regresa a la página principal de Shodan o utiliza el cuadro de búsqueda disponible.
2. **Paso 2.** Elimina la consulta anterior.
3. **Paso 3.** Introduce la siguiente consulta:

   ```text
   screenshot.label:webcam screenshot.label:webcam has_screenshot:1 -screenshot.label:blank country:"MX"
   ```

4. **Paso 4.** Presiona **Enter**.
5. **Paso 5.** Espera a que Shodan muestre los resultados.
6. **Paso 6.** Observa si aparecen registros relacionados con dispositivos de videovigilancia.
7. **Paso 7.** Identifica el número de resultados, si la plataforma lo presenta.

> [!NOTE]
> La consulta contiene dos veces el filtro `screenshot.label:webcam`. Esta repetición no es necesaria para expresar la búsqueda y puede eliminarse si se desea simplificarla.

#### Parte 2. Interpretación de los filtros

| Filtro | Descripción |
|---|---|
| `screenshot.label:webcam` | Busca capturas clasificadas como imágenes relacionadas con cámaras web. |
| `has_screenshot:1` | Solicita registros que incluyen una captura indexada. |
| `-screenshot.label:blank` | Excluye registros cuya captura está clasificada como vacía. |
| `country:"MX"` | Limita los resultados a dispositivos asociados con México. |

8. **Paso 8.** Identifica cuáles de los filtros buscan información relacionada con las imágenes.
9. **Paso 9.** Observa la función del filtro geográfico `country:"MX"`.
10. **Paso 10.** Registra el propósito de los filtros que componen la consulta.

#### Parte 3. Análisis de la información disponible

11. **Paso 11.** Examina los títulos, descripciones y campos técnicos generales de los resultados indexados.
12. **Paso 12.** Identifica, cuando estén disponibles, la información de ubicación, los puertos y el tipo de servicio.
13. **Paso 13.** Observa qué información puede revelar Shodan sobre la tecnología de un dispositivo.
14. **Paso 14.** No abras transmisiones privadas ni intentes acceder a los paneles de administración de las cámaras encontradas.
15. **Paso 15.** Completa la siguiente tabla:

| Elemento | Observación |
|---|---|
| Fecha de consulta | |
| País consultado | México |
| Tipo de dispositivo | |
| Puertos identificados | |
| Producto o servicio identificado | |
| Riesgo potencial para la privacidad | |
| Control de seguridad recomendado | |

#### Parte 4. Evaluación de riesgos

La exposición de sistemas de videovigilancia puede representar riesgos importantes cuando no existen controles de acceso adecuados.

Entre los posibles riesgos destacan:

- Divulgación de imágenes privadas.
- Exposición de información relacionada con ubicaciones físicas.
- Uso de configuraciones o credenciales inseguras.
- Acceso no autorizado a las funciones de administración.
- Posible utilización de dispositivos comprometidos como puntos de entrada a una red.

16. **Paso 16.** Considera el siguiente escenario:

    > Una empresa instala cámaras IP para supervisar sus instalaciones. El administrador configura las cámaras para permitir su consulta remota, pero no restringe adecuadamente el acceso desde Internet.

17. **Paso 17.** Identifica los principales riesgos asociados con esa configuración.
18. **Paso 18.** Selecciona al menos tres controles de seguridad que puedan reducir la exposición de las cámaras IP.
19. **Paso 19.** Registra los riesgos y las medidas preventivas seleccionadas en tus observaciones.

#### Resultado esperado

Deberás comprender cómo Shodan permite localizar información indexada sobre dispositivos IoT y reconocer las implicaciones de seguridad y privacidad de publicar sus servicios en Internet.

#### Recomendaciones de seguridad

- Cambiar las credenciales predeterminadas.
- Mantener actualizado el firmware.
- Deshabilitar funciones de acceso remoto que no sean necesarias.
- Restringir el acceso mediante firewalls o VPN.
- Separar los dispositivos IoT de las redes que contienen sistemas críticos.
- Supervisar periódicamente los dispositivos publicados en Internet.

---

### 5.3. Problemas frecuentes

#### Problema 1. Shodan no muestra resultados

**Posibles causas:** filtros restrictivos, ausencia de registros coincidentes o limitaciones de acceso.

**Solución:**

1. Verifica que la consulta se haya escrito correctamente.
2. Revisa las comillas y los espacios entre filtros.
3. Prueba una consulta general, como `product:"Remote Desktop Protocol"`, para familiarizarte con el funcionamiento del buscador.
4. Si Shodan no devuelve información, continúa con el análisis de los ejemplos explicados en la actividad.

#### Problema 2. La cantidad de resultados es diferente

La información indexada cambia constantemente. La cantidad de dispositivos puede variar debido a nuevas exploraciones realizadas por Shodan, desconexiones de equipos o cambios en sus servicios.

**Solución:** registra el número que aparece durante tu búsqueda y la fecha en que realizaste la consulta. No es necesario reproducir una cantidad histórica.

#### Problema 3. Algunos filtros no funcionan

Shodan puede limitar ciertas capacidades según las características de la cuenta.

**Solución:** confirma que has iniciado sesión y comprueba si tu plan permite utilizar las funciones solicitadas. Si no están disponibles, interpreta los filtros y registra la limitación como parte de tus observaciones.

#### Problema 4. No se muestra información del sistema operativo

Shodan no siempre puede identificar correctamente el sistema operativo de un dispositivo.

**Solución:** registra que la información no está disponible. No debes establecer conexiones activas para intentar obtenerla en esta actividad.

#### Problema 5. La interfaz es diferente

Shodan puede actualizar el diseño de su plataforma.

**Solución:** utiliza los nombres de los campos, filtros y funciones para orientarte, aunque la posición de los elementos visuales haya cambiado.

---

## 6. Evidencias de aprendizaje

Para demostrar que realizaste las actividades, prepara un documento breve que contenga los siguientes elementos:

- [ ] Captura de pantalla de la consulta de servidores RDP.
- [ ] Cantidad de resultados RDP y fecha de consulta.
- [ ] Tabla de interpretación técnica de los registros RDP.
- [ ] Captura de pantalla de la consulta de cámaras web.
- [ ] Tabla de interpretación de los resultados relacionados con cámaras.
- [ ] Breve descripción de los riesgos identificados en cada ejercicio.
- [ ] Recomendaciones de seguridad aplicables a los servicios y dispositivos analizados.
- [ ] Conclusión personal sobre la importancia del reconocimiento pasivo en Ethical Hacking.

> [!CAUTION]
> En las capturas que compartas, oculta cualquier dirección IP pública, información privada o identificador sensible de terceros.

---

## 7. Conclusiones

Shodan es una herramienta importante dentro de las actividades de reconocimiento pasivo en Ethical Hacking, ya que facilita la identificación de dispositivos, servicios e información técnica indexada a partir de sistemas accesibles desde Internet.

Durante esta práctica utilizaste filtros de búsqueda para investigar servicios RDP y dispositivos relacionados con cámaras web, además de interpretar información como puertos, protocolos, ubicación geográfica y características técnicas de los sistemas.

Estas actividades permiten comprender cómo la información públicamente disponible puede ayudar a identificar y evaluar la superficie de ataque de una organización.

También es importante reconocer que **la identificación de un servicio expuesto no constituye por sí misma la confirmación de una vulnerabilidad**. Los resultados deben analizarse en su contexto y cualquier validación activa posterior requiere autorización expresa.

La documentación de hallazgos, la interpretación de resultados y la formulación de recomendaciones son habilidades fundamentales para un profesional de ciberseguridad.

---

## 8. Referencias

- [Shodan — Plataforma oficial](https://www.shodan.io)
- [Shodan — Centro de ayuda](https://help.shodan.io)
- [Shodan — Filtros de búsqueda](https://www.shodan.io/search/filters)
- [OWASP — Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [NIST — Cybersecurity Framework](https://www.nist.gov/cyberframework)
