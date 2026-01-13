# 🚀 Guía Completa de n8n para Principiantes

> **Versión:** 1.0  
> **Última actualización:** Enero 2026  
> **Audiencia:** Usuarios sin experiencia previa en automatización

---

## 📋 Índice

1. [¿Qué es n8n?](#1-qué-es-n8n)
2. [Conceptos Básicos](#2-conceptos-básicos)
3. [Instalación y Configuración](#3-instalación-y-configuración)
4. [Tu Primer Workflow](#4-tu-primer-workflow)
5. [Nodos Esenciales](#5-nodos-esenciales)
6. [Credenciales y Conexiones](#6-credenciales-y-conexiones)
7. [Casos de Uso Prácticos](#7-casos-de-uso-prácticos)
8. [Buenas Prácticas](#8-buenas-prácticas)
9. [Solución de Problemas](#9-solución-de-problemas)
10. [Recursos Adicionales](#10-recursos-adicionales)

---

## 1. ¿Qué es n8n?

### 🎯 Definición Simple

**n8n** (pronunciado "n-eight-n") es una herramienta de **automatización de flujos de trabajo** que permite conectar diferentes aplicaciones y servicios para que trabajen juntos de forma automática, **sin necesidad de programar**.

### 💡 Analogía para Entenderlo

Imagina que n8n es como un **asistente virtual** que puede:
- Revisar tu email cada mañana
- Extraer información importante
- Guardarla en una hoja de Excel
- Enviarte un resumen por WhatsApp

Todo esto **automáticamente**, mientras tú te tomas el café ☕

### ✨ Beneficios Principales

| Beneficio | Descripción |
|-----------|-------------|
| **Ahorro de tiempo** | Automatiza tareas repetitivas que consumen horas |
| **Reducción de errores** | Los procesos automáticos son consistentes |
| **Sin código** | Interfaz visual de arrastrar y soltar |
| **Open Source** | Gratuito y con comunidad activa |
| **Flexible** | Se conecta con +400 aplicaciones |

---

## 2. Conceptos Básicos

### 🧩 Vocabulario Esencial

Antes de empezar, es importante entender estos términos:

#### **Workflow (Flujo de Trabajo)**
Un workflow es una **secuencia de pasos automatizados** que realiza una tarea. Piensa en él como una receta de cocina: tiene ingredientes (datos) y pasos (nodos) para obtener un resultado final.

```
📥 Entrada → 🔄 Proceso → 📤 Salida
```

#### **Nodo (Node)**
Un nodo es un **bloque individual** que realiza una acción específica. Cada nodo:
- Recibe datos de entrada
- Ejecuta una acción
- Produce datos de salida

**Tipos de nodos:**
- 🟢 **Trigger (Disparador):** Inicia el workflow (ej: cada hora, al recibir un email)
- 🔵 **Action (Acción):** Hace algo con los datos (ej: enviar email, crear archivo)
- 🟡 **Transform (Transformación):** Modifica los datos (ej: filtrar, combinar)

#### **Ejecución (Execution)**
Cada vez que un workflow se activa y ejecuta todos sus pasos, se llama una **ejecución**. Puedes ver el historial de ejecuciones para revisar qué pasó.

#### **Credenciales (Credentials)**
Son las **"llaves"** que permiten a n8n conectarse con otros servicios (Gmail, Excel, Slack, etc.). Se configuran una vez y se reutilizan.

### 🔄 Flujo de Datos

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   TRIGGER   │────▶│   ACCIÓN 1  │────▶│   ACCIÓN 2  │
│  (Inicio)   │     │ (Procesar)  │     │  (Guardar)  │
└─────────────┘     └─────────────┘     └─────────────┘
      │                    │                    │
      ▼                    ▼                    ▼
   Dispara            Transforma            Resultado
   el flujo           los datos              final
```

---

## 3. Instalación y Configuración

### 🖥️ Opción 1: n8n Cloud (Recomendado para Principiantes)

La forma más fácil de empezar es usar **n8n Cloud**, la versión en la nube que no requiere instalación.

#### Pasos:

1. **Visitar n8n Cloud**
   - Ir a: [https://app.n8n.cloud](https://app.n8n.cloud)

2. **Crear una cuenta**
   - Clic en "Sign Up"
   - Usar email corporativo o cuenta de Google
   - Verificar el email

3. **Acceder al panel**
   - Una vez verificado, ya tienes acceso al editor de workflows

> ⚡ **Ventaja:** Prueba gratuita de 14 días sin tarjeta de crédito

### 💻 Opción 2: Instalación Local con Docker

Para empresas que prefieren tener control total:

```bash
# Instalar Docker (si no lo tienes)
# Descargar desde: https://www.docker.com/products/docker-desktop

# Ejecutar n8n con Docker
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

Acceder a: `http://localhost:5678`

### 🪟 Opción 3: Instalación en Windows con npm

```bash
# Requisitos: Node.js 18+ instalado

# Instalar n8n globalmente
npm install n8n -g

# Iniciar n8n
n8n start
```

---

## 4. Tu Primer Workflow

### 🎓 Tutorial: "Hola Mundo" en n8n

Vamos a crear un workflow simple que se ejecute manualmente y muestre un mensaje.

#### Paso 1: Crear nuevo workflow

1. En el panel principal, clic en **"+ New Workflow"**
2. Se abre el editor visual (canvas vacío)

#### Paso 2: Añadir nodo Trigger

1. Clic en el botón **"+"** en el centro
2. Buscar: **"Manual Trigger"**
3. Seleccionarlo (aparece en el canvas)

> 💡 El Manual Trigger permite ejecutar el workflow con un clic

#### Paso 3: Añadir nodo de acción

1. Clic en el **"+"** a la derecha del Manual Trigger
2. Buscar: **"Set"**
3. Configurar el nodo Set:
   - Clic en "Add Field"
   - Nombre: `mensaje`
   - Valor: `¡Hola! Este es mi primer workflow en n8n 🎉`

#### Paso 4: Ejecutar el workflow

1. Clic en el botón **"Execute Workflow"** (esquina inferior)
2. Ver el resultado en el panel derecho

```
Resultado esperado:
{
  "mensaje": "¡Hola! Este es mi primer workflow en n8n 🎉"
}
```

#### Paso 5: Guardar el workflow

1. Clic en **"Save"** (esquina superior derecha)
2. Nombrar: "Mi Primer Workflow"

### 🎊 ¡Felicidades!

Has completado tu primer workflow. Aunque es simple, ya entiendes el concepto básico de cómo funcionan los nodos y la ejecución.

---

## 5. Nodos Esenciales

### 📌 Los 10 Nodos que Debes Conocer

#### 1. **Manual Trigger** 🟢
- **Qué hace:** Inicia el workflow manualmente
- **Cuándo usarlo:** Para pruebas o workflows que ejecutas tú mismo
- **Ejemplo:** Generar un reporte cuando lo necesites

#### 2. **Schedule Trigger** 🟢
- **Qué hace:** Ejecuta el workflow en horarios programados
- **Cuándo usarlo:** Tareas recurrentes (diarias, semanales, etc.)
- **Ejemplo:** Enviar resumen de ventas cada lunes a las 9:00

```
Configuración típica:
- Rule: CRON
- Expression: 0 9 * * 1  (Cada lunes a las 9:00)
```

#### 3. **HTTP Request** 🔵
- **Qué hace:** Realiza peticiones a APIs web
- **Cuándo usarlo:** Obtener o enviar datos a servicios externos
- **Ejemplo:** Consultar el clima, obtener cotizaciones

#### 4. **Set** 🟡
- **Qué hace:** Define o modifica valores de datos
- **Cuándo usarlo:** Preparar datos antes de usarlos
- **Ejemplo:** Crear un objeto con fecha y usuario

#### 5. **IF** 🟡
- **Qué hace:** Divide el flujo según condiciones
- **Cuándo usarlo:** Cuando necesitas lógica condicional
- **Ejemplo:** Si el total > 1000, enviar alerta

```
Condición ejemplo:
{{ $json.total }} > 1000
```

#### 6. **Code** 🟡
- **Qué hace:** Ejecuta código JavaScript personalizado
- **Cuándo usarlo:** Transformaciones complejas
- **Ejemplo:** Formatear fechas, calcular porcentajes

```javascript
// Ejemplo: Formatear fecha
const fecha = new Date($input.first().json.fecha);
return {
  fechaFormateada: fecha.toLocaleDateString('es-ES')
};
```

#### 7. **Merge** 🟡
- **Qué hace:** Combina datos de múltiples fuentes
- **Cuándo usarlo:** Unir información de diferentes nodos
- **Ejemplo:** Combinar datos de clientes con sus pedidos

#### 8. **Loop Over Items** 🟡
- **Qué hace:** Procesa cada elemento de una lista
- **Cuándo usarlo:** Cuando tienes múltiples items
- **Ejemplo:** Enviar un email a cada cliente de una lista

#### 9. **Wait** 🟡
- **Qué hace:** Pausa la ejecución por un tiempo
- **Cuándo usarlo:** Respetar límites de API, esperar procesos
- **Ejemplo:** Esperar 5 segundos entre peticiones

#### 10. **Error Trigger** 🟢
- **Qué hace:** Se activa cuando hay un error en otro workflow
- **Cuándo usarlo:** Manejo de errores y notificaciones
- **Ejemplo:** Enviar alerta cuando un workflow falla

---

## 6. Credenciales y Conexiones

### 🔐 ¿Qué son las Credenciales?

Las credenciales son la forma en que n8n se conecta de forma segura con otros servicios. Es como darle a n8n una llave para entrar a tu Gmail, Excel, Slack, etc.

### 📝 Crear Credenciales (Ejemplo: Gmail)

#### Paso 1: Ir a Credenciales
1. Menú lateral izquierdo → **Settings** → **Credentials**
2. Clic en **"+ Add Credential"**

#### Paso 2: Seleccionar tipo
1. Buscar: "Gmail"
2. Seleccionar "Gmail OAuth2"

#### Paso 3: Configurar OAuth2
1. Necesitas ID de cliente y secreto de Google Cloud
2. Seguir el asistente de conexión
3. Autorizar el acceso

> ⚠️ **Importante:** Los administradores de IT suelen configurar las credenciales una vez para todo el equipo.

### 🔗 Servicios Comunes y sus Credenciales

| Servicio | Tipo de Credencial | Dificultad |
|----------|-------------------|------------|
| Gmail | OAuth2 | Media |
| Microsoft 365 | OAuth2 | Media |
| Slack | OAuth2 o API Token | Fácil |
| Google Sheets | OAuth2 | Media |
| Notion | API Token | Fácil |
| Airtable | Personal Access Token | Fácil |
| PostgreSQL | Usuario/Contraseña | Fácil |

### 💡 Consejos sobre Credenciales

1. **Nunca compartas credenciales** en texto plano
2. **Usa cuentas de servicio** dedicadas cuando sea posible
3. **Revisa los permisos** mínimos necesarios
4. **Documenta** qué credenciales usa cada workflow

---

## 7. Casos de Uso Prácticos

### 📧 Caso 1: Guardar Adjuntos de Email en OneDrive

**Problema:** Cada vez que recibes un email con adjuntos importantes, tienes que descargarlos y subirlos manualmente a OneDrive.

**Solución con n8n:**

```
📧 Email Trigger → 📎 Filtrar con adjuntos → 📁 Subir a OneDrive → ✅ Notificar
```

**Nodos necesarios:**
1. Microsoft Outlook Trigger (nuevo email)
2. IF (tiene adjuntos?)
3. Microsoft OneDrive (subir archivo)
4. Slack (notificar que se guardó)

---

### 📊 Caso 2: Reporte Semanal Automático

**Problema:** Cada semana tienes que extraer datos de Excel, procesarlos y enviar un resumen por email.

**Solución con n8n:**

```
⏰ Schedule (Lunes 9am) → 📊 Leer Excel → 🔄 Procesar datos → 📧 Enviar email
```

**Nodos necesarios:**
1. Schedule Trigger (cada lunes)
2. Microsoft Excel (leer datos)
3. Code (calcular totales)
4. Gmail (enviar resumen)

---

### 💬 Caso 3: Bot de Slack para Consultas

**Problema:** Los empleados hacen preguntas repetitivas en Slack que podrían responderse automáticamente.

**Solución con n8n:**

```
💬 Slack Trigger → 🤖 Analizar pregunta → 📚 Buscar respuesta → 💬 Responder
```

**Nodos necesarios:**
1. Slack Trigger (nuevo mensaje con mención)
2. IF (contiene palabra clave?)
3. Notion (buscar en base de conocimiento)
4. Slack (responder en hilo)

---

### 📝 Caso 4: Sincronizar Formularios con Base de Datos

**Problema:** Los datos de formularios de Google Forms deben llegar a tu base de datos interna.

**Solución con n8n:**

```
📝 Google Forms → 🔄 Transformar datos → 🗄️ Insertar en BD → ✅ Confirmar
```

**Nodos necesarios:**
1. Webhook (recibe datos de Forms)
2. Set (formatear campos)
3. MySQL (insertar registro)
4. Email (confirmar recepción)

---

## 8. Buenas Prácticas

### ✅ Hacer (Do's)

#### 1. **Nombrar workflows claramente**
```
❌ Malo: "Workflow 1"
✅ Bueno: "Reporte Ventas Semanal - Envío Automático"
```

#### 2. **Usar notas y sticky notes**
- Añade notas explicativas en el canvas
- Documenta qué hace cada sección

#### 3. **Testear antes de activar**
- Usa "Execute Workflow" para probar
- Revisa los datos en cada paso
- Verifica con datos reales de prueba

#### 4. **Manejar errores**
- Añade nodos de notificación de errores
- Configura reintentos cuando sea apropiado
- Crea un workflow de "Error Handler"

#### 5. **Versionar workflows importantes**
- Exporta el JSON periódicamente
- Guarda en repositorio de control de versiones

### ❌ Evitar (Don'ts)

#### 1. **No ignorar los límites de API**
- Respeta los rate limits de servicios externos
- Usa nodos Wait cuando sea necesario

#### 2. **No hardcodear valores sensibles**
- Usa credenciales para tokens y contraseñas
- Usa variables de entorno para configuraciones

#### 3. **No crear workflows monolíticos**
- Divide workflows grandes en subworkflows
- Facilita el mantenimiento y debugging

#### 4. **No olvidar la documentación**
- Cada workflow debe tener su propósito documentado
- Incluye instrucciones para modificaciones

---

## 9. Solución de Problemas

### 🔧 Problemas Comunes y Soluciones

#### ❓ "El workflow no se ejecuta automáticamente"

**Causas posibles:**
1. El workflow no está **activado** (toggle superior derecho)
2. El trigger no está bien configurado
3. Las credenciales expiraron

**Solución:**
1. Verificar que el toggle de activación esté en verde
2. Revisar la configuración del trigger
3. Re-autenticar las credenciales

---

#### ❓ "Error de credenciales"

**Mensaje:** "Credentials are not valid"

**Causas posibles:**
1. Token expirado
2. Permisos insuficientes
3. Credenciales incorrectas

**Solución:**
1. Ir a Settings → Credentials
2. Editar la credencial problemática
3. Re-autenticar o regenerar tokens

---

#### ❓ "Los datos no llegan al siguiente nodo"

**Causas posibles:**
1. El nodo anterior no produce output
2. El filtro IF está bloqueando los datos
3. El mapeo de datos es incorrecto

**Solución:**
1. Ejecutar paso a paso
2. Revisar el output de cada nodo
3. Verificar las expresiones de mapeo

---

#### ❓ "El workflow es muy lento"

**Causas posibles:**
1. Demasiados items procesados en serie
2. APIs externas lentas
3. Operaciones innecesarias

**Solución:**
1. Usar procesamiento en paralelo cuando sea posible
2. Cachear datos que no cambian frecuentemente
3. Optimizar el flujo eliminando pasos redundantes

---

### 🆘 Dónde Obtener Ayuda

| Recurso | URL | Para qué |
|---------|-----|----------|
| Documentación Oficial | [docs.n8n.io](https://docs.n8n.io) | Referencia técnica |
| Comunidad | [community.n8n.io](https://community.n8n.io) | Preguntas y ejemplos |
| YouTube | Canal n8n | Tutoriales en video |
| Discord | n8n Discord | Chat en tiempo real |

---

## 10. Recursos Adicionales

### 📚 Plantillas Recomendadas

n8n incluye una librería de plantillas listas para usar:

1. **Productividad**
   - Backup automático de Notion
   - Sincronizar Google Calendar con Notion

2. **Marketing**
   - Posts automáticos en redes sociales
   - Seguimiento de menciones de marca

3. **Ventas**
   - CRM automation con HubSpot
   - Notificaciones de nuevos leads

4. **IT/DevOps**
   - Monitoreo de servidores
   - Deploy automático con GitHub

### 🎓 Ruta de Aprendizaje Sugerida

```
Semana 1: Conceptos básicos + Tu primer workflow
    ↓
Semana 2: Nodos de transformación (Set, Code, IF)
    ↓
Semana 3: Integraciones con servicios (Email, Excel)
    ↓
Semana 4: Proyectos prácticos del día a día
    ↓
Continuo: Optimización y casos avanzados
```

### 📋 Checklist del Principiante

- [ ] Crear cuenta en n8n Cloud
- [ ] Completar el tutorial "Hola Mundo"
- [ ] Configurar primera credencial
- [ ] Crear workflow con Schedule Trigger
- [ ] Conectar con una herramienta del trabajo (Email/Excel/Slack)
- [ ] Automatizar una tarea repetitiva real
- [ ] Documentar el workflow creado
- [ ] Compartir con el equipo

---

## 📞 Contacto y Soporte Interno

Para dudas específicas de nuestra empresa:

- **Canal de Slack:** #automatizaciones
- **Responsable técnico:** [Añadir nombre]
- **Documentación interna:** [Añadir enlace]

---

> 💡 **Recuerda:** La mejor forma de aprender n8n es practicando. Empieza con automatizaciones pequeñas y ve aumentando la complejidad gradualmente.

---

*Guía creada para el equipo de [Nombre de Empresa]*  
*¿Sugerencias? Abre un issue o envía feedback al canal de Slack*
