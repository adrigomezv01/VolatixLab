\# Escenario 1 — Análisis Forense de Memoria  

\## Initial Access mediante ejecución de binario



---



\## 1. Descripción del escenario



Este escenario simula un caso de acceso inicial en un sistema Windows 10 mediante la ejecución manual de un binario por parte del usuario. El objetivo del laboratorio es analizar una captura de memoria obtenida tras la ejecución del archivo sospechoso, con el fin de identificar evidencias de ejecución, comportamiento del proceso y artefactos relevantes en memoria.

El análisis se centra exclusivamente en técnicas de análisis forense de memoria (DFIR), utilizando herramientas estándar del sector, y está diseñado como un ejercicio práctico y reproducible para el aprendizaje de respuesta ante incidentes.




---



\## 2. Evidencia analizada



La evidencia analizada consiste en un volcado de memoria RAM completo del sistema afectado, obtenido tras la ejecución del binario sospechoso como parte del escenario simulado.

La adquisición de la memoria se realizó utilizando la herramienta DumpIt, ejecutada directamente en el sistema Windows 10 afectado. El sistema fue apagado posteriormente y la evidencia fue trasladada al entorno de análisis para su estudio.

Para garantizar la integridad de la evidencia, se calculó el hash criptográfico SHA256 del archivo de volcado antes de iniciar el análisis forense.

- Archivo de evidencia: `DESKTOP-O13V67M-20260104-234637.dmp`
- Algoritmo de hash: SHA256
- Hash: `61D3D21F052D5799E598B6DD0F5BF14228A1A710733EA31CDAC0383B00BF8325`



---



\## 3. Entorno de análisis



El análisis forense se realizó en un sistema independiente al equipo afectado, utilizando un entorno de trabajo dedicado para análisis DFIR.

- Sistema operativo del analista: Windows 11
- Herramientas utilizadas:
  - Volatility Framework 3 (versión 2.28.0)
  - DumpIt (adquisición de memoria)
  - Sysinternals Strings (extracción de cadenas de texto)
- Consola utilizada: Windows PowerShell

El análisis se llevó a cabo sobre una copia de la evidencia, manteniendo la integridad del archivo original durante todo el proceso.




---



\## 4. Identificación del sistema analizado



La identificación del sistema analizado se realizó a partir de la información extraída directamente del volcado de memoria mediante el plugin `windows.info` de Volatility 3.

Los datos obtenidos indican que el sistema afectado corresponde a un equipo con las siguientes características:

- Sistema operativo: Windows 10
- Versión: 10.0.19041
- Arquitectura: 64 bits
- Tipo de sistema: Estación de trabajo (NtProductWinNt)

Esta información permite contextualizar el análisis y confirmar la compatibilidad del sistema con las técnicas forenses aplicadas durante el escenario.




---



\## 5. Análisis de procesos



En primer lugar, se realizó un listado de los procesos activos en el momento de la captura de memoria mediante el plugin `windows.pslist` de Volatility 3.

En los resultados obtenidos no se identificó ningún proceso correspondiente al binario `invoice_viewer.exe`. Este comportamiento es coherente con el diseño del escenario, ya que el proceso sospechoso tuvo una ejecución de corta duración y había finalizado antes de que se completara la adquisición de memoria.




Dado que el binario sospechoso no aparecía como proceso activo, se procedió a realizar un escaneo de procesos finalizados en memoria mediante el plugin `windows.psscan`.

Este análisis permitió identificar la ejecución del proceso `invoice_viewer.exe`, el cual había finalizado antes de la captura de memoria. Los datos relevantes obtenidos son los siguientes:

- Nombre del proceso: `invoice_viewer.exe`
- PID: 4412
- PPID: 4180
- Hora de inicio: 2026-01-04 23:46:33 UTC
- Hora de finalización: 2026-01-04 23:46:49 UTC

La presencia del proceso en los resultados de `psscan` confirma que el binario fue ejecutado en el sistema, a pesar de no encontrarse activo en el momento de la adquisición de memoria.




