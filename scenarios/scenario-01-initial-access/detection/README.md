\# Escenario 1 — Detección Blue Team  

\## Initial Access por ejecución de binario



---



\## 1. Objetivo de detección



El objetivo de esta detección es identificar la ejecución de binarios no habituales en sistemas Windows, lanzados de forma interactiva por el usuario desde el entorno gráfico, como posible indicador de un evento de acceso inicial.

La detección se centra en actividades que, aun siendo breves y sin persistencia, pueden representar el inicio de un compromiso del sistema y que normalmente pasan desapercibidas en análisis basados únicamente en procesos activos.




---



\## 2. Resumen del comportamiento observado



El incidente analizado corresponde a un evento de acceso inicial en el que un usuario ejecutó manualmente un binario desde el entorno gráfico del sistema Windows. El proceso fue lanzado por `explorer.exe`, indicando interacción directa del usuario, y tuvo una duración breve, finalizando poco después de su ejecución.

El binario ejecutado no formaba parte del software habitual del sistema y no se encontraba ubicado en rutas estándar del sistema operativo. No se identificaron mecanismos de persistencia ni ejecución posterior, lo que sugiere una prueba inicial o una fase temprana del ataque.




---



\## 3. Fuentes de logs relevantes



Para la detección de este comportamiento, resultan especialmente relevantes aquellas fuentes de logs que registran la creación de procesos y la ejecución de binarios en sistemas Windows.

Las principales fuentes de información que permitirían detectar este tipo de actividad son:

- **Registro de seguridad de Windows (Security Log)**: proporciona eventos relacionados con la creación de procesos cuando la auditoría correspondiente está habilitada.
- **Sysmon**: en caso de estar desplegado, ofrece visibilidad detallada sobre la creación de procesos, incluyendo información adicional como rutas completas y relaciones padre-hijo.
- **Microsoft Defender**: puede generar alertas o registros asociados a la ejecución de archivos potencialmente sospechosos, incluso cuando no se detecta malware conocido.




---



\## 4. Eventos clave de Windows



La ejecución del binario sospechoso habría dejado rastro en eventos relacionados con la creación de procesos en el sistema operativo Windows.

Los eventos más relevantes para este escenario son los siguientes:

- **Event ID 4688 (Windows Security Log)**: registra la creación de un nuevo proceso cuando la auditoría de creación de procesos está habilitada. Este evento incluye información como el nombre del proceso creado y el proceso padre.
- **Sysmon Event ID 1 (Process Create)**: en entornos donde Sysmon está desplegado, este evento proporciona detalles adicionales sobre la creación del proceso, incluyendo la ruta completa del ejecutable y la relación padre-hijo.

Estos eventos permitirían identificar la ejecución de un binario no habitual lanzado desde `explorer.exe`, incluso si el proceso tuvo una duración breve.




---



\## 5. Estrategia de detección



La estrategia de detección para este escenario se basa en la identificación de procesos creados de forma interactiva por el usuario que no correspondan a software habitual del sistema.

Una posible aproximación consiste en monitorizar eventos de creación de procesos y filtrar aquellos casos en los que el proceso padre sea `explorer.exe` y el ejecutable se encuentre ubicado en rutas de usuario o presente un nombre no reconocido. Este tipo de comportamiento, especialmente cuando la ejecución es breve y no va acompañada de persistencia, puede indicar una fase temprana de acceso inicial.

La correlación de estos factores permite generar alertas más precisas, reduciendo falsos positivos asociados a procesos legítimos del sistema operativo.




---



\## 6. Ejemplo de regla de detección



A continuación se muestra un ejemplo conceptual de cómo podría expresarse esta detección utilizando una lógica similar a una regla Sigma:

```yaml
title: Ejecución interactiva de binario no habitual
logsource:
  product: windows
  category: process_creation
detection:
  selection:
    ParentImage|endswith: '\explorer.exe'
    Image|contains:
      - '\Users\'
  condition: selection

Esta regla busca identificar procesos creados desde el entorno gráfico del usuario cuyo ejecutable se encuentra en rutas de usuario, lo que puede indicar la ejecución de binarios no habituales como parte de un acceso inicial.



---



\## 7. Limitaciones y evasión



La detección propuesta presenta varias limitaciones inherentes al uso de registros de creación de procesos. En primer lugar, depende de que la auditoría de procesos o Sysmon estén correctamente habilitados en el sistema. En entornos donde estos mecanismos no están desplegados, la visibilidad sería limitada.

Además, un atacante podría evadir esta detección utilizando nombres de binarios que imiten software legítimo, ejecutando el archivo desde rutas menos sospechosas o lanzándolo desde procesos distintos a `explorer.exe`, como scripts o servicios.

Por último, ejecuciones extremadamente breves o técnicas de living-off-the-land podrían reducir la efectividad de esta detección, lo que refuerza la necesidad de combinar múltiples fuentes de telemetría en entornos de producción.




