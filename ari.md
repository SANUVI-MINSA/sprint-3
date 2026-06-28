# Ariana — Módulo de Comunicación y Pacientes

> Documentación técnica para el desarrollo de las secciones **Comunicación + Chat** y **Pacientes** (app del enfermero).

## Índice

1. [Sección: Comunicación + Chat](#1-sección-comunicación--chat)
2. [Sección: Pacientes](#2-sección-pacientes)
3. [Flujos](#3-flujos)
4. [Notas y pendientes](#4-notas-y-pendientes)

---

## 1. Sección: Comunicación + Chat

### 1.1 Pantallas

| Pantalla | Cuándo se muestra |
|---|---|
| **Bandeja de Consultas** | Al seleccionar "Consultas" en el nav inferior. Lista las consultas activas de las madres. |
| **Chat** | Al seleccionar una consulta (card) desde la Bandeja de Consultas. |
| **Modal "¿Cerrar consulta?"** | Al presionar el botón de cerrar dentro del chat, para confirmar o cancelar el cierre. |
| **Sin Consultas** | El enfermero tiene pacientes asignados, pero ninguna madre tiene una consulta activa. |
| **Sin Pacientes** | El enfermero no tiene pacientes asignados en su cartera. |
| **Sin Resultados de Búsqueda** | La búsqueda por nombre de paciente o madre no arroja resultados. |

<div align="center">
    <img src="resources/communication/Bandeja de Consultas.png" width="260">
</div>

<div align="center">
    <img src="resources/communication/chat.png" width="260">
</div>

<div align="center">
    <img src="resources/communication/modal-decision-cerrar.png" width="260">
</div>

<div align="center">
    <img src="resources/communication/Sin Consultas.png" width="260">
</div>

<div align="center">
    <img src="resources/communication/Sin pacientes asignados 0.png" width="260">
</div>

<div align="center">
    <img src="resources/communication/Sin resultados de Busqueda.png" width="260">
</div>

### 1.2 Endpoints

#### `GET /communication/consultations/nurse?searchTerm=`

Devuelve las consultas activas del enfermero. El campo `status` de la respuesta indica qué pantalla mostrar:

| `status` | Pantalla a mostrar |
|---|---|
| *(array con datos, sin campo `status`)* | Bandeja de Consultas, con la lista |
| `NO_CONSULTAS` | Frame "Sin Consultas" |
| `SIN_PACIENTES` | Frame "Sin Pacientes" |
| `BUSQUEDA_SIN_RESULTADOS` | Frame "Sin Resultados de Búsqueda" |

**Escenario 1 — Con consultas activas**

```json
[
  {
    "consultationId": "string",
    "patientId": "string",
    "patientName": "Mateo Pérez",
    "motherId": "string",
    "motherName": "Ana Pérez",
    "nurseId": "string",
    "nurseName": "María González",
    "lastMessage": "Gracias enfermera, aplicaré la indicación...",
    "lastMessageDate": "2024-01-15T10:30:00.000Z",
    "createdAt": "2024-01-15T10:00:00.000Z",
    "messageCount": 5
  },
  {
    "consultationId": "string",
    "patientId": "string",
    "patientName": "Valentina Gómez",
    "motherId": "string",
    "motherName": "María Gómez",
    "nurseId": "string",
    "nurseName": "María González",
    "lastMessage": "Mi hija tiene fiebre...",
    "lastMessageDate": "2024-01-15T11:00:00.000Z",
    "createdAt": "2024-01-15T10:30:00.000Z",
    "messageCount": 3
  }
]
```

**Escenario 2 — Tiene pacientes asignados pero NO tiene consultas activas** → Frame "Sin Consultas"

```json
{
  "consultations": [],
  "message": "No tienes consultas activas aún",
  "detail": "Las madres pueden iniciar consultas para sus hijos. Cuando una madre inicie una consulta, aparecerá aquí.",
  "status": "NO_CONSULTAS"
}
```

**Escenario 3 — NO tiene pacientes asignados en su cartera** → Frame "Sin Pacientes"

```json
{
  "consultations": [],
  "message": "No tienes pacientes asignados en tu cartera",
  "detail": "Puedes asignar pacientes a tu cartera desde el módulo de pacientes. Ve a 'Pacientes' y selecciona 'Asignar a mi cartera'.",
  "action": "Asignar pacientes",
  "status": "SIN_PACIENTES"
}
```

**Escenario 4 — Búsqueda sin resultados** → Frame "Sin Resultados de Búsqueda"

```json
{
  "consultations": [],
  "message": "No se encontraron consultas que coincidan con tu búsqueda",
  "detail": "No hay consultas con \"Carlos\" en el nombre del paciente o de la madre. Intenta con otro término.",
  "searchTerm": "Carlos",
  "status": "BUSQUEDA_SIN_RESULTADOS"
}
```

> Ver más: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/deployment-test/src/context/comunication-management/Documentacion.md#8-obtener-consultas-activas-de-una-enfermera-bandeja-de-consultas)

---

#### `POST /messages`

Envía un mensaje dentro de una teleconsulta activa.

**Request body:**
```json
{
  "consultationId": "string",
  "senderId": "string",
  "senderRole": "MOTHER | NURSE",
  "content": "string"
}
```

> Ver más: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/comunication-management/Documentacion.md#2-enviar-mensaje-madre-o-enfermera)

---

#### `GET /chat/:consultationId`

Abre el chat al seleccionar una consulta desde la Bandeja de Consultas.

```json
{
  "consultationId": "string",
  "patientId": "string",
  "nurseId": "string",
  "messages": [
    {
      "id": "string",
      "senderId": "string",
      "senderRole": "MOTHER | NURSE",
      "content": "string",
      "sentAt": "2024-01-15T10:30:00.000Z"
    }
  ]
}
```

> Ver más: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/comunication-management/Documentacion.md#6-obtener-chat-de-consulta-madre-o-enfermera)

---

#### `DELETE /consultations/close`

La enfermera cierra una teleconsulta. **Requisito:** debe haber enviado al menos un mensaje de respuesta.

**Request body:**
```json
{
    "consultationId": "string",
}
```

| Campo | Tipo | Requerido | Descripción                  |
|---|---|---|------------------------------|
| `consultationId` | string | ✅ | ID de la consulta            |
| `nurseId` | string | ✅ | ID de la enfermera via token |

**Response 200 OK**
```json
{
    "message": "Consultation closed successfully"
}
```

**Errores 400**

| Error | Significado |
|---|---|
| `Consultation not found` | La consulta no existe |
| `Only assigned nurse can close consultation` | Solo la enfermera asignada puede cerrar |
| `Consultation must contain at least one nurse response before closing` | La enfermera debe responder al menos una vez |


> Ver más: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/deployment/src/context/comunication-management/Documentacion.md#3-cerrar-consulta-enfermera)

---

## 2. Sección: Pacientes

### 2.1 Pantallas

| Pantalla | Cuándo se muestra |
|---|---|
| **Búsqueda de madre por DNI** | Pantalla inicial de la sección Pacientes. |
| **Pacientes registrados por la madre** | Tras encontrar a la madre, se listan sus pacientes (con su estado de asignación). |
| **Sin pacientes registrados** | La madre no registró ningún paciente desde FerovaFamily. |
| **Sin posta asignada** | El enfermero intenta asignarse un paciente, pero no tiene posta asignada por el admin. |

<div align="center">
<img src="resources/patient/Pacientes-Serch.png" width="260">
</div>

<div align="center">
<img src="resources/patient/Pacientes registados por la madre.png" width="260">
</div>

<div align="center">
<img src="resources/patient/Pacientes registados por la madre-1.png" width="260">
</div>

<div align="center">
<img src="resources/patient/CASO QUE NO HAY PACIENTES REGISTRADOS POR LA MADRE.png" width="260">
</div>

<div align="center">
<img src="resources/patient/Group 205.png" width="260">
</div>

### 2.2 Endpoints

#### `GET /mother/search/{search}`

```
searchTermin: "123..."
```

```json
{
  "motherId": "550e8400-...",
  "fullName": "Diana Carrillo",
  "dni": "12345678"
}
```

```
searchTermin: "12345678"
```

```json
{
  "motherId": "550e8400-...",
  "fullName": "Diana Carrillo",
  "dni": "12345678"
}
```

```
searchTermin: "12345"
```

```json
  { "error": "No mothers found matching the search criteria" }
```


**Errores 400**

| Error | Significado                 |
|---|-----------------------------|
| `Mother not found` | No existe madre con ese DNI |

> Ver más: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-mothersearchdni--buscar-madre-por-dni)

---

#### `GET /mother/{motherId}`

```json
[
  {
    "patientId": "660e8400-...",
    "patientName": "Mateo",
    "patientLastName": "Perez",
    "gender": "MALE",
    "status": "ACTIVE",
    "statusAssignment": "ASSIGNED"
  },
  {
    "patientId": "660e8400-...",
    "patientName": "Valentina",
    "patientLastName": "Gomez",
    "gender": "FEMALE",
    "status": "ACTIVE",
    "statusAssignment": "UNASSIGNED"
  }
]
```

Caso de que la madre no registró ningún paciente:

```json
[]
```

> Ver más: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-mothermotherid--listar-pacientes-por-madre)

---

#### `POST /assign-nurse`

**Request body:**
```json
{ "patientId": "660e8400-e29b-41d4-a716-446655440001" }
```

**Response 200 OK**
```json
{ "message": "Patient assigned successfully" }
```

**Error 404 — sin posta asignada**
```json
{ "message": "Nurse is not assigned to any facility" }
```

**Errores 400**

| Error | Significado           |
|---|-----------------------|
| `Nurse ID no encontrado en el token` | Token inválido        |
| `Patient not found` | El paciente no existe |
| `Patient already has an assigned nurse` | Ya tiene enfermera asignada       |
| `Nurse is not assigned to any facility` | Enfermera sin establecimiento        |


> Ver más: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#post-assign-nurse--asignarse-un-paciente)

---

## 3. Flujos

### 3.1 Comunicación + Chat

#### Escenario 1 — Pacientes asignados, sin consultas activas

<div align="center">
<img src="resources/communication/Group%20264.png" width="280">
</div>

1. Desde Home, el enfermero entra a "Consultas".
2. Se redirige a la Bandeja de Consultas (`GET /communication/consultations/nurse`).
3. Como no hay consultas activas, se muestra el frame **Sin Consultas**.

#### Escenario 2 — Sin pacientes asignados en la cartera

<div align="center">
<img src="resources/communication/Group%20267.png" width="280">
</div>

1. Desde Home, el enfermero entra a "Consultas".
2. Se redirige a la Bandeja de Consultas.
3. Como no tiene pacientes asignados, se muestra el frame **Sin Pacientes**, con un botón **"Asignar pacientes"**.
4. Al presionar el botón, se redirige a la sección Pacientes, donde puede buscar a la madre por DNI y asignar su paciente a la cartera.

#### Escenario 3 — Búsqueda de consultas por nombre

<div align="center">
<img src="resources/communication/Group%20266.png" width="280">
</div>

1. Desde Home, el enfermero entra a "Consultas" y ve la Bandeja de Consultas.
2. Escribe un nombre de paciente o madre en el buscador.
3. Si no hay coincidencias, se muestra el frame **Sin Resultados de Búsqueda**.
4. Si hay coincidencias, se muestran solo las consultas que coinciden con el término buscado.

#### Escenario 4 — Abrir chat, enviar mensaje y cerrar consulta

<div align="center">
<img src="resources/communication/Group%20265.png" width="280">
</div>

1. Desde Home, el enfermero entra a "Consultas" y ve la Bandeja de Consultas.
2. Selecciona una consulta → se abre el Chat (`GET /chat/:consultationId`).
3. Envía un mensaje a la madre (`POST /messages`).
4. Si la duda de la madre quedó resuelta, presiona el botón de cerrar consulta.
5. Se muestra el modal de confirmación "¿Cerrar consulta?".
6. Al confirmar, se llama a `DELETE /consultations/close`. La consulta se cierra y se elimina de la Bandeja de Consultas (la lista se actualiza).

> ⚠️ **Implicación de UX:** el cierre falla con error 400 (`Consultation must contain at least one nurse response before closing`) si el enfermero aún no envió ningún mensaje. El botón de cerrar debería deshabilitarse, o el modal no debería mostrarse, hasta que se haya enviado al menos un mensaje — así se evita mostrarle al usuario un error que se puede prevenir desde la UI.

### 3.2 Asignación de pacientes a la cartera del enfermero

#### Escenario 1 — La madre no tiene pacientes registrados en FerovaFamily

<div align="center">
<img src="resources/patient/Group%20261.png" width="280">
</div>

1. Desde Home, el enfermero entra a "Pacientes".
2. Ingresa el DNI de la madre (`GET /mother/search/{dni}`).
3. Si la madre no registró ningún paciente desde FerovaFamily, se muestra el frame **Sin pacientes registrados**.

#### Escenario 2 — El enfermero no tiene posta asignada por el admin

<div align="center">
<img src="resources/patient/Group%20263.png" width="280">
</div>

1. Desde Home, el enfermero entra a "Pacientes" e ingresa el DNI de la madre.
2. Selecciona a la madre en los resultados → se listan sus pacientes (`GET /mother/{motherId}`).
3. Presiona "Asignar" sobre un paciente (`POST /assign-nurse`).
4. Como el enfermero no tiene posta asignada por el admin, se muestra el modal **"Nurse is not assigned to any facility"**.
5. El paciente no se asigna a la cartera.

#### Escenario 3 — El enfermero sí tiene posta asignada

<div align="center">
<img src="resources/patient/Group%20262.png" width="280">
</div>

1. Desde Home, el enfermero entra a "Pacientes" e ingresa el DNI de la madre.
2. Selecciona a la madre en los resultados → se listan sus pacientes.
3. Presiona "Asignar" sobre un paciente (`POST /assign-nurse`).
4. Como sí tiene posta asignada, la asignación es exitosa y el card cambia de estado: **Sin asignar → Asignado**.

---

## 4. Notas y pendientes

**Sugerencia de UX (no bloqueante):**

- Animación al presionar el botón "Asignar paciente" (transición de estado "Sin asignar → Asignado"). Dyaron ya implementó algo similar en Flutter — vale la pena consultarle antes de construir esto desde cero.