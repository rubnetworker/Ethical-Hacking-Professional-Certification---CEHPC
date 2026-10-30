# Actividad 08 | Presentación ejecutiva de resultados de pentesting

> **Ethical Hacking Professional Certification (CEHPC)** · Módulo 8: Informe de resultados · Modalidad: práctica integradora · Nivel: básico–intermedio · Duración sugerida: 120 minutos

[Inicio](#descripción) · [Caso práctico](#caso-práctico-simulado) · [Presentación completa](#guion-de-la-presentación-ejecutiva) · [Actividad](#actividad-del-participante) · [Evaluación](#rúbrica-de-evaluación)

## Descripción

En una prueba de penetración, el trabajo no termina al identificar vulnerabilidades. Los resultados deben comunicarse de forma comprensible, verificable y útil para tomar decisiones. Esta actividad enseña a convertir hallazgos técnicos en una **presentación ejecutiva de resultados** dirigida a responsables de TI y de negocio.

Este README **contiene todo lo necesario para realizar la actividad**: objetivos, escenario, datos simulados, estructura y texto de una presentación de 12 diapositivas, ejercicios, modelo de ficha de hallazgo, plan de remediación, criterios de evaluación y lista de verificación. No es necesario descargar archivos ni consultar anexos.

**Relación con otras actividades CEHPC:** esta práctica cierra el ciclo iniciado en reconocimiento pasivo y activo, escaneo y análisis de red, análisis de vulnerabilidades y validación controlada de hallazgos. Puede trabajarse por separado o con evidencias generadas en actividades anteriores.

> [!IMPORTANT]
> **Uso exclusivamente educativo y autorizado.** Toda la organización, los activos, las pruebas y los resultados del caso *NovaCommerce* son ficticios. No se ejecutaron pruebas reales. Cualquier escaneo o validación adicional debe realizarse únicamente en laboratorios propios, aislados o expresamente autorizados. No se requieren ataques activos para completar esta actividad.

## Objetivo de aprendizaje

**Objetivo general:** elaborar y defender una presentación ejecutiva de resultados de pentesting que comunique el alcance de las pruebas, el nivel de exposición, los hallazgos prioritarios y las acciones de mitigación recomendadas.

Al terminar, el participante podrá:

1. Diferenciar la finalidad de un **informe técnico** frente a una **presentación ejecutiva**.
2. Sintetizar un conjunto de hallazgos sin perder trazabilidad ni exagerar las conclusiones.
3. Relacionar vulnerabilidades con impactos potenciales en **confidencialidad, integridad y disponibilidad (CID)**.
4. Priorizar medidas correctivas según severidad, criticidad del activo y exposición.
5. Comunicar decisiones, responsables y plazos con lenguaje adecuado para la dirección.

### Conceptos fundamentales

| Concepto | Significado en esta actividad |
|---|---|
| Pentesting | Evaluación autorizada que intenta comprobar debilidades de seguridad dentro de un alcance acordado. |
| Enfoque de caja negra (*black box*) | Evaluación realizada sin disponer inicialmente de detalles internos de arquitectura o configuración. |
| Hallazgo | Debilidad observada y documentada, con su evidencia y recomendación. |
| CVE | Identificador público de una vulnerabilidad conocida; **no todos los hallazgos tienen CVE**. |
| CVSS | Sistema de puntuación de **severidad técnica**. No equivale por sí solo al riesgo empresarial. |
| Riesgo | Valoración contextual que considera la probabilidad y las consecuencias para el negocio. |
| Evidencia | Registro verificable que fundamenta una observación o comprobación. |
| Remediación | Acción destinada a corregir o reducir una debilidad y verificar la efectividad del cambio. |

## Caso práctico simulado

### Organización y solicitud

**NovaCommerce** es una empresa ficticia de comercio electrónico. Su dirección solicita una revisión de exposición tecnológica para conocer si las aplicaciones públicas y los servicios asociados cuentan con medidas suficientes de protección.

**Objetivo de negocio:** reducir la posibilidad de interrupciones de ventas, accesos indebidos y divulgación de información de clientes.

**Tipo de evaluación:** prueba de seguridad externa con enfoque de caja negra, presentada como ejercicio de formación.

**Periodo supuesto:** 5 al 9 de octubre de 2026. **Estado:** ejercicio de simulación documental; no existió ejecución real.

### Alcance y reglas

| Elemento | Definición para el caso |
|---|---|
| Portal de compras | `shop.novacommerce.example` |
| Panel administrativo | `admin.novacommerce.example` |
| API | `api.novacommerce.example` |
| Servicios publicados | Servicios asociados con estos tres activos ficticios. |
| Fuera de alcance | Redes internas, equipos personales, proveedores y cualquier infraestructura real. |
| Restricciones | Sin pruebas de denegación de servicio, sin extracción de datos y sin persistencia. |

El sufijo `.example` está reservado para documentación. Los nombres anteriores no deben tratarse como destinos de prueba reales.

### Metodología del ejercicio

1. **Definición y autorización del alcance:** activos, objetivos y límites.
2. **Reconocimiento:** revisión de información ficticia sobre activos y servicios publicados.
3. **Análisis:** revisión de los hallazgos simulados y su severidad.
4. **Validación documental:** contrastar cada observación con la evidencia simulada indicada, sin explotarla.
5. **Comunicación:** elaborar informe ejecutivo, recomendaciones y plan de atención.

Como referencia metodológica, en el material CEHPC se mencionan **PTES, OWASP y CAPEC**. Para este ejercicio se utilizan como marcos conceptuales; **no** se afirma que el caso haya ejecutado una evaluación completa de conformidad con dichos marcos.

## Resultados del caso

### Resumen general

Se proporcionan **8 hallazgos simulados**: **1 crítico, 2 altos, 3 medios y 2 bajos**. El **riesgo general ilustrativo es ALTO**, por la exposición del servicio administrativo, las debilidades de autenticación y la importancia operativa de los sistemas afectados. Esta valoración es una hipótesis pedagógica, no una medición real del riesgo de una empresa.

| Severidad | Cantidad | Proporción |
|---|---:|---:|
| Crítica | 1 | 12.5 % |
| Alta | 2 | 25 % |
| Media | 3 | 37.5 % |
| Baja | 2 | 25 % |
| **Total** | **8** | **100 %** |

**Lectura ejecutiva:** tres de ocho hallazgos presentan severidad alta o crítica (**37.5 %**). La prioridad no depende solo de contar hallazgos: también importa qué procesos del negocio podrían verse afectados.

### Matriz de hallazgos simulados

> Las puntuaciones siguientes son **valores didácticos asignados para practicar la clasificación**. No se calcularon vectores CVSS, no se verificaron con una calculadora y **no deben publicarse como puntuaciones oficiales**.

| ID | Hallazgo ficticio | Activo | Severidad | Puntuación ilustrativa | Impacto potencial (CID) | Estado |
|---|---|---|---|---:|---|---|
| H-01 | Control de acceso insuficiente en función administrativa | Panel admin. | Crítica | 9.1 | Confidencialidad / Integridad | Simulado |
| H-02 | Ausencia de autenticación multifactor en administración | Panel admin. | Alta | 8.1 | Confidencialidad / Integridad | Simulado |
| H-03 | Componentes de aplicación sin actualización documentada | Portal de compras | Alta | 7.5 | Confidencialidad / Disponibilidad | Simulado |
| H-04 | Cabeceras de seguridad web incompletas | Portal de compras | Media | 6.1 | Confidencialidad / Integridad | Simulado |
| H-05 | Política de intentos de autenticación insuficiente | Panel admin. | Media | 5.8 | Confidencialidad | Simulado |
| H-06 | Mensajes de error con detalles técnicos excesivos | API | Media | 5.3 | Confidencialidad | Simulado |
| H-07 | Información de versión expuesta en respuestas HTTP | Portal de compras | Baja | 3.7 | Confidencialidad | Simulado |
| H-08 | Políticas de caché mejorables para recursos no públicos | API | Baja | 3.1 | Confidencialidad | Simulado |

**Nota de interpretación:** algunos problemas de configuración no son directamente explotables y su impacto depende del contexto. En una evaluación real, cada fila necesita evidencia suficiente, una valoración fundamentada y, cuando proceda, su CVE o CWE correspondiente. Una ausencia de MFA no implica por sí sola una vulnerabilidad con CVSS definido.

### Evidencias simuladas, sin información sensible

Se proporciona una descripción resumida que puede utilizarse para redactar los informes. **No son registros de escaneo reales.**

| Hallazgo | Evidencia didáctica proporcionada | Límite de la afirmación |
|---|---|---|
| H-01 | Captura ficticia de un rol con acceso a una operación que debería estar restringida. | No demuestra acceso real a un sistema. |
| H-02 | Lista ficticia de factores de autenticación donde no aparece MFA para administradores. | Requeriría validación de políticas y flujos reales. |
| H-03 | Inventario de dependencias ficticio con versiones pendientes de revisión. | Sin CVE confirmada. |
| H-04 | Ejemplo de respuesta HTTP donde faltan cabeceras esperadas. | La severidad depende de la aplicación. |
| H-05 | Configuración ficticia sin límites claros de intentos. | No se efectuaron intentos de fuerza bruta. |
| H-06 | Ejemplo fabricado de un error que expone nombre de componente. | No se produjo divulgación real. |
| H-07 | Ejemplo de encabezado de versión de servidor. | La exposición de versión no demuestra explotación. |
| H-08 | Configuración de caché de ejemplo que requiere revisión. | No se observó almacenamiento real de datos sensibles. |

## Guion de la presentación ejecutiva

A continuación se ofrece el **contenido íntegro de las 12 diapositivas**. Puede exponerse directamente desde GitHub, leerse en clase o adaptarse a una presentación oral. No se necesita PowerPoint.

### Diapositiva 1. Portada

**Título:** Evaluación de seguridad externa — Informe ejecutivo

**Organización:** NovaCommerce (caso ficticio)  
**Periodo ilustrativo:** 5–9 de octubre de 2026  
**Tipo:** Evaluación de caja negra  
**Clasificación:** Material académico / no constituye auditoría real.

**Mensaje del expositor:** «Presentamos un ejercicio de comunicación ejecutiva que muestra cómo traducir observaciones de seguridad en decisiones de mitigación».

### Diapositiva 2. Resumen ejecutivo

**Mensaje clave:** El escenario simulado presenta una exposición general **ALTA** y requiere atención prioritaria de los controles administrativos.

- **8** hallazgos: 1 crítico, 2 altos, 3 medios y 2 bajos.
- **3 de 8** hallazgos se ubican en severidad alta o crítica.
- Las principales prioridades son **control de acceso**, **autenticación administrativa** y **actualización de componentes**.
- No se declara un incidente, filtración o interrupción real.

**Decisión solicitada:** aprobar el plan correctivo y asignar responsables.

### Diapositiva 3. Antecedentes y objetivos

**Situación:** El canal digital es importante para la operación comercial. Cualquier falla en sus sistemas públicos puede afectar confianza, atención a clientes y continuidad.

**Objetivos:**

1. Identificar debilidades potenciales en activos externos.
2. Determinar impactos posibles para el negocio.
3. Definir prioridades de tratamiento.
4. Facilitar seguimiento y comprobación de correcciones.

**Mensaje del expositor:** «La finalidad del trabajo no es contabilizar fallas, sino ofrecer información útil para proteger procesos críticos».

### Diapositiva 4. Alcance y restricciones

**Activos incluidos:** portal de compras, panel administrativo y API ficticios.

**Enfoque:** caja negra desde la perspectiva de un evaluador externo.

**Limitaciones:** el caso se resuelve documentalmente; no hubo pruebas reales, afectación de servicios ni acceso a datos. Las observaciones no describen toda la postura de seguridad de una organización.

**Mensaje del expositor:** «Las conclusiones aplican únicamente al alcance y a los datos suministrados».

### Diapositiva 5. Metodología aplicada

**Secuencia didáctica:** definir alcance → reconocer activos → analizar posibles debilidades → revisar evidencia simulada → priorizar → informar.

**Buenas prácticas de referencia:** PTES para organizar el proceso de pentesting; OWASP para comprender riesgos de aplicaciones web; CAPEC para relacionar patrones de ataque.

**Mensaje del expositor:** «La metodología hace trazable cómo se pasa de una observación a una recomendación».

### Diapositiva 6. Evaluación del riesgo general

**Resultado ilustrativo:** **ALTO**.

**Justificación:**

- Posible afectación del panel administrativo.
- Debilidades de acceso e identificación en funciones sensibles.
- Dependencia operativa de servicios públicos.

**Aclaración:** este nivel de riesgo se definió como supuesto del ejercicio. **CVSS mide severidad técnica y no sustituye un análisis contextual del riesgo empresarial.**

**Mensaje del expositor:** «Priorizamos por impacto operativo y exposición, no únicamente por una puntuación».

### Diapositiva 7. Distribución de hallazgos

| Crítica | Alta | Media | Baja | Total |
|---:|---:|---:|---:|---:|
| 1 | 2 | 3 | 2 | 8 |

Representación textual:

```text
Crítica  █         1 (12.5 %)
Alta     ██        2 (25.0 %)
Media    ███       3 (37.5 %)
Baja     ██        2 (25.0 %)
```

**Mensaje del expositor:** «El volumen más elevado está en riesgo medio, pero los hallazgos de mayor severidad concentran las decisiones inmediatas».

### Diapositiva 8. Hallazgos prioritarios

| Prioridad | ID | Debilidad | Por qué importa |
|---|---|---|---|
| 1 | H-01 | Control de acceso administrativo | Podría permitir operaciones fuera de los permisos previstos. |
| 2 | H-02 | Falta de MFA en administración | Debilita una barrera ante el uso indebido de credenciales. |
| 3 | H-03 | Componentes desactualizados | Requiere revisión de exposición y actualización. |

**Mensaje del expositor:** «Estas debilidades deben atenderse primero por la función de los activos afectados».

### Diapositiva 9. Impacto potencial en el negocio

**Confidencialidad:** posible exposición de información o funciones restringidas.

**Integridad:** posibilidad de cambios no previstos en operaciones administrativas.

**Disponibilidad:** dependencia de la operación comercial respecto de aplicaciones y componentes expuestos.

**Límites:** no se confirmó robo de información, alteración de datos ni interrupción del servicio.

**Mensaje del expositor:** «Describimos consecuencias posibles, no incidentes que hayan ocurrido».

### Diapositiva 10. Recomendaciones

1. **Control de acceso:** aplicar autorización del lado del servidor y revisar permisos por rol.
2. **Autenticación:** exigir MFA para cuentas administrativas y revisar mecanismos de recuperación.
3. **Actualización:** inventariar dependencias, validar versiones y corregir componentes vulnerables confirmados.
4. **Configuración web:** revisar cabeceras de seguridad, tratamiento de errores y políticas de caché.
5. **Detección:** establecer registros, alertas y revisiones periódicas de los controles.

**Mensaje del expositor:** «Las acciones deben verificarse para evitar que la corrección sea solo declarativa».

### Diapositiva 11. Plan de remediación

Los plazos son **metas sugeridas para el ejercicio**, no compromisos reales ni niveles de servicio universales.

| Prioridad | Acciones | Responsable propuesto | Plazo orientativo | Verificación |
|---|---|---|---|---|
| Inmediata | Revisar y restringir accesos H-01 | Desarrollo + Seguridad | 0–7 días | Pruebas de autorización por rol. |
| Alta | Habilitar MFA H-02 y revisar dependencias H-03 | Identidad + Desarrollo | 7–15 días | Evidencia de MFA y versiones revisadas. |
| Media | Corregir H-04 a H-06 | Desarrollo + Operaciones | 15–30 días | Revisión de configuración y errores. |
| Programada | Revisar H-07 y H-08 | Operaciones | 30–45 días | Inspección de encabezados y caché. |

**Decisión solicitada:** confirmar responsables, fechas objetivo y criterios de aceptación.

### Diapositiva 12. Conclusiones y próximos pasos

**Conclusión:** El escenario ficticio evidencia la utilidad de presentar resultados de pentesting en un formato que priorice decisiones de seguridad, impacto potencial y seguimiento.

**Próximos pasos:**

1. Validar los hallazgos con los equipos técnicos.
2. Aprobar acciones y responsables de remediación.
3. Ejecutar correcciones en un ambiente controlado.
4. Realizar una nueva validación autorizada.
5. Actualizar el estado de los hallazgos y comunicar el riesgo residual.

**Cierre sugerido:** «Una evaluación de seguridad aporta valor cuando sus observaciones se transforman en mejoras verificables y sostenibles».

## Actividad del participante

### Recursos necesarios

- Acceso a este README mediante GitHub o una copia local de su texto.
- Editor de texto o el editor Markdown de GitHub.
- Los datos simulados que aparecen en las secciones anteriores.
- **Opcional:** evidencias anonimizadas de un laboratorio CEHPC anterior, siempre que estén autorizadas para su uso.

No se necesitan cuentas de terceros, instalaciones nuevas, servicios de pago ni archivos descargables.

### Desarrollo sugerido (120 minutos)

| Fase | Tiempo | Trabajo solicitado |
|---|---:|---|
| 1. Comprensión del caso | 20 min | Leer alcance, objetivos y matriz de hallazgos. |
| 2. Análisis y priorización | 30 min | Justificar severidad, impacto y orden de atención. |
| 3. Redacción ejecutiva | 40 min | Adaptar las 12 diapositivas a mensajes claros y consistentes. |
| 4. Exposición y evaluación | 30 min | Presentar conclusiones, responder preguntas y completar revisión final. |
| **Total** | **120 min** | |

### Instrucciones paso a paso

**Paso 1. Comprender el alcance.** Identifica los tres activos, la perspectiva de caja negra y las limitaciones. Explica por qué no se pueden extrapolar las conclusiones a sistemas fuera de alcance.

**Paso 2. Revisar los hallazgos.** Para cada H-01 a H-08, registra el activo, la evidencia simulada, la posible afectación a CID y la recomendación. No inventes pruebas de explotación.

**Paso 3. Comprobar las cifras.** Verifica que la suma de severidades sea ocho y que sus porcentajes sean 100 %. Revisa que los tres hallazgos prioritarios coincidan con la matriz.

**Paso 4. Elaborar el mensaje ejecutivo.** Resume los resultados en un máximo de cinco ideas: qué se evaluó, qué se encontró, por qué importa, qué corregir primero y qué decisión se requiere.

**Paso 5. Completar la ficha de un hallazgo.** Utiliza la plantilla incluida más adelante. Elige H-01, H-02 o H-03 y justifica su prioridad sin confundir una hipótesis con un incidente confirmado.

**Paso 6. Preparar la exposición.** Usa el contenido de las doce diapositivas como guion. Evita detallar herramientas y comandos que no ayuden a decidir.

**Paso 7. Simular el comité directivo.** Responde las preguntas de reflexión. Si trabajas en equipo, una persona expone y otra representa a la dirección.

### Plantilla integrada: ficha de hallazgo

Copia y completa este bloque **dentro de tu propio README o en un comentario de entrega**, sin necesidad de otro archivo:

```markdown
#### Hallazgo: H-XX — [Nombre]

- **Activo:** [Sistema ficticio o activo de laboratorio autorizado]
- **Descripción:** [Qué condición se observó]
- **Evidencia:** [Descripción o referencia de evidencia disponible]
- **Estado de validación:** [Simulado / Observado / Confirmado / Pendiente]
- **Severidad:** [Crítica / Alta / Media / Baja, con justificación]
- **Impacto potencial en CID:** [Confidencialidad, integridad, disponibilidad]
- **Consecuencia para el negocio:** [Escenario posible, sin afirmar incidentes]
- **Recomendación:** [Acción correctiva concreta]
- **Responsable sugerido:** [Área]
- **Prioridad y plazo:** [Orden de atención y justificación]
- **Criterio de cierre:** [Cómo se comprobará la corrección]
```

### Ejemplo de ficha resuelta

#### Hallazgo H-02 — Ausencia de autenticación multifactor en administración

- **Activo:** `admin.novacommerce.example` (ficticio).
- **Descripción:** el supuesto del caso plantea que no se exige MFA para cuentas con funciones administrativas.
- **Evidencia:** inventario ficticio de controles de autenticación; **no validado en un sistema real**.
- **Estado de validación:** simulado.
- **Severidad:** alta, **clasificación académica ilustrativa**; requiere análisis contextual para una evaluación real.
- **Impacto potencial en CID:** confidencialidad e integridad.
- **Consecuencia para el negocio:** una cuenta comprometida podría facilitar operaciones administrativas indebidas.
- **Recomendación:** incorporar MFA robusto para cuentas privilegiadas, revisar accesos y vigilar eventos anómalos.
- **Responsable sugerido:** gestión de identidad y equipo de TI.
- **Prioridad:** alta; iniciar la atención en el corto plazo.
- **Criterio de cierre:** comprobar con cuentas de prueba autorizadas que las funciones administrativas exigen el segundo factor previsto.

## Preguntas de reflexión

1. ¿Por qué una puntuación CVSS alta no equivale automáticamente a un riesgo de negocio alto?
2. ¿Qué diferencia existe entre **encontrar un indicio**, **confirmar una vulnerabilidad** y **demostrar un impacto**?
3. Si hay varios hallazgos medios y uno crítico, ¿qué información adicional necesitas para priorizarlos?
4. ¿Por qué una dirección general necesita conocer **responsables y plazos**, además de las debilidades técnicas?
5. ¿Qué cambiaría en tu presentación si un hallazgo aún no ha sido validado?
6. ¿Cómo comunicarías a un directivo que no hubo pruebas de denegación de servicio y, por tanto, no se puede asegurar la resistencia de la plataforma ante ellas?

### Orientaciones para el instructor

- Valorar **razonamiento y trazabilidad**, no solo el uso de términos especializados.
- No aceptar afirmaciones de compromisos reales sustentadas únicamente en datos de este caso.
- Pedir a los participantes que justifiquen cualquier cambio en cantidad, severidad o prioridad.
- Promover lenguaje comprensible para una audiencia no técnica.
- Si se utilizan resultados de laboratorios previos, exigir anonimización y autorización antes de compartir capturas o registros en un repositorio público.

## Rúbrica de evaluación

| Criterio | Ponderación | Evidencia de logro |
|---|---:|---|
| Exactitud y trazabilidad | 30 % | Datos coherentes, referencias a hallazgos y límites de validación claros. |
| Interpretación de riesgos | 20 % | Explica impacto potencial y distingue severidad técnica de riesgo empresarial. |
| Recomendaciones y remediación | 20 % | Acciones viables, prioridades, responsables y criterios de cierre. |
| Comunicación ejecutiva | 20 % | Mensajes claros, concisos, apropiados para la dirección. |
| Integridad de la entrega | 10 % | Cumple estructura, responde preguntas y reconoce supuestos. |
| **Total** | **100 %** | |

**Escala sugerida:** 90–100 excelente; 80–89 satisfactorio; 70–79 básico; menos de 70 requiere reforzamiento. Es una propuesta didáctica, no un criterio oficial de Certiprof.

## Lista de verificación antes de publicar

- [ ] El contenido identifica claramente el caso como **simulado**.
- [ ] La organización y los activos son ficticios.
- [ ] El alcance y las restricciones están definidos.
- [ ] Las cifras de severidad suman ocho y los porcentajes suman 100 %.
- [ ] Se distingue entre severidad técnica y riesgo empresarial.
- [ ] Ningún hallazgo se presenta como explotación real sin evidencia.
- [ ] Las recomendaciones corresponden a los hallazgos.
- [ ] El plan de remediación indica responsables, plazos y verificación.
- [ ] Se evita publicar credenciales, datos personales, direcciones reales o evidencias sensibles.
- [ ] La actividad se entiende sin anexos ni descargas.

## Conclusiones

El valor de un pentesting no está únicamente en descubrir debilidades, sino en **documentarlas con rigor y comunicarlas para que la organización pueda tomar decisiones**. Una presentación ejecutiva debe responder cinco preguntas: **qué se evaluó, qué se observó, por qué importa, qué debe hacerse y cómo se comprobará que el riesgo se redujo**.

Esta actividad complementa las prácticas anteriores de CEHPC y puede reutilizarse como parte de una secuencia de aprendizaje mayor. Para ejercicios futuros, sustituye los datos ficticios por hallazgos obtenidos en ambientes autorizados, manteniendo la trazabilidad y protegiendo la información sensible.

## Referencias de consulta opcional

El README es autosuficiente; los siguientes recursos solo sirven para profundizar:

- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [PTES — Penetration Testing Execution Standard](http://www.pentest-standard.org/)
- [MITRE CAPEC](https://capec.mitre.org/)
- [FIRST — Common Vulnerability Scoring System](https://www.first.org/cvss/)
- [NIST — National Vulnerability Database](https://nvd.nist.gov/)

---

**Nota académica:** actividad original de aprendizaje elaborada a partir del enfoque de presentación de resultados del material CEHPC aportado. No representa una auditoría real ni una plantilla oficial de certificación.
