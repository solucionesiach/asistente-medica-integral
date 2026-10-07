# 🏥 DoctorIA - Agente Conversacional e Integración Asíncrona (Nivel 3)

**DoctorIA** es una solución avanzada de atención médica automatizada que reemplaza los tradicionales IVR y sistemas de árbol de decisión rígidos por un **Agente de IA Autónomo**. El sistema posee comprensión semántica de lenguaje natural, memoria conversacional, cualificación activa de turnos, gestión inmediata de urgencias y un subsistema de recordatorios asíncronos[cite: 6, 7].

---

## 🚀 Características Principales

* **Comprensión Semántica y Contexto Controlado:** Procesa expresiones coloquiales, modismos y consultas complejas manteniendo respuestas precisas basadas en una Base de Conocimiento oficial (tarifas, horarios, coberturas).
* **Cualificación Activa de Pacientes:** Filtra y solicita datos obligatorios (`Nombre Completo`, `DNI`, `Teléfono`, `Cobertura/Prepaga`, `Motivo de Consulta`, `Fecha` y `Hora del Turno`) antes de efectuar cualquier reserva o registro.
* **Protocolo de Urgencias Médicas:** Identificación automática de situaciones críticas (dolores agudos, sangrado, etc.). Interrumpe la atención automatizada, brinda instrucciones inmediatas de seguridad (SAME 107) y dispara una alerta por **Gmail** en tiempo real a la secretaría del centro médico.
* **Persistencia de Datos (CRM) y Agendamiento:**
  * Sincronización automática de citas en **Google Calendar**[cite: 7].
  * Registro centralizado e histórico de leads/pacientes en **Google Sheets**[cite: 7].
* **Subsistema de Recordatorios Asíncronos (Cron 24hs):** Automatización diaria que consulta la base de datos, filtra las citas del día posterior y dispara notificaciones salientes de recordatorio al canal de mensajería del paciente[cite: 6, 7].

---

## 🛠️ Arquitectura Técnica del Sistema

El proyecto está construido sobre **n8n** conectando modelos de LLM con herramientas externas (*Tools*)[cite: 7]:

### 1. Flujo Conversacional Principal (Atención en Tiempo Real)
```text
[Chat Trigger / Mensajería] 
        ↓
    [AI Agent] ← (Google Gemini + Simple Memory)
        ├── Tool: Google Calendar (Agendamiento)
        ├── Tool: Google Sheets (Persistencia CRM)
        └── Tool: Gmail (Alerta Urgencias a Secretaría)
