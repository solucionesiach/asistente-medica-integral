# 📚 Base de Conocimiento — Centro Médico DoctorIA

*Última actualización: Octubre 2026*  
*Versión del documento: 3.0 (Nivel Producción)*  

Este documento constituye la fuente central de información utilizada por el Agente de IA (**Sofía**) para la atención de consultas, cualificación de turnos y gestión de urgencias.

---

## 1. Información Institucional

* **Nombre de la Institución:** Centro Médico DoctorIA
* **Dirección:** Av. Calixto Calderón, Chivilcoy, Provincia de Buenos Aires, Argentina
* **Horarios de Atención:**
  * Lunes a Viernes: 08:00 a 17:00 hs.
  * Sábados: 08:00 a 12:00 hs.
  * Domingos y Feriados: Cerrado.

---

## 2. Especialidades y Aranceles Particulares

* **Medicina General / Pediatría:** $25.000
* **Traumatología / Dermatología:** $30.000
* **Odontología:** $28.000

---

## 3. Coberturas Médicas y Obras Sociales

* **Prepagas / Obras Sociales con Convenio:** OSDE, Swiss Medical, Galeno y OSECAC.
* **Condición de Cobertura:** Cobertura al 100% (sujeto a plan y presentación de credencial activa / nº de afiliado).
* **Atención Particular:** Disponible para pacientes sin convenio mediante pago de arancel correspondiente.

---

## 4. Requisitos Obligatorios para la Reserva de Turnos

Para efectuar la cualificación activa y completar el agendamiento (en **Google Calendar** y **Google Sheets**), el sistema exige recopilar obligatoriamente los siguientes 5 datos del paciente:

1. **Nombre Completo**
2. **DNI**
3. **Teléfono de Contacto** *(con código de área)*
4. **Obra Social / Prepaga** *(o condición de Particular)*
5. **Motivo Breve de Consulta**
6. **Fecha y Hora Deseada** *(dentro de las franjas de atención)*

---

## 5. Protocolo de Urgencias y Emergencias Médicas

* **Criterio de Activación:** Detección de síntomas críticos o gravedad manifiestos (ej. dolor precordial/de pecho, dificultad respiratoria, sangrado profuso, pérdida de conocimiento, traumatismos graves, fiebre muy alta).
* **Acción Inmediata (Línea de Respuesta):**
  > *"⚠️ ATENCIÓN: Si estás experimentando una emergencia médica, por favor dirígete inmediatamente a la guardia médica más cercana o comunícate con el servicio de emergencias (SAME - 107). Esta línea automática no procesa emergencias de salud."*
* **Acción de Fondo:** Interrupción inmediata del flujo automatizado y disparo de alerta por correo electrónico (**Gmail**) a la secretaría del centro médico.

---

## 6. Fuera de Alcance y Restricciones Operativas

El Agente de IA tiene prohibido de forma estricta:
* Emitir diagnósticos médicos preliminares o definitivos.
* Indicar o recetar medicamentos/tratamientos fármaco-terapéuticos.
* Interpretar estudios clínicos, laboratorio o placas radiográficas.
* Negociar valores de tarifas o excepciones en convenios de obras sociales.
