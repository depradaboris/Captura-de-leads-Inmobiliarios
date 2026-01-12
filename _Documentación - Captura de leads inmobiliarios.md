## **?? Documentaci??n: Captura de leads inmobiliarios**

Links : 

* Google forms de captura de leads : https://docs.google.com/forms/d/e/1FAIpQLSduajHKBgFxeOQhTqCsinTtXMDFE3_SQsgwE3YpeAcnJEccLg/viewform?usp=dialog
* Google sheets de captura de leads : https://docs.google.com/spreadsheets/d/1dyF9kiOsVdNZlRs2Ay23CkXGqQ-tVPtx2-rQ0NgNgEw/edit?usp=sharing

### **1\. Disparador y Control de Flujo**

* **Google Sheets (Search Rows):** Consulta la hoja "Respuestas de formulario 1" buscando nuevas filas donde la columna "Enviado" (L) est?? vac??a. Limita la b??squeda a 5 registros por ejecuci??n para mantener un procesamiento controlado.  
* **Basic Router (Principal):** Dirige el flujo hacia los pasos de procesamiento s??lo si se confirma que existe un n??mero de fila v??lido. Act??a como un filtro de seguridad para evitar errores en ejecuciones vac??as.  
* **Sleep (Herramienta):** Pausa la ejecuci??n durante 15 segundos para dar margen al sistema antes de procesar los datos. Ayuda a evitar saturaci??n de la API y asegura que la informaci??n est?? asentada.

### **2\. Enriquecimiento y Datos**

"* **HTTP (Make a Request):** Conecta con la API de Abstract para obtener la fecha y hora exacta de Buenos Aires, Argentina. Esto asegura que el registro de contacto sea preciso y no dependa de la zona horaria del servidor.  "
"* **Set Variables:** Organiza y renombra los datos del lead (nombre, email, tel??fono, prioridad, etc.) en variables f??ciles de usar. Mapea la informaci??n de las columnas de Google Sheets para simplificar los pasos siguientes."

### **3\. Segmentaci??n y Respuesta (Router de Prioridad)**

* **Basic Router (Segmentaci??n):** Divide el camino seg??n la urgencia del lead: una ruta para "Muy Interesados" (prioridad \> 3\) y otra para "Menos Interesados" (prioridad ?? 3).  
* **Google Sheets (Update Row \- Ambas Rutas):** Actualiza la fila original del lead marcando la columna "Enviado" con el texto "ENVIADO". Esto evita que el mismo lead sea procesado nuevamente en la pr??xima ejecuci??n del flujo.  
* **Gmail (Send an Email \- Lead Muy Interesado):** Env??a un correo personalizado y urgente confirmando que un asesor se comunicar?? a la brevedad. Incluye un resumen detallado de la solicitud y los barrios de inter??s del cliente.  
* **Gmail (Send an Email \- Lead Menos Interesado):** Despacha un correo de confirmaci??n est??ndar agradeciendo el contacto y validando los datos recibidos. Mantiene una comunicaci??n profesional sin prometer una llamada inmediata.
