# Dyron — Historial Médico y Control de Hemoglobina

> Documentación técnica para el desarrollo de las secciones **Historial Médico** y **Control de Hemoglobina** (app del enfermero). Ambas secciones parten de la lista de pacientes asignados a la cartera del enfermero — asignación que se hace desde la sección Pacientes (a cargo de Ariana).

## Índice

1. [Sección: Historial Médico](#1-sección-historial-médico)
2. [Sección: Control de Hemoglobina](#2-sección-control-de-hemoglobina)
3. [Flujos](#3-flujos)
4. [Notas y pendientes](#4-notas-y-pendientes)

---

## 1. Sección: Historial Médico

### 1.1 Pantallas

| Pantalla | Cuándo se muestra |
|---|---|
| **Lista de pacientes (Historial Médico)** | Pantalla inicial de la sección. Lista los pacientes de la cartera del enfermero. |
| **Card con botones "Ver" y "Actualizar"** | Se habilitan en el card de un paciente cuando éste ya tiene un historial médico registrado. |
| **Sin pacientes asignados (Historial Médico)** | El enfermero no tiene pacientes en su cartera. |
| **Registrar Historial Médico** | Formulario para crear el historial médico del paciente seleccionado. |
| **Modal: registrar antecedentes** | Se abre desde el formulario de historial médico para agregar antecedentes. |
| **Modal: registrar síntomas** | Se abre desde el formulario de historial médico para agregar síntomas. |
| **Actualizar Historial Médico** | Formulario de edición de un historial médico ya existente (botón "Actualizar" del card). |

**Lista de pacientes (Historial Médico):**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Selecionar%20Paciente%20Historial%20Medico.png" width="260">
</div>

**Card con botones "Ver" y "Actualizar" habilitados:**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Selecionar%20Paciente%20Historial%20Medico%20(1).png" width="260">
</div>

**Sin pacientes asignados (Historial Médico):**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Selecionar%20Paciente%20Historial%20Medico%203.png" width="260">
</div>

**Registrar Historial Médico:**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Mateo-Historial%20Medico.png" width="260">
</div>

**Modal: registrar antecedentes:**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Background+Border+Shadow%20(1).png" width="260">
</div>

**Modal: registrar síntomas:**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Background+Border+Shadow.png" width="260">
</div>

**Actualizar Historial Médico:**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Actualizar.png" width="260">
</div>

### 1.2 Endpoints

#### `GET patients/nurse`

Lista los pacientes en la cartera del enfermero. Se usa tanto en **Historial Médico** como en **Control de Hemoglobina** (sección 2) para seleccionar al paciente sobre el que se va a registrar información.

```json
[
  {
    "patientId": "b77eab3c-3ab7-40b8-9fb3-e4dd7b63d4b6",
    "fullName": "Mateo Perez",
    "gender": "MALE",
    "status": "ACTIVE",
    "facilityId": "33e8ab63-2875-41b5-91f1-ac9a37d1ddc6"
  },
  {
    "patientId": "bd16a94a-7171-4f5b-a561-0cf10db13770",
    "fullName": "Diana Lucia Briceño Vera",
    "gender": "MALE",
    "status": "ACTIVE",
    "facilityId": "33e8ab63-2875-41b5-91f1-ac9a37d1ddc6"
  },
  {
    "patientId": "8ad97c1d-7a3c-4101-b086-8551b0a85f6a",
    "fullName": "Daniel Baca",
    "gender": "MALE",
    "status": "ACTIVE",
    "facilityId": "33e8ab63-2875-41b5-91f1-ac9a37d1ddc6"
  },
  {
    "patientId": "072a086a-68c4-4952-bbf8-0362d23d3a22",
    "fullName": "Pepe DeTal",
    "gender": "MALE",
    "status": "ACTIVE",
    "facilityId": "33e8ab63-2875-41b5-91f1-ac9a37d1ddc6"
  },
  {
    "patientId": "40094724-fc8f-44cb-9b34-d349f5de97cb",
    "fullName": "testeo tal",
    "gender": "FEMALE",
    "status": "ACTIVE",
    "facilityId": "33e8ab63-2875-41b5-91f1-ac9a37d1ddc6"
  },
  {
    "patientId": "0c311ed8-ac1e-43d3-ba9c-d07518c23912",
    "fullName": "Paoly Gonzalez",
    "gender": "FEMALE",
    "status": "ACTIVE",
    "facilityId": "33e8ab63-2875-41b5-91f1-ac9a37d1ddc6"
  }
]
```

Caso de arreglo vacío → mostrar el frame **Sin pacientes asignados**, con un botón "Asignar pacientes" que redirige a la sección Pacientes. Esto aplica tanto en Historial Médico como en Control de Hemoglobina:

```json
[]
```

> Ver más info: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-nurse--listar-pacientes-asignados)

---

#### `POST /medical-record`

Crea el historial médico de un paciente seleccionado desde `GET patients/nurse`.

**Request body:**
```json
{
  "patientId": "660e8400-e29b-41d4-a716-446655440001",
  "weight": 12.5,
  "height": 85,
  "motivoConsulta": "Control de rutina y evaluación de crecimiento",
  "observaciones": "Paciente en buen estado general, activo, sin signos de alarma",
  "antecedentes": [
    { "type": "alergia", "description": "Penicilina" },
    { "type": "antecedente_familiar", "description": "Madre con anemia" }
  ],
  "sintomas": ["fiebre", "tos", "decaimiento"]
}
```

**Response 201 Created**
```json
{ "message": "Medical record created successfully" }
```

Una vez creado, en el card de ese paciente (dentro de `GET patients/nurse`) se habilitan los botones **"Ver historial"** y **"Actualizar"**.

> Ver más info: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#post-medical-record--crear-historia-cl%C3%ADnica)

---

#### `GET /{patientId}/medical-record`

Devuelve los datos del paciente junto con su historial médico y sus controles de hemoglobina.

**Caso: historial recién creado, sin controles de hemoglobina aún**
```json
{
  "patient": {
    "id": "072a086a-68c4-4952-bbf8-0362d23d3a22",
    "name": "Pepe",
    "lastName": "DeTal",
    "birthDate": "2025-12-09T00:00:00.000Z",
    "currentWeight": 20,
    "currentHeight": 148,
    "motherId": "6a1b179c2b5b07eee905898d",
    "nurseId": "6a22a5f92b5b07eee90589aa",
    "gender": "MALE",
    "facilityId": "33e8ab63-2875-41b5-91f1-ac9a37d1ddc6",
    "status": "ACTIVE"
  },
  "medicalRecord": {
    "id": "d43bcf6e-bfdc-4122-a621-87dfb125597a",
    "createdAt": "2026-06-26T14:03:03.394Z",
    "updatedAt": "2026-06-26T14:03:03.394Z",
    "hemoglobinLevel": null,
    "weight": 12.5,
    "height": 85,
    "gender": "MALE",
    "antecedentes": [
      { "type": "alergia", "description": "Penicilina" }
    ],
    "motivoConsulta": "Control de rutina",
    "observaciones": "Paciente en buen estado general",
    "controls": [],
    "patientId": "072a086a-68c4-4952-bbf8-0362d23d3a22",
    "nurseId": "6a22a5f92b5b07eee90589aa",
    "sintomas": ["fiebre", "tos"]
  }
}
```

> 🔑 **Campos clave:**
> - `patient.id` → úsalo para redirigir al formulario de registro de control de hemoglobina de este paciente (ver frame "Historial médico creado por primera vez", sección 2.1).
> - `medicalRecord.hemoglobinLevel: null` junto con `controls: []` → significa que el paciente **aún no tiene ningún control de hemoglobina registrado**. En este caso se muestra el botón **"Realizar primer control"** en el card de hemoglobina.

**Caso: ya tiene al menos un control de hemoglobina registrado**

Una vez registrado el primer control (ver `POST /hemoglobin-control` en la sección 2.2), `hemoglobinLevel` deja de ser `null` y refleja el valor del control más reciente, y `controls` deja de estar vacío. El botón "Realizar primer control" desaparece y se muestra el control más reciente junto con un botón "Ver historial":

```json
{
  "patient": {
    "id": "0c311ed8-ac1e-43d3-ba9c-d07518c23912",
    "name": "Paoly",
    "lastName": "Gonzalez",
    "birthDate": "2023-06-12T00:00:00.000Z",
    "currentWeight": 50,
    "currentHeight": 170,
    "motherId": "6a1b179c2b5b07eee905898d",
    "nurseId": "6a22a5f92b5b07eee90589aa",
    "gender": "FEMALE",
    "facilityId": "33e8ab63-2875-41b5-91f1-ac9a37d1ddc6",
    "status": "ACTIVE"
  },
  "medicalRecord": {
    "id": "8e2b3ce5-59eb-4bc7-aec7-1ecd2849ad51",
    "createdAt": "2026-06-21T05:07:56.525Z",
    "updatedAt": "2026-06-21T05:08:12.309Z",
    "hemoglobinLevel": 20,
    "weight": 12.5,
    "height": 85,
    "gender": "FEMALE",
    "antecedentes": [
      { "type": "alergia", "description": "Penicilina" }
    ],
    "motivoConsulta": "Control de rutina",
    "observaciones": "Paciente en buen estado general",
    "controls": [
      {
        "id": "4fcdd88c-132c-4e52-b771-377a7f5b1336",
        "date": "2026-06-21T05:08:12.308Z",
        "hemoglobinLevel": 20,
        "anemiaStatus": "CONTROLLED"
      }
    ],
    "patientId": "0c311ed8-ac1e-43d3-ba9c-d07518c23912",
    "nurseId": "6a22a5f92b5b07eee90589aa",
    "sintomas": ["fiebre", "tos"]
  }
}
```

> El registro de control de hemoglobina también puede hacerse desde Home, en accesos rápidos → "Registrar control" (ver Flujo 4, sección 3).

> Ver más info: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-patientidmedical-record--historia-cl%C3%ADnica-completa)

---

#### `PUT /medical-record/update`

Actualiza el historial médico de un paciente (se habilita junto con el botón "Actualizar" una vez que el historial fue creado). Los datos actualizados se reflejan luego en `GET /{patientId}/medical-record`.

**Request body:**
```json
{
  "patientId": "660e8400-e29b-41d4-a716-446655440001",
  "weight": 13.2,
  "height": 88,
  "motivoConsulta": "Control de crecimiento y desarrollo",
  "observaciones": "Paciente con buen apetito, peso adecuado para la edad",
  "antecedentes": [{ "type": "alergia", "description": "Ninguna conocida" }],
  "sintomas": ["ninguno"]
}
```

**Response 200 OK**
```json
{ "message": "Medical record updated successfully" }
```


> Ver más info: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#put-medical-recordupdate--actualizar-historia-cl%C3%ADnica)

---

#### `GET /medical-record/{medicalRecordId}/pdf` — Descargar historia clínica (PDF)

Genera y descarga la historia clínica completa en PDF.

```
Content-Type: application/pdf
Content-Disposition: attachment; filename=medical-record.pdf

[Archivo PDF binario]
```

> Ver más info: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-medical-recordmedicalrecordidpdf--descargar-historia-cl%C3%ADnica-pdf)

---

## 2. Sección: Control de Hemoglobina

### 2.1 Pantallas

| Pantalla | Cuándo se muestra |
|---|---|
| **Historial médico creado por primera vez** | El historial no tiene controles de hemoglobina aún → aparece el botón "Realizar primer control". |
| **Lista de pacientes (Control de Hemoglobina)** | Pantalla inicial de la sección: lista de pacientes de la cartera para seleccionar y registrar un control. |
| **Sin pacientes asignados (Control de Hemoglobina)** | El enfermero no tiene pacientes en su cartera. |
| **Falta historial médico** | Al seleccionar un paciente sin historial médico, no se puede registrar el control todavía. |
| **Nuevo control de hemoglobina** | Formulario de registro, disponible una vez que el paciente ya tiene historial médico. |
| **Card de hemoglobina (con último registro)** | Tras el primer control, muestra el valor más reciente y el botón de descargar PDF. |
| **Historial de Control de Hemoglobina** | Lista de todos los controles, con promedio, evolución, tendencia, botón de descargar y botón de añadir nuevo control. |

**Historial médico creado por primera vez:**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%203.png" width="260">
</div>

**Lista de pacientes (Control de Hemoglobina):**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Control%20de%20hemoglobina.png" width="260">
</div>

**Sin pacientes asignados (Control de Hemoglobina):**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Control%20de%20hemoglobina-sin%20pacientes.png" width="260">
</div>

**Falta historial médico:**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%2072.png" width="260">
</div>

**Nuevo control de hemoglobina:**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%204.png" width="260">
</div>

**Card de hemoglobina con último registro (+ botón descargar PDF):**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%201.png" width="260">
</div>

**Historial de Control de Hemoglobina (promedio, evolución, descargar, añadir control):**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%207.png" width="260">
</div>

**Historial de control de otro paciente (ejemplo adicional):**
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%202.png" width="260">
</div>

### 2.2 Endpoints

> Esta sección también usa `GET patients/nurse` y `GET /{patientId}/medical-record`, ya documentados en la sección 1.2.

#### `GET /{patientId}/medical-record/check`

Verifica si un paciente ya tiene una historia clínica registrada. Debe llamarse **antes de mostrar el formulario de registro de control de hemoglobina**.

- Si `hasMedicalRecord` es `false` → mostrar el frame "Falta historial médico", con un botón **"Registrar Historial Médico"** que redirige al formulario de creación (`POST /medical-record`), usando el `patientId` que devuelve este mismo endpoint.
- Si `hasMedicalRecord` es `true` → continuar al formulario de registro de control de hemoglobina.

**Response 200 OK (con historia clínica):**
```json
{
  "patientId": "0c311ed8-ac1e-43d3-ba9c-d07518c23912",
  "hasMedicalRecord": true,
  "medicalRecordId": "880e8400-e29b-41d4-a716-446655440002"
}
```

**Response 200 OK (sin historia clínica):**
```json
{
  "patientId": "0c311ed8-ac1e-43d3-ba9c-d07518c23912",
  "hasMedicalRecord": false
}
```

> Ver más info: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-patientidmedical-recordcheck--verificar-si-tiene-historia-cl%C3%ADnica)

