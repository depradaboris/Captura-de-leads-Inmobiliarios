## **📋 Informe Técnico: Automatización de Captura y Clasificación de Leads**

El escenario **"Captura de leads inmobiliarios"** tiene como objetivo centralizar la recepción de consultas, clasificarlas mediante Inteligencia Artificial (Gemini) y ejecutar acciones diferenciadas según la prioridad del cliente.

**Enlace de inicio del flujo :** 

**https://forms.gle/kdhcTRWNAHrzYW8z5**

### **1\. Resumen del Flujo de Trabajo**

El sistema opera bajo una arquitectura de **procesamiento en tiempo real** (Instant Hook). Sigue esta secuencia lógica:

1. **Recepción:** Captura de datos vía Webhook.  
2. **Normalización:** Mapeo de variables clave para el proceso.  
3. **Cerebro (IA):** Análisis de intención y urgencia.  
4. **Enrutamiento:** Ejecución de acciones (Alertas, Emails o Actualización de base de datos) basadas en la temperatura del lead.

---

### **2\. Detalle de Módulos y Funcionalidades**

| Orden | Módulo | Función Principal |
| :---- | :---- | :---- |
| **01** | **Custom Webhook** | Punto de entrada que recibe los datos del formulario web (Nombre, Teléfono, Interés, Presupuesto, etc.). |
| **02** | **Set Variables** | Organiza la información entrante en variables legibles para facilitar el mantenimiento del flujo. |
| **03** | **Gemini AI (Flash-Lite)** | **Clasificador:** Analiza el texto y asigna una categoría (**HOT, WARM, COLD**) y una razón corta basándose en reglas comerciales. |
| **04** | **Router** | Segmenta el camino que seguirá el lead según el resultado entregado por la IA. |

---

### **3\. Lógica de Clasificación (Reglas de Oro)**

El sistema utiliza un "Gerente Comercial Virtual" (Gemini) con instrucciones específicas para Bahía Blanca:

* **HOT (Prioridad Máxima):** \* Propietarios que quieren vender o alquilar (Captación).  
  * Compradores con urgencia nivel 4 o 5\.  
  * **Acción:** Genera alerta inmediata en Telegram y marca como "CONTACTADO".  
* **WARM (Seguimiento):** \* Interesados con presupuesto coherente pero sin urgencia inmediata.  
  * **Acción:** Envía un Email automático de bienvenida y marca como "EN SEGUIMIENTO".  
* **COLD (Descarte):** \* Consultas genéricas, spam o urgencia mínima (Nivel 1).  
  * **Acción:** Marca directamente como "DESCARTADO" en la base de datos sin notificar al equipo.

---

### **4\. Canales de Salida y Notificaciones**

#### **📱 Canal de Alerta (Lead HOT)**

Se utiliza un segundo módulo de **Gemini AI (Flash Latest)** para redactar una notificación optimizada para **Telegram** que incluye:

* Datos del cliente con emojis para lectura rápida.  
* **Mensaje sugerido para WhatsApp:** Redactado con tono argentino, listo para que el vendedor lo copie y pegue, acelerando el tiempo de respuesta.

#### **📧 Canal de Nutrición (Lead WARM)**

Envío automático a través de **Gmail** con un diseño profesional en HTML. Confirma al cliente que su consulta fue recibida y que un asesor lo contactará en un plazo de 24-48 hs.

#### **📊 Base de Datos (Google Sheets)**

El flujo cierra actualizando la fila correspondiente en la hoja de cálculo de Google, modificando la **Columna M (Estado)** según la clasificación obtenida, manteniendo así el CRM actualizado automáticamente.

---

### **5\. Robustez y Seguridad**

* **Manejo de Errores:** Se han implementado módulos de **"Break"** en los pasos críticos (IA, Email, Telegram). En caso de fallo de conexión, el sistema realizará hasta **3 reintentos** automáticos cada 1 minuto antes de detenerse.  
* **Formato de Datos:** La IA está configurada para responder estrictamente en formato **JSON**, garantizando que el Router pueda leer la clasificación sin errores de texto.

