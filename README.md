# 🧩 Combustibles Unigas | NSX  
![version](https://img.shields.io/badge/Versión2-1.25.10.11-blue.svg)  
![estado](https://img.shields.io/badge/Estado-Estable-brightgreen.svg)  
![NSX](https://img.shields.io/badge/NSX-2-orange.svg)

---

## 📘 Descripción General  

La **API de Combustibles Unigas** proporciona acceso a los **maestros de configuración corporativos** utilizados por las distintas **unidades de negocio** de la organización.  

Su propósito es **unificar y homologar** las estructuras de datos con el **ERP SIESA**, garantizando coherencia, trazabilidad e integración fluida entre sistemas.  

Mediante **consultas y conectores dinámicos**, permite una **integración automatizada**, optimizando procesos, reduciendo duplicidades y centralizando la información maestra.  

---

## ⚙️ Funcionalidad  

Ofrece un conjunto integral de servicios para la **gestión y consulta dinámica de maestros corporativos**, facilitando la interoperabilidad con el **ERP SIESA** y sistemas externos.

### 🔹 Principales funcionalidades  

- **Consultas dinámicas** de terceros con filtros flexibles.  
- Obtención de **maestros**:
  - Compañías  
  - Unidades de negocio  
  - Bodegas  
  - Centros de operación  
  - Unidades de medida  
  - Ítems  
- **Cuentas por Cobrar (CxC)**:
  - Detalle de movimientos por cliente  
  - Consolidado general de saldos  
- **Cuentas por Pagar (CxP)**:
  - Detalle de facturas y documentos asociados  
  - Consolidado general de obligaciones  
- **Creación dinámica de terceros (POST)**  
- **Gestión comercial**:
  - Remisiones  
  - Ventas de contado  
  - Facturación electrónica  
- **Servidor de pruebas** para validación antes de producción  

---

## 🔗 Integración y Pruebas  

Los endpoints están disponibles en el **servidor de pruebas** para validar consultas y conectores antes del paso a producción.  

| Entorno | Ruta Base |
|----------|------------|
| 🧪 **QA / Pruebas** | `/ConnektaQA` |
| 🚀 **Producción** | `/Core` |

---

### 💻 Ejemplo `curl`

```bash
curl -X 'GET' \
  'http://SERVER/v3/CONSULTA_CONECTOR?PARAMETROS' \
  -H 'accept: */*' \
  -H 'Key: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX' \
  -H 'Token: WSXWSXWSXWSXWSXWSXWSXWSXWSXWSXWSXWsdSXQ'
```

### 🔍 Ejemplo de Endpoint
![GET](https://img.shields.io/badge/GET-brightgreen.svg) 
```bash
GET http://SERVER/v3/CONSULTA_CONECTOR?PARAMETROS
```

![POST](https://img.shields.io/badge/POST-orange.svg) 
```bash
POST http://SERVER/v3/CONSULTA_CONECTOR?PARAMETROS
```

### 📡 Respuesta del Servidor
```bash
content-length: 436 
content-type: application/json; charset=utf-8 
date: Wed, 29 Oct 2025 00:35:07 GMT 
server: Microsoft-IIS/10.0 
x-powered-by: ASP.NET 
```

### 🧠 Ejemplos de Respuesta
tip
Los siguientes ejemplos reflejan posibles respuestas del servicio según el estado de la operación o la validez de los parámetros enviados.

✅ 200 - Éxito
```json
{
  "status": 200,
  "message": "Consulta procesada correctamente",
  "data": [
    {
      "codigo": "B001",
      "descripcion": "Bodega Principal Bogotá",
      "estado": "Activo"
    }
  ]
}
```

🕓 200 - Pendiente
```json
{
  "status": 200,
  "message": "Solicitud en proceso de sincronización con ERP",
  "job_id": "SYNC-984512",
  "timestamp": "2025-10-28T15:32:45Z"
}
```

❌ 400 - Solicitud Inválida
```json
{
  "status": 400,
  "error": "Parámetros inválidos o faltantes",
  "detalle": "El campo 'unidad_negocio' es obligatorio."
}
```

🔒 401 - No Autorizado
```json
{
  "status": 401,
  "error": "Acceso no autorizado",
  "detalle": "Clave o token no válidos."
}
```

🚫 404 - Recurso No Encontrado
```json
{
  "status": 404,
  "error": "Recurso no existe",
  "detalle": "El endpoint o maestro solicitado no fue encontrado."
}
```

💥 500 - Error Interno
```json
{
  "status": 500,
  "error": "Error interno del servidor",
  "detalle": "Error inesperado durante la ejecución del conector."
}
```

### 🔐 Autenticación y Seguridad

Cada proveedor de desarrollo deberá solicitar sus credenciales de acceso (Key / Token) al área de Tecnología.
Las credenciales son únicas, temporales y asociadas a su entorno de pruebas.

Key → Identificador de aplicación o integración.
Token → Credencial temporal o por sesión.

Método recomendado → Autenticación por encabezados HTTP seguros (Header Authorization).

Comunicación → Exclusivamente bajo HTTPS.

Header:
Key: XXXXXXXXXXXXXXXXXXXXXXXX
Token: XXXXXXXXXXXXXXXXXXXXX

🧩 Guía para Proveedores Externos de Desarrollo

Esta guía aplica para empresas integradoras, freelancers o desarrolladores que creen conectores o servicios sobre la API Combustibles Unigas SAS.

✅ Buenas Prácticas

* Usar siempre el entorno QA antes de solicitar despliegue.
* Documentar los endpoints consumidos y parámetros utilizados.
* Registrar logs de ejecución para trazabilidad.
* Evitar llamadas masivas sin control de paginación.
* Validar códigos HTTP antes de continuar un flujo.

🚫 No permitido

* Usar credenciales de producción sin autorización.
* Modificar estructuras del payload sin aprobación.
* Publicar endpoints o tokens en repositorios públicos.

📎 Información Complementaria
Tema	Detalle
📚 Documentación ERP SIESA	Disponible bajo solicitud interna
🧠 Manual de conectores	En actualización
🔐 Seguridad	Basada en Key + Token + HTTPS
🧾 Contacto técnico	cio@grupounigas.co
---
© Combustibles Unigas - Dirección de Tecnología | 2025
Documentación generada para uso interno y controlado de proveedores de integración con ERP SIESA.
---