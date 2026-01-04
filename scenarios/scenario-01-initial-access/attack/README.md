\# Ataque — Escenario 01



Este documento describe el ataque utilizado en el Escenario 01 — Acceso inicial en sistema Windows.



El ataque está diseñado con fines \*\*educativos y controlados\*\*, con el objetivo de generar evidencias claras para su posterior análisis forense.



---



\## 🎯 Objetivo del ataque



Simular un acceso inicial sencillo mediante la \*\*ejecución manual de un binario malicioso por parte del usuario\*\*.



El objetivo no es causar daño al sistema, sino generar huellas claras y reproducibles para aprender el proceso de investigación DFIR.



---



\## 🧪 Tipo de ataque



\- Vector: ejecución de archivo descargado

\- Sistema objetivo: Windows

\- Privilegios: usuario estándar

\- Complejidad: baja

\- Persistencia: no implementada



Este tipo de ataque es frecuente en incidentes reales de acceso inicial.



---



\## 🧩 Descripción del ataque



El ataque sigue el siguiente flujo general:



1\. El usuario descarga un archivo ejecutable desde Internet

2\. El usuario ejecuta manualmente el archivo

3\. El binario se lanza como un nuevo proceso

4\. El proceso realiza acciones básicas y deja rastros en el sistema

5\. El sistema permanece operativo tras la ejecución



No se utilizan técnicas de evasión ni mecanismos avanzados.



---



\## 🧠 Huellas esperadas



Como resultado de la ejecución del binario, se esperan las siguientes huellas:



\- Nuevo proceso visible en memoria

\- Proceso padre asociado a `explorer.exe`

\- Binario presente en disco

\- Archivos temporales o artefactos simples



Estas huellas servirán como base para el análisis forense posterior.



---



\## 🚫 Acciones no realizadas



De forma intencionada, este ataque \*\*no incluye\*\*:



\- Persistencia avanzada

\- Comunicación con servidores externos

\- Ofuscación o empaquetado

\- Técnicas de evasión



Estas técnicas se abordarán en escenarios posteriores.



---



\## ⚠️ Nota importante



Este ataque debe ejecutarse únicamente en entornos controlados y con fines educativos.



