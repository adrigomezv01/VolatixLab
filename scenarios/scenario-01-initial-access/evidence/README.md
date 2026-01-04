\# Evidencias — Escenario 01



Este directorio contiene las evidencias forenses asociadas al Escenario 01 — Acceso inicial en sistema Windows.



Las evidencias deben considerarse \*\*inmutables\*\* y utilizarse únicamente para análisis forense.



---



\## 🧪 memory/



Contiene el volcado de memoria RAM del sistema afectado.



Esta evidencia permite analizar:

\- Procesos en ejecución

\- Comandos lanzados

\- Actividad sospechosa en memoria

\- Posible malware activo en el momento de la captura



La memoria representa el estado del sistema \*\*durante el incidente\*\*.



---



\## 💽 disk/



Contiene artefactos relevantes extraídos del disco del sistema.



Incluye únicamente información necesaria para el escenario, como:

\- Binarios ejecutados

\- Archivos creados o modificados

\- Posibles mecanismos básicos de persistencia



No se proporciona una imagen completa del disco para mantener el escenario ligero y enfocado.



La información de disco representa \*\*qué quedó tras el incidente\*\*.



---



\## 📜 context/



Contiene información contextual del incidente, como:

\- Datos básicos del sistema

\- Usuario afectado

\- Hora aproximada del incidente

\- Notas iniciales del caso



Esta información es clave para interpretar correctamente las evidencias técnicas.



---



\## ⚠️ Nota importante



Las evidencias no deben modificarse bajo ninguna circunstancia.



Cualquier análisis debe realizarse sobre copias o de forma no destructiva.



