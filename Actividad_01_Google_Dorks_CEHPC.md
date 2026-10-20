# Ethical Hacking

## Actividad 01. Google Dorks

**Ethical Hacking Professional Certification (CEHPC)**

| Característica | Descripción |
|---|---|
| **Duración estimada** | 45–60 minutos |
| **Nivel** | Básico |
| **Herramienta** | Google |
| **Modalidad** | Práctica individual, presencial o autodirigida |

---

## 1. Introducción

**Google Dorks**, también conocido como *Google Hacking*, es una técnica que utiliza operadores avanzados de búsqueda para localizar información específica en Internet.

Estos operadores permiten encontrar documentos, directorios, páginas web y otros recursos que no siempre aparecen fácilmente mediante búsquedas convencionales.

En **Ethical Hacking**, Google Dorks se utiliza principalmente durante la fase de **reconocimiento pasivo**, con el propósito de recopilar información pública e identificar posibles riesgos de seguridad.

Por ejemplo, mediante búsquedas avanzadas es posible identificar:

- Documentos publicados en servidores web.
- Directorios y archivos indexados.
- Páginas que muestran información técnica.
- Posibles exposiciones de información confidencial.
- Recursos relacionados con aplicaciones web.

### Operadores básicos de Google

| Operador | Descripción | Ejemplo |
|---|---|---|
| `site:` | Busca información dentro de un dominio. | `site:example.com` |
| `inurl:` | Busca términos dentro de una URL. | `inurl:index.php` |
| `intitle:` | Busca términos en el título de una página. | `intitle:"Index of"` |
| `filetype:` | Busca archivos de un formato específico. | `filetype:pdf` |
| `intext:` | Busca términos en el contenido indexado. | `intext:"security"` |
| `" "` | Busca una expresión exacta. | `"Confidential"` |

> **Importante:** La información localizada mediante Google Dorks puede representar un indicio de exposición, pero no confirma por sí misma la existencia de una vulnerabilidad.

<img width="1774" height="887" alt="2 Guía Visual de Google Dorks en Español" src="https://github.com/user-attachments/assets/4b56bf51-b64b-4d61-a68d-7d7aa4172ff7" />


---

## 2. Objetivos

El objetivo principal de esta actividad es utilizar Google Dorks para localizar información mediante búsquedas avanzadas y comprender cómo esta técnica contribuye a identificar posibles debilidades de seguridad.

Al finalizar la actividad, serás capaz de:

1. Comprender el funcionamiento de Google Dorks.
2. Utilizar operadores avanzados de búsqueda.
3. Identificar páginas con parámetros que podrían ser relevantes para SQL Injection.
4. Reconocer archivos y directorios potencialmente expuestos.
5. Localizar documentos mediante búsquedas específicas.
6. Interpretar resultados e identificar posibles riesgos de seguridad.

---

## 3. Alcance

Google Dorks puede utilizarse en diferentes actividades:

1. **Seguridad informática:** Identificación de archivos, directorios y recursos potencialmente expuestos.
2. **Investigación de vulnerabilidades:** Localización de información que puede ayudar a identificar posibles debilidades en aplicaciones web.
3. **Análisis SEO:** Identificación de páginas y documentos indexados en motores de búsqueda.
4. **Recolección de información:** Búsqueda de documentos, archivos y otra información disponible públicamente.
5. **Auditoría de seguridad:** Evaluación de la información que una organización expone en Internet.

### Consideraciones de seguridad

Las actividades de reconocimiento deberán realizarse respetando los límites éticos y legales del hacking ético.

Puedes realizar consultas sobre información indexada públicamente. Sin embargo, cualquier prueba activa de seguridad debe ejecutarse únicamente sobre sistemas propios o expresamente autorizados.

No intentes acceder a credenciales, descargar archivos sensibles de terceros ni explotar posibles vulnerabilidades.

---

## 4. Herramientas Utilizadas

### Google

Google es un motor de búsqueda que permite localizar información publicada en Internet mediante consultas convencionales y operadores avanzados.