---

#### `POST /hemoglobin-control`

Registra un control de hemoglobina. Se usa en 3 puntos distintos de la app (ver Flujos, sección 3).

**Request body:**
```json
{
  "patientId": "660e8400-e29b-41d4-a716-446655440001",
  "hemoglobinLevel": 11.2
}
```

**Response 200 OK**
```json
{ "message": "Hemoglobin control registered successfully" }
```

**Cálculo automático de anemia:**

| Resultado | Rango |
|-----------|-------|
| SEVERE    |< 7.0|
| MODERATE    |7.0 – 8.9|
| MILD    |9.0 – 10.9|
| CONTROLLED    |≥ 11.0|



**Errores 400:**

| Error                     | Causa  |
|---------------------------|--------|
| Medical record not found  |Sin historia clínica|
| Hemoglobin level must be between 0 and 30  |Nivel fuera de rango|
| Access denied: This patient is not assigned to you  |Paciente no asignado|

> Ver más info: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#post-hemoglobin-control--registrar-control-de-hemoglobina)

---

#### `GET /medical-record/{medicalRecordId}/controls`

Devuelve el historial de controles de hemoglobina de un historial médico, con promedio y evolución calculados por el backend. Se usa en el frame "Historial de Control de Hemoglobina", al que se llega desde el botón correspondiente en el card de hemoglobina.

