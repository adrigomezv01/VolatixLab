\# Project Guidelines — VolatixLab



Este documento define las normas internas del proyecto VolatixLab.

Su objetivo es garantizar coherencia, claridad y mantenibilidad a medida que el laboratorio crece.



Estas normas aplican a escenarios, documentación, evidencias, scripts y commits.



---



\## 🧭 Principios del proyecto



VolatixLab se rige por los siguientes principios:



\- Claridad antes que complejidad

\- Comprensión antes que automatización

\- Realismo antes que espectacularidad

\- Documentación antes que código

\- Proceso antes que resultado



---



\## 📁 Convención de nombres



\### Directorios

\- Nombres en minúsculas

\- Separados por guiones (`-`)

\- Sin espacios

\- Prefijo numérico cuando aplique orden



Ejemplos:

\- `scenario-01-initial-access`

\- `scenario-02-persistence`



---



\### Archivos

\- Markdown en inglés técnico estándar (`README.md`, `ANALYSIS.md`)

\- Nombres descriptivos y claros

\- Mayúsculas solo para archivos principales



---



\## 🧱 Estructura estándar de un escenario



Cada escenario debe seguir esta estructura base:



scenario-XX-nombre/

│

├── README.md # Contexto y objetivos

├── attack/ # Descripción del ataque

├── evidence/ # Evidencias forenses

├── analysis/ # Proceso de análisis

├── detection/ # Detección y conclusiones

└── notes.md # Observaciones finales





Esta estructura es obligatoria para todos los escenarios.



---



\## 🧪 Reglas sobre evidencias



\- Las evidencias no se modifican nunca

\- Deben documentarse claramente:

&nbsp; - origen

&nbsp; - tipo

&nbsp; - fecha aproximada

\- Los archivos grandes deben justificarse

\- Nunca subir evidencias innecesarias



Si una evidencia no aporta aprendizaje, no se incluye.



---



\## 📚 Documentación



\- Toda acción debe estar explicada

\- No se asume conocimiento previo

\- Cada comando debe tener contexto

\- Se debe explicar el \*por qué\*, no solo el \*cómo\*



---



\## 🛠️ Scripts y utilidades



\- Scripts solo si aportan valor real

\- Siempre documentados

\- Nunca scripts “mágicos”

\- Prioridad a comprensión frente a automatización



---



\## 🧾 Commits



Reglas para commits:



\- Mensajes claros y concisos

\- Un propósito por commit

\- Evitar commits genéricos tipo “update”

\- Commits pequeños y coherentes



Ejemplo correcto:

Add base structure for scenario 01





---



\## 🚫 Qué evitar



\- Mezclar teoría con análisis

\- Automatizar sin explicar

\- Escenarios incompletos

\- Documentación ambigua

\- Evidencias sin contexto



---



\## 📌 Nota final



Estas normas pueden evolucionar con el proyecto, pero cualquier cambio debe ser consciente y documentado.



El objetivo no es la rigidez, sino la coherencia.





