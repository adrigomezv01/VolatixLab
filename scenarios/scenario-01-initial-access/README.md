\# Escenario 01 — Acceso inicial en sistema Windows



---



\## 🧪 Descripción general



En este escenario se investiga un posible \*\*incidente de seguridad en un sistema Windows\*\* tras detectarse un comportamiento anómalo por parte del usuario.



El objetivo es analizar las evidencias disponibles y determinar si el sistema ha sido comprometido, cómo se produjo el acceso inicial y cuál es el impacto del incidente.



El rol del lector es el de \*\*analista forense\*\*, encargado de investigar el caso desde cero.



---



\## 🕵️ Contexto del incidente



Un usuario reporta que su equipo Windows presenta un comportamiento extraño tras ejecutar un archivo descargado de Internet.



Desde ese momento, el sistema muestra signos de actividad sospechosa, lo que motiva la apertura de un incidente de seguridad y la recopilación de evidencias para su análisis.



No se dispone de información adicional sobre el origen exacto del archivo ni sobre el alcance del posible compromiso.



---



\## 🎯 Objetivos de aprendizaje



Al completar este escenario, el lector será capaz de:



\- Comprender el flujo básico de una investigación DFIR

\- Identificar procesos sospechosos en memoria

\- Analizar artefactos básicos de ejecución en Windows

\- Razonar y documentar hallazgos forenses

\- Extraer conclusiones a partir de evidencias reales



---



\## 🔍 Alcance del escenario



Este escenario se centra en:



\- Análisis forense básico de memoria

\- Identificación de actividad sospechosa

\- Comprensión del acceso inicial



Quedan fuera del alcance:



\- Análisis avanzado de malware

\- Ingeniería inversa

\- Respuesta activa al incidente



---



\## 📂 Evidencias disponibles




Las evidencias utilizadas en este escenario no se incluyen directamente en el repositorio debido a su tamaño.

El volcado de memoria RAM puede descargarse desde la sección **Releases** del proyecto:

- **Scenario 01 – Initial Access – Evidence**

El paquete incluye:
- Volcado de memoria RAM (Windows 10)
- Archivo de hashes SHA256 para verificación de integridad

Antes de comenzar el análisis, se recomienda verificar la integridad del archivo descargado.




---



\## 🧭 Cómo abordar el escenario



Se recomienda seguir una metodología estructurada:



1\. Comprender el contexto del incidente

2\. Identificar qué evidencias están disponibles

3\. Analizar primero la memoria del sistema

4\. Documentar cada hallazgo de forma clara

5\. Extraer conclusiones basadas en evidencias



No se trata de encontrar respuestas rápidas, sino de \*\*entender el proceso de investigación\*\*.



---



\## ⚠️ Notas importantes



\- No modifiques las evidencias originales

\- Sigue el escenario en el orden propuesto

\- Documenta tus razonamientos, no solo los resultados

\- Prioriza la comprensión frente a la rapidez