**Response 200 OK (con datos):**
```json
{
  "patientId": "660e8400-e29b-41d4-a716-446655440001",
  "patientName": "Mateo Perez",
  "controls": [
    { "id": "...", "date": "2026-05-20T10:00:00.000Z", "hemoglobinLevel": 10.5, "anemiaStatus": "MILD" },
    { "id": "...", "date": "2026-05-22T10:00:00.000Z", "hemoglobinLevel": 11.2, "anemiaStatus": "CONTROLLED" }
  ],
  "averageHemoglobin": 10.85,
  "totalControls": 2,
  "evolution": 0.7,
  "trend": "UP"
}
```

**Response 200 OK (sin datos):**
```json
{
  "patientId": "660e8400-e29b-41d4-a716-446655440001",
  "patientName": "Mateo",
  "controls": [],
  "averageHemoglobin": 0,
  "totalControls": 0,
  "evolution": null,
  "trend": null
}
```

La tendencia se calcula como: último nivel – primer nivel
    
- UP: evolución > 0 (mejorando)
- DOWN: evolución < 0 (empeorando)
- STABLE: evolución = 0

> Ver más info: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-medical-recordmedicalrecordidcontrols--historial-de-controles)

---

#### `GET /medical-record/{medicalRecordId}/hemoglobin-report` — Reporte de hemoglobina (PDF)

