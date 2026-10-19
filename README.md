# 🏥 DoctorIA — Sistema Agente Conversacional e Integración Asíncrona

**DoctorIA** es una solución de atención médica automatizada orientada a optimizar la interacción entre pacientes y el centro médico. Diseñado como un **Agente de IA Autónomo**, reemplaza los esquemas rígidos de respuesta por menúes (IVR) mediante comprensión semántica del lenguaje natural, ingeniería de contexto controlada, cualificación activa de solicitudes y gestión supervisada de urgencias.

---

## 🚀 Capacidades y Valor Operativo

* **Comprensión Semántica y Contexto Controlado:** Interpreta consultas complejas, modismos y múltiples intenciones en lenguaje natural, operando bajo una Base de Conocimiento oficial (tarifas, horarios, coberturas) que evita alucinaciones o respuestas fuera de alcance.
* **Cualificación Activa de Pacientes:** Evalúa y recopila secuencialmente la información requerida (`Nombre Completo`, `DNI`, `Teléfono de Contacto`, `Cobertura/Prepaga`, `Motivo de Consulta`, `Fecha` y `Hora del Turno`) antes de ejecutar cualquier registro o reserva.
* **Protocolo de Urgencias Médicas:** Identifica de forma automática indicadores o palabras clave de severidad clínica. Interrumpe el flujo automático para emitir instrucciones inmediatas de seguridad (SAME - 107) y dispara una alerta por correo electrónico a la secretaría del centro médico.
* **Persistencia de Datos (CRM) y Agendamiento:**
  * Reserva y sincronización directa de eventos en **Google Calendar**.
  * Registro centralizado de pacientes y turnos en **Google Sheets** (hojas `turnos` y `base de datos`) para auditoría y seguimiento administrativo.
* **Subsistema de Recordatorios Asíncronos:** Flujo automatizado de ejecución diaria que consulta la base de datos, identifica las citas programadas para las 24 horas posteriores y emite notificaciones salientes de recordatorio al contacto del paciente.

---

## 🛠️ Arquitectura Técnica de la Solución

El sistema se encuentra orquestado sobre la plataforma **n8n**, articulando modelos de lenguaje (LLM) con herramientas de procesamiento y persistencia:

### 1. Flujo Conversacional Principal (Atención e Interacción)

- **[Chat Trigger / Mensajería]**
  - └── **[AI Agent]** (Google Gemini + Simple Memory)
      - ├── **Tool:** Google Calendar (Agendamiento)
      - ├── **Tool:** `registrar_turno` (Google Sheets — Hoja "turnos")
      - ├── **Tool:** `guardar_paciente` (Google Sheets — Hoja "base de datos")
      - └── **Tool:** Gmail (Alerta Inmediata a Secretaría)

### 2. Flujo Asíncrono de Recordatorios (Procesamiento Programado)

- **[Schedule Trigger (Cron Diario 09:00 hs)]**
  - └── **[Google Sheets — Consulta de Turnos]**
      - └── **[Filter Node (Filtro: Fecha del Turno = Día Posterior)]**
          - └── **[WhatsApp Cloud API / Canal de Mensajería (Notificación Saliente)]**

---

## 🔄 Historial de Versiones y Desarrollo Iterativo

El desarrollo de la arquitectura avanzó mediante un proceso continuo de pruebas, diagnóstico y refinamiento técnico:

* **v1.0 — Prototipo Conversacional Base:** Configuración del activador de mensajería (`Chat Trigger`), el agente de IA (`AI Agent`) y Google Gemini.
* **v2.0 — Memoria y Corrección de Herramienta CRM (`guardar_paciente`):** Integración de `Simple Memory`. Corrección del mapeo del DNI (`$fromAI`) en la herramienta CRM y reestructuración para actualizar filas existentes por DNI sin duplicar pacientes.
* **v3.0 — Protocolo de Emergencias (Gmail):** Incorporación del nodo de Gmail para el envío de alertas automáticas a la secretaría ante la detección de palabras clave de gravedad clínica.
* **v4.0 — Sincronización de Agenda y Nueva Herramienta `registrar_turno`:** Incorporación de la herramienta específica para escribir filas en la pestaña *"turnos"* (`Fecha registro`, `Nombre completo`, `DNI`, `Cobertura/Prepaga`, `Teléfono`, `Motivo de consulta`, `Fecha del turno` y `Hora del turno`).
* **v5.0 — Directivas de Ejecución Secuencial para el LLM:** Restructuración de las instrucciones del agente para imponer un orden estrictamente secuencial (1. Google Calendar ➔ 2. `registrar_turno` ➔ 3. `guardar_paciente`), evitando errores de ejecución en paralelo producidos por Google Gemini.
* **v6.0 — Estado de Validación y Trabajo Futuro:** Mantenimiento del flujo en entorno borrador/simulado. Se contemplan como ajustes para paso a producción la normalización de variables entre la planilla y el nodo de WhatsApp (mayúsculas/minúsculas en nombres de columnas) y la autenticación de credenciales de salida.

---

## 📋 Estructura de Persistencia (Base de Datos en Google Sheets)

### Hoja 1: `turnos`
| Fecha registro | Nombre completo | DNI | Cobertura/Prepaga | Teléfono | Motivo de consulta | Fecha del turno | Hora del turno |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| *YYYY-MM-DD* | *Texto* | *Texto* | *Texto* | *Texto* | *Texto* | *YYYY-MM-DD* | *HH:mm* |

### Hoja 2: `base de datos`
| Nombre completo | DNI | Teléfono | Cobertura/Prepaga |
| :--- | :--- | :--- | :--- |
| *Texto* | *Texto* | *Texto* | *Texto* |

---

## ⚙️ Directivas del Sistema (System Message)

El comportamiento de la asistente virtual (**Sofía**) se encuentra enmarcado por reglas operativas rigurosas:
1. **Límites de Actuación:** Prohibición estricta de emitir diagnósticos médicos, recetar medicamentos o interpretar estudios clínicos.
2. **Secuencia de Cualificación:** Cumplimiento ordenado de captura de datos indispensables.
3. **Orden Secuencial de Herramientas:** Ejecución individual de Calendar, `registrar_turno` y `guardar_paciente` previo a emitir la confirmación final al paciente.
4. **Derivación de Emergencia:** Invocación transparente de herramientas de notificación (Gmail) ante eventos críticos.

---

## 📂 Archivos del Repositorio

* `README.md`: Presentación oficial, arquitectura técnica e historial de versiones.
* `knowledge_base.md`: Base de conocimiento institucional en Markdown (tarifas, horarios y políticas).
* `system_prompt.txt`: Prompt maestro con instrucciones operativas, secuencia de cualificación y ejecución de herramientas.
* `DoctorIA_n8n_workflow.json`: Archivo JSON exportado directamente desde n8n con el flujo completo de automatización.