**Sitio web:** [https://www.google.com](https://www.google.com)

### Requisitos

Para realizar esta actividad necesitas:

- Computadora con conexión a Internet.
- Navegador web actualizado, como Chrome, Firefox o Edge.
- Acceso al motor de búsqueda Google.

No es necesario instalar herramientas adicionales ni disponer de conocimientos avanzados de ciberseguridad.

### Preparación

1. Abre tu navegador web.
2. Ingresa a [https://www.google.com](https://www.google.com).
3. Comprueba que puedes realizar búsquedas.
4. Mantén abierta la pestaña de Google para realizar los ejercicios.

---

## 5. Ejercicio

### 5.1. Exploración de Google Dorks

Antes de comenzar, conocerás algunas consultas que pueden utilizarse durante una investigación de seguridad.

**Paso 1.** Abre una nueva pestaña en tu navegador.

**Paso 2.** Ingresa a la siguiente dirección:

[https://www.boxpiper.com/posts/top-35-google-dorks-list](https://www.boxpiper.com/posts/top-35-google-dorks-list)

**Paso 3.** Examina las consultas disponibles e identifica operadores como `inurl:`, `intitle:` y `filetype:`.

**Paso 4.** Observa cómo se combinan los operadores con palabras clave para obtener resultados específicos.

**Paso 5.** Regresa a Google para comenzar los ejercicios.

Esta lista contiene ejemplos de consultas, pero también puedes construir tus propias combinaciones de acuerdo con la información que necesites localizar.

> **Nota:** Si el sitio web no está disponible, puedes continuar directamente con los ejemplos incluidos en esta actividad.

### 5.2. Ejercicio 1. Identificación de posibles vulnerabilidades SQL Injection

#### Objetivo

Identificar páginas web que utilizan parámetros en sus direcciones URL y comprender cómo ciertos errores pueden proporcionar información sobre el funcionamiento de una aplicación.

#### Contexto

**SQL Injection** es una vulnerabilidad que puede presentarse cuando una aplicación web procesa incorrectamente datos proporcionados por el usuario y los incorpora en consultas a una base de datos.

Por ejemplo, considera esta dirección:

```text
https://example.com/index.php?id=10
```

En ella, el parámetro `id=10` podría utilizarse para identificar un registro almacenado en una base de datos.

La presencia de este parámetro no significa necesariamente que exista una vulnerabilidad.

#### Parte 1. Búsqueda de páginas web

**Paso 1.** Abre Google.

**Paso 2.** Escribe la siguiente consulta:

```text
inurl:index.php?id=
```
<img width="1672" height="941" alt="3 Guía visual para buscar en Google" src="https://github.com/user-attachments/assets/0891e85f-33d0-44ed-9009-2ba1f544c9bc" />

**Paso 3.** Presiona Enter para ejecutar la búsqueda.

**Paso 4.** Observa los resultados e identifica las direcciones URL que contengan parámetros similares a `id=10`.

**Paso 5.** Examina los componentes de las direcciones URL:

- **Dominio:** Identifica el sitio web.
- **Archivo:** Representa el recurso solicitado, por ejemplo `index.php`.
- **Parámetro:** Identifica el dato enviado, por ejemplo `id`.
- **Valor:** Representa la información asignada al parámetro, por ejemplo `10`.

**Paso 6.** Observa cómo diferentes páginas pueden utilizar parámetros para consultar o mostrar información.

**Resultado esperado:** Identificar direcciones URL con parámetros y comprender su funcionamiento básico.

<img width="1672" height="941" alt="4 Partes de una URL web" src="https://github.com/user-attachments/assets/1d4c963a-0596-41ee-8f30-1707cf80f8e4" />


#### Parte 2. Identificación de errores SQL

En algunas aplicaciones vulnerables, la modificación de un parámetro puede provocar mensajes de error relacionados con SQL o MySQL.

<img width="1672" height="941" alt="5 Infografía de error SQL en navegador" src="https://github.com/user-attachments/assets/b625cf9e-7e76-4ddf-9fd0-792edcc45141" />


Una comprobación conocida consiste en agregar una comilla simple (`'`) al final del valor de un parámetro.

Para comprender este comportamiento, utilizaremos el siguiente ejemplo:

**Dirección normal:**

```text
https://example.com/index.php?id=10
```

**Dirección modificada:**

```text
https://example.com/index.php?id=10'
```

La dirección es ilustrativa y no corresponde a una aplicación de pruebas.

#### Procedimiento

**Paso 1.** Compara ambas direcciones y observa la comilla simple agregada al final del parámetro.

**Paso 2.** Examina la siguiente representación de un posible mensaje de error:

```text
You have an error in your SQL syntax;
check the manual that corresponds to
your MySQL server version.
```

**Paso 3.** Identifica las palabras `SQL syntax` y `MySQL server` dentro del mensaje.

**Paso 4.** Reconoce que el mensaje está relacionado con una operación de base de datos.

**Paso 5.** Relaciona este comportamiento con las aplicaciones que utilizan parámetros de entrada para construir consultas SQL.

> **Seguridad:** No ejecutes la comprobación sobre sitios externos sin autorización. Para observarla de manera práctica, puedes utilizar una aplicación vulnerable instalada en un laboratorio local y aislado que sea de tu propiedad.

#### Interpretación del resultado

Cuando una aplicación muestra errores internos de SQL, podría revelar detalles sobre su funcionamiento.

Esto puede indicar una deficiencia en el tratamiento de entradas o en la gestión de errores.

Sin embargo, un mensaje de error no confirma por sí mismo que una vulnerabilidad pueda explotarse.

**Recomendación de seguridad:** Utilizar consultas parametrizadas, validar entradas y evitar mostrar errores internos detallados.

### 5.3. Ejercicio 2. Búsqueda de archivos de contraseñas expuestos

#### Objetivo

Identificar directorios indexados que podrían contener archivos relacionados con contraseñas y comprender los riesgos asociados a su exposición.

#### Contexto

Algunos servidores web permiten visualizar el contenido de sus directorios mediante una página que muestra los archivos y carpetas disponibles.

Este comportamiento se conoce como *Directory Listing*.

Frecuentemente, estos listados presentan títulos como:

```text
Index of /
```

Si un administrador publica accidentalmente archivos confidenciales dentro de un directorio accesible, estos podrían quedar expuestos.

#### Procedimiento

**Paso 1.** Abre Google.

**Paso 2.** Introduce la siguiente consulta:

```text
intitle:"Index of" password.txt
```

<img width="1672" height="941" alt="6 Guía visual de búsqueda avanzada en Google" src="https://github.com/user-attachments/assets/98be1ddb-8609-4b35-b968-47997f2fb2de" />


**Paso 3.** Presiona Enter.

**Paso 4.** Observa los resultados que aparecen en el buscador.

**Paso 5.** Identifica resultados que mencionen directorios o archivos denominados `password.txt`.

**Paso 6.** Examina los títulos y las descripciones de los resultados sin acceder a archivos de contraseñas de terceros.

#### Interpretación de la consulta

- `intitle:"Index of"` busca páginas cuyo título incluya la expresión indicada.
- `password.txt` representa el nombre del archivo que se desea localizar.

La combinación permite identificar posibles listados de directorios relacionados con ese nombre de archivo.

#### Ejemplo de un directorio expuesto

Considera el siguiente listado ficticio de un servidor web:

```text
Index of /archivos/

manual.pdf
imagenes/
notas.txt
password.txt
```

El listado muestra diferentes archivos almacenados en un directorio.

Si `password.txt` contuviera credenciales reales y pudiera consultarse sin autorización, existiría un riesgo para la confidencialidad de la información.

<img width="1600" height="900" alt="_7_directorio_indexado" src="https://github.com/user-attachments/assets/419141bb-3136-4737-aa94-68f20c514f21" />


**Resultado esperado:** Comprender cómo los motores de búsqueda pueden localizar directorios indexados y por qué la publicación de archivos sensibles representa un riesgo.

**Recomendación de seguridad:** Deshabilitar el listado de directorios cuando no sea necesario, restringir el acceso a archivos sensibles y evitar almacenar contraseñas en texto plano.

### 5.4. Ejercicio 3. Búsqueda de documentos confidenciales

#### Objetivo

Utilizar operadores avanzados para localizar documentos PDF indexados y reconocer posibles riesgos relacionados con la publicación de información.

<img width="1600" height="900" alt="7 busqueda_google_pdf_confidential" src="https://github.com/user-attachments/assets/78db6740-8018-4b4f-9e5a-37d9f09d1ded" />


#### Contexto

Los motores de búsqueda pueden indexar documentos almacenados en servidores web.

Cuando una organización publica archivos sin los controles adecuados, determinados documentos internos podrían quedar disponibles para usuarios externos.

Google permite realizar búsquedas específicas mediante el operador `filetype:`.

#### Procedimiento

**Paso 1.** Abre Google.

**Paso 2.** Introduce la siguiente consulta:

```text
filetype:pdf "Confidential"
```

**Paso 3.** Presiona Enter.

**Paso 4.** Observa los resultados obtenidos.

**Paso 5.** Identifica los documentos PDF a partir de sus títulos y descripciones.

**Paso 6.** Observa la cantidad aproximada de resultados, si Google la muestra.

**Paso 7.** Examina cómo los documentos encontrados se relacionan con la palabra utilizada en la búsqueda.

#### Interpretación de la consulta

- `filetype:pdf` limita la búsqueda a documentos PDF.
- `"Confidential"` busca la expresión exacta indicada entre comillas.

La combinación permite localizar documentos PDF relacionados con esa expresión.

> **Importante:** Que un documento incluya la palabra «Confidential» no significa necesariamente que contenga información privada o que exista una filtración.

#### Actividad complementaria

**Paso 1.** Regresa al cuadro de búsqueda de Google.

**Paso 2.** Sustituye la consulta anterior por:

```text
filetype:pdf "cybersecurity"
```

**Paso 3.** Presiona Enter.

**Paso 4.** Observa cómo cambian los resultados cuando se utiliza una palabra clave diferente.

**Paso 5.** Compara los títulos y tipos de documentos que aparecen en ambas búsquedas.

**Resultado esperado:** Comprender cómo utilizar el operador `filetype:` para localizar documentos específicos y cómo las palabras clave influyen en los resultados.

**Recomendación de seguridad:** Aplicar controles de acceso, revisar los archivos publicados y evitar almacenar información privada en ubicaciones accesibles públicamente.

### 5.5. Problemas frecuentes

**1. Google no devuelve resultados.**

Verifica que hayas escrito correctamente los operadores y las palabras clave. La ausencia de resultados también puede deberse a que el contenido ya no está indexado.

**2. Los resultados son diferentes a los ejemplos.**

La información indexada cambia constantemente. Los resultados pueden variar dependiendo de la fecha, la ubicación y las políticas del buscador.

**3. El enlace de referencia no está disponible.**

Puedes continuar utilizando las consultas incluidas en esta actividad.

**4. No aparecen páginas con los parámetros esperados.**

Prueba a realizar una búsqueda más general, como `inurl:index.php`, para comprender cómo funciona el operador.

**5. No aparece la cantidad aproximada de resultados.**

Google puede modificar la manera de presentar esta información. La consulta sigue siendo válida aunque no se muestre una cifra.

### 5.6. Conclusiones

Google Dorks es una técnica de reconocimiento pasivo que permite localizar información específica mediante operadores avanzados de Google.

Durante esta actividad exploraste tres escenarios: identificación de páginas con parámetros relacionados con SQL Injection, búsqueda de archivos potencialmente expuestos y localización de documentos PDF indexados.

Estas técnicas permiten comprender cómo la información publicada en Internet puede convertirse en un elemento importante durante una evaluación de seguridad.

<img width="1536" height="1024" alt="10 De Google al PDF_ credenciales expuestas" src="https://github.com/user-attachments/assets/53a41212-df3c-4de2-bd0a-7567e4af005e" />


Recuerda que **encontrar información no significa haber confirmado una vulnerabilidad**. Un profesional de ethical hacking debe interpretar los resultados correctamente y respetar siempre los límites de autorización establecidos.

---

## Referencias

- [Google](https://www.google.com)
- [Google Dorks List](https://www.boxpiper.com/posts/top-35-google-dorks-list)
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [OWASP SQL Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