Genera y descarga el reporte de evolución de hemoglobina en PDF.

```
Content-Type: application/pdf
Content-Disposition: attachment; filename=hemoglobin-report.pdf

[Archivo PDF binario]
```

> Ver más info: [Documentación backend](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-medical-recordmedicalrecordidhemoglobin-report--reporte-de-hemoglobina-pdf)

---

## 3. Flujos

### Escenario 1 — Crear, actualizar y ver el Historial Médico

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Group%20271.png" width="280">
</div>

1. Desde Home, el enfermero entra a "Historial Médico".
2. Se muestra la lista de pacientes de su cartera (`GET patients/nurse`).
3. Selecciona un paciente sin historial médico → se abre el formulario de registro (`POST /medical-record`), donde puede agregar antecedentes y síntomas mediante los modales correspondientes.
4. Una vez creado, en el card de ese paciente se habilitan los botones **"Ver"** y **"Actualizar"**.
5. **"Ver"** muestra los datos del historial (`GET /{patientId}/medical-record`); **"Actualizar"** abre el formulario de edición (`PUT /medical-record/update`).

### Escenario 2 — Primer control de hemoglobina desde un historial médico recién creado

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Group%20272.png" width="280">
</div>

1. Tras crear un historial médico por primera vez (Escenario 1), el card de hemoglobina no muestra ningún control (`hemoglobinLevel: null`, `controls: []`).
2. Se muestra el botón **"Realizar primer control"**.
3. Al presionarlo, se abre el formulario de registro de control de hemoglobina, usando el `patientId` de ese historial (`POST /hemoglobin-control`).
4. Tras registrar, el botón "Realizar primer control" desaparece y se muestra el control más reciente en el card.

