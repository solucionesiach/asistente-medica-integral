Markdown# 🏥 DoctorIA — Sistema Agente Conversacional e Integración Asíncrona

**DoctorIA** es una solución de atención médica automatizada orientada a optimizar la interacción entre pacientes y el centro médico. Diseñado como un **Agente de IA Autónomo**, reemplaza los esquemas rígidos de respuesta por menúes (IVR) mediante comprensión semántica del lenguaje natural, ingeniería de contexto controlada, cualificación activa de solicitudes y gestión supervisada de urgencias.

---

## 🚀 Capacidades y Valor Operativo

* **Comprensión Semántica y Contexto Controlado:** Interpreta consultas complejas, modismos y múltiples intenciones en lenguaje natural, operando bajo una Base de Conocimiento oficial (tarifas, horarios, coberturas) que evita alucinaciones o respuestas fuera de alcance.
* **Cualificación Activa de Pacientes:** Evalúa y recopila secuencialmente la información requerida (`Nombre Completo`, `DNI`, `Teléfono de Contacto`, `Cobertura/Prepaga`, `Motivo de Consulta`, `Fecha` y `Hora del Turno`) antes de ejecutar cualquier registro o reserva.
* **Protocolo de Urgencias Médicas:** Identifica de forma automática indicadores o palabras clave de severidad clínica. Interrumpe el flujo automático para emitir instrucciones inmediatas de seguridad (SAME - 107) y dispara una alerta por correo electrónico a la secretaría del centro médico.
* **Persistencia de Datos (CRM) y Agendamiento:**
  * Reserva y sincronización directa de eventos en **Google Calendar**.
  * Registro centralizado de pacientes y turnos en **Google Sheets** para auditoría y seguimiento administrativo.
* **Subsistema de Recordatorios Asíncronos:** Flujo automatizado de ejecución diaria que consulta la base de datos, identifica las citas programadas para las 24 horas posteriores y emite notificaciones salientes de recordatorio al contacto del paciente.

---

## 🛠️ Arquitectura Técnica de la Solución

El sistema se encuentra orquestado sobre la plataforma **n8n**, articulando modelos de lenguaje (LLM) con herramientas de procesamiento y persistencia:

### 1. Flujo Conversacional Principal (Atención e Interacción)
```text
[Chat Trigger / Mensajería] 
        ↓
    [AI Agent] ← (Google Gemini + Memory)
        ├── Tool: Google Calendar (Agendamiento)
        ├── Tool: Google Sheets (Persistencia de Turnos)
        └── Tool: Gmail (Alerta Inmediata a Secretaría)
2. Flujo Asíncrono de Recordatorios (Procesamiento Programado)Plaintext[Schedule Trigger (Cron Diario)]
        ↓
[Google Sheets - Consulta de Turnos]
        ↓
[Filter Node (Filtro: Fecha del Turno = Día Posterior)]
        ↓
[WhatsApp Cloud API / Canal de Mensajería (Notificación Saliente)]
📋 Estructura de Persistencia (Base de Datos)Fecha RegistroNombre CompletoDNITeléfonoCobertura/PrepagaMotivo ConsultaFecha del TurnoHora del TurnoYYYY-MM-DDTextoTextoTextoTextoTextoYYYY-MM-DDHH:MM⚙️ Directivas del Sistema (System Message)El comportamiento de la asistente virtual (Sofía) se encuentra enmarcado por reglas operativas rigurosas:Límites de Actuación: Prohibición estricta de emitir diagnósticos médicos, recetar medicamentos o interpretar estudios clínicos.Secuencia de Cualificación: Cumplimiento ordenado de captura de datos indispensables.Derivación de Emergencia: Invocación transparente de herramientas de notificación ante eventos críticos.📂 Repositorio de Entregables/workflows/DoctorIA_n8n_workflow.json: Exportación del flujo estructurado en n8n./docs/Informe_Tecnico_DoctorIA.pdf: Documentación del proyecto (Relevamiento, Base de Conocimiento, Arquitectura y Pruebas).
