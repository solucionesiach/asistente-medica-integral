# Arquitectura de Agente Conversacional Inteligente (MédicaIntegral)
> Trabajo Final Integrador — Diplomatura en IA Aplicada a Entornos Digitales de Gestión (FCE-UBA · Cohorte 2026)

## 📌 Descripción del Proyecto
Este proyecto presenta la arquitectura y diseño de un asistente conversacional basado en Inteligencia Artificial Generativa para la gestión de consultas iniciales, cualificación de pacientes y asistencia en la reserva de turnos en el **Centro Médico MédicaIntegral**.

El objetivo es reemplazar los sistemas tradicionales de respuesta automática basados en árboles de decisión rígidos por un agente capaz de comprender lenguaje coloquial, operar dentro de una base de conocimiento delimitada y derivar casos urgentes de forma supervisada.

---

## 🛠️ Estructura del Repositorio
* `README.md`: Descripción general del proyecto e instrucciones.
* `knowledge_base.md`: Base de conocimiento estructurada (tarifas, horarios, especialidades y políticas).
* `system_prompt.txt`: Instrucciones maestras, flujo de cualificación activa y reglas del agente.

---

## 🚀 Herramientas Utilizadas
* **Motor de IA / LLM:** Google AI Studio / Gemini / ChatGPT.
* **Gestión de Conocimiento:** Markdown estructurado (RAG / Context Window).
* **Repositorio y Control de Versiones:** GitHub.

---

## 📋 Funcionalidades Clave
1. **Comprensión semántica:** Procesa lenguaje coloquial y consultas complejas.
2. **Contexto controlado:** Responde únicamente con información verificada para evitar alucinaciones.
3. **Cualificación activa:** Recopila datos obligatorios (Nombre, DNI, Cobertura, Motivo) antes de direccionar a la reserva de turnos.
4. **Trigger de seguridad (Urgencias):** Detecta síntomas graves y deriva inmediatamente a la guardia médica o emergencias (SAME 107).