### Escenario 3 — Registro de hemoglobina desde el historial de controles

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Group%20273.png" width="280">
</div>

1. Desde el historial médico, el enfermero presiona "Ver historial" en el card de hemoglobina → se abre el Historial de Controles (`GET /medical-record/{medicalRecordId}/controls`), con promedio, evolución y tendencia.
2. Presiona **"Añadir nuevo control"** → se abre el formulario de nuevo control (`POST /hemoglobin-control`).
3. El nuevo control se agrega a la lista y se recalculan promedio/evolución/tendencia.

### Escenario 4 — Registro de hemoglobina desde accesos rápidos en Home

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Group%20274.png" width="280">
</div>

1. Desde Home, el enfermero entra a "Registrar control" (accesos rápidos).
2. Se muestra la lista de pacientes de su cartera (`GET patients/nurse`).
3. Selecciona un paciente.
4. Se verifica si tiene historial médico (`GET /{patientId}/medical-record/check`):
    - Si `hasMedicalRecord` es `false` → se muestra el frame **"Falta historial médico"**, con un botón para registrar el historial de ese paciente primero (`POST /medical-record`).
    - Si `hasMedicalRecord` es `true` → se abre el formulario de registro de control (`POST /hemoglobin-control`).
5. Al registrar el control exitosamente, se muestra un frame de celebración y se vuelve a la lista de pacientes de Control de Hemoglobina.

> ⚠️ No se incluyó una captura del frame de "celebración" mencionado en este paso — falta ese asset visual eso lo haces vos dyron un frame de celbracion por el registro de un control de hemoglobina.