El análisis de la relación padre-hijo se realizó correlacionando la información obtenida mediante `windows.psscan` y `windows.pstree`.

El proceso `invoice_viewer.exe` presentaba como proceso padre el identificador PPID 4180, el cual corresponde al proceso `explorer.exe`. Este hecho indica que el binario fue ejecutado directamente desde el entorno gráfico del usuario, lo que es coherente con una ejecución manual del archivo.

Aunque el proceso `invoice_viewer.exe` ya no se encontraba activo en el momento del análisis, la correlación entre el PPID y el árbol de procesos permite atribuir su ejecución a una acción iniciada por el usuario.




---



\## 6. Análisis de comportamiento en memoria



Con el objetivo de identificar artefactos adicionales asociados a la ejecución del binario sospechoso, se realizó un análisis de cadenas de texto presentes en el volcado de memoria.

Para ello, se extrajeron los strings del archivo de memoria y se revisaron en busca de referencias relacionadas con el binario analizado. Durante este proceso se identificó el siguiente artefacto relevante:

- `INVOICE_VIEWER.EXE-85A65062.pf`

La presencia de este archivo de tipo Prefetch en memoria constituye una evidencia adicional de ejecución, ya que los archivos `.pf` son generados por el sistema operativo Windows cuando un ejecutable es lanzado, con el objetivo de optimizar su carga.

Este hallazgo refuerza la conclusión de que el binario `invoice_viewer.exe` fue ejecutado en el sistema analizado, complementando la información obtenida previamente mediante el análisis de procesos.




---



\## 7. Línea temporal del incidente



A partir de la información extraída del volcado de memoria, se pudo reconstruir una línea temporal aproximada de los eventos asociados al incidente simulado.

- **2026-01-04 23:46:33 UTC**: Inicio de la ejecución del proceso `invoice_viewer.exe`, identificado mediante el plugin `windows.psscan`.
- **2026-01-04 23:46:49 UTC**: Finalización del proceso `invoice_viewer.exe`.
- **2026-01-04 23:46:37 UTC**: Ejecución de la herramienta DumpIt para la adquisición de memoria del sistema.

La secuencia temporal indica que el binario sospechoso fue ejecutado y finalizó su ejecución antes de que se completara la captura de memoria, lo que explica su ausencia como proceso activo en el análisis inicial.



---



\## 8. Conclusiones del análisis



El análisis forense de la memoria del sistema permitió confirmar la ejecución del binario `invoice_viewer.exe` como parte del escenario de acceso inicial simulado.

Aunque el proceso no se encontraba activo en el momento de la captura de memoria, su ejecución fue identificada mediante el análisis de procesos finalizados (`windows.psscan`), así como por la presencia de artefactos asociados en memoria, incluyendo un archivo Prefetch relacionado con el ejecutable.

La correlación de los identificadores de proceso y la relación padre-hijo indicó que la ejecución del binario fue iniciada desde el entorno gráfico del usuario, lo que es coherente con una ejecución manual del archivo. No se identificaron evidencias de persistencia ni de actividad posterior a la finalización del proceso.

En conjunto, las evidencias obtenidas permiten concluir que el incidente corresponde a un evento de acceso inicial basado en la ejecución directa de un binario por parte del usuario.




---



\## 9. Lecciones aprendidas



Este escenario pone de manifiesto la importancia del análisis forense de memoria para la identificación de actividades que no dejan procesos activos en el sistema. La ausencia del binario sospechoso en los listados de procesos activos demuestra que un análisis superficial puede resultar insuficiente para detectar eventos relevantes.

El uso de técnicas como el escaneo de procesos finalizados y la identificación de artefactos en memoria permite reconstruir con precisión la ejecución de un binario, incluso cuando su duración es limitada. Asimismo, el escenario ilustra la necesidad de correlacionar múltiples fuentes de información forense para obtener conclusiones fiables.

Como laboratorio práctico, este escenario permite al analista familiarizarse con flujos reales de trabajo DFIR, comprender las limitaciones de cada técnica y desarrollar un enfoque analítico basado en evidencias.




