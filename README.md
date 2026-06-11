
# 🚨 Hackeo DIAN: Informe de Ciberataque y Filtración de Datos

> **Repositorio con el análisis técnico y detalles del incidente de seguridad ocurrido en la DIAN de Colombia.**

---

## 📌 Descripción General

En **2024**, un actor malicioso explotó una **vulnerabilidad crítica sin parchear** en un sistema de terceros que gestiona el agendamiento de citas de la **DIAN (Dirección de Impuestos y Aduanas Nacionales de Colombia)**. Como consecuencia, se extrajo y filtró una base de datos masiva con información sensible de millones de ciudadanos, la cual fue posteriormente comercializada en la **Dark Web**.

Este repositorio recopila:
✅ **Análisis forense** del vector de ataque.
✅ **Métodos técnicos** empleados por el atacante.
✅ **Impacto** y consecuencias del incidente.
✅ **Recomendaciones** para usuarios y entidades.

---

## 🔍 Resumen del Incidente

| **Campo** | **Detalle** |
|-----------|-------------|
| **Entidad afectada** | DIAN (Colombia) |
| **Sistema vulnerado** | Plataforma externa de agendamiento de citas |
| **Proveedor externo** | CIEL Ingeniería |
| **Tipo de incidente** | Filtración de datos + Extorsión |
| **Volumen de datos** | 16 GB (base de datos SQLite) |
| **Registros comprometidos** | Nombres, cédulas, correos electrónicos, teléfonos |
| **Número de afectados** | Millones de ciudadanos |

---

## 🛠️ Vector de Ataque y Técnicas Utilizadas

### 🔴 Vulnerabilidades Explotadas

1. **Falta de parches y obsolescencia**
   - La plataforma de citas (gestionada por CIEL Ingeniería) llevaba **más de 12 meses** con una vulnerabilidad conocida sin corregir.
   - **Dwell Time prolongado**: Tiempo excesivo entre la detección de la falla y su parcheo.

2. **Inyección de Código y Ejecución Remota (RCE)**
   - El atacante **omitió autenticación** mediante fallos en la validación de solicitudes.
   - Ejecutó comandos directamente en el servidor web **sin credenciales**.

3. **Exposición de almacenamiento local**
   - La aplicación guardaba datos históricos en un **archivo SQLite de 16 GB** en el servidor.
   - **Error de permisos**: El archivo quedó accesible para descarga directa desde internet tras vulnerar el portal.

4. **Falta de segmentación**
   - La aplicación tenía **privilegios excesivos** sobre los archivos del sistema, permitiendo la extracción masiva de registros.

---

## 🕵️‍♂️ Cronología del Ataque

### **Fase 1: Reconocimiento y Explotación**
- El atacante usó **scanners automatizados** (como herramientas de subdominios y puertos) para identificar sistemas desactualizados.
- Detectó la vulnerabilidad en el portal de citas de la DIAN **sin parches desde hacía más de un año**.

### **Fase 2: Extracción de Datos**
- Utilizó un **exploit personalizado** para extraer los **16 GB de datos** en formato SQLite.
- La extracción se realizó de manera **silenciosa**, sin activar alertas en los sistemas de monitoreo.

### **Fase 3: Monetización y Extorsión**
- **Venta en la Dark Web**: La base de datos fue ofrecida por **~$2,000 USD** en criptomonedas.
- **Software malicioso incluido**: El atacante vendió también un **exploit personalizado** para que otros pudieran explotar la misma vulnerabilidad.

### **Fase 4: Respuesta de la DIAN**
1. **Desactivación del servicio**: Se suspendió temporalmente el sistema de agendamiento de citas.
2. **Auditoría con ColCERT**: Se trabajó con el **Grupo de Respuesta a Emergencias Cibernéticas de Colombia** para parchear la vulnerabilidad.
3. **Denuncia penal**: La DIAN presentó una **denuncia ante la Fiscalía General de la Nación**.

---

## ⚠️ Impacto del Incidente

### **Para los Ciudadanos**
- **Riesgo de phishing y suplantación**: Los datos filtrados (cédula, correo, teléfono) son ideales para **ataques de ingeniería social**.
- **Estafas dirigidas (Spear Phishing)**: Posibles llamadas o mensajes fraudulentos suplantando a la DIAN.

### **Para la DIAN**
- **Daño reputacional**: Pérdida de confianza en los sistemas digitales del Estado.
- **Interrupción operativa**: Retrasos en la atención al usuario por la suspensión del servicio.

---

## 🔐 Recomendaciones de Seguridad

### **Para los Usuarios**
🔹 **Desconfía de correos sospechosos**: La DIAN **nunca** solicita contraseñas, pines o descargas de archivos adjuntos para "evitar sanciones".
🔹 **Verifica el remitente**: Revisa que el correo provenga de `@dian.gov.co`.
🔹 **Usa canales oficiales**: Accede siempre a través de [https://dian.gov.co](https://dian.gov.co).

### **Para la DIAN y Proveedores**
🔹 **Parcheo inmediato**: Aplicar actualizaciones de seguridad tan pronto como se detecten vulnerabilidades.
🔹 **Segmentación de sistemas**: Limitar permisos de acceso para evitar extracciones masivas.
🔹 **Monitoreo continuo**: Implementar sistemas de detección de intrusiones (IDS/IPS).
🔹 **Auditorías periódicas**: Revisar configuraciones de permisos y almacenamiento de datos.

---

## 📚 Fuentes y Referencias

[1] Análisis forense de firmas de ciberseguridad.
[2] Informes de ColCERT y Fiscalía General de la Nación.
[3] Documentación técnica del proveedor CIEL
