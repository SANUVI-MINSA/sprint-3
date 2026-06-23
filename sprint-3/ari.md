### Ariana

#### Seccion de Comunicacion + Chat

> se redirecciona a este frame cuando seleciona en el nav inferior la opcion de consultas

<div align="center">
    <img src="resources/communication/Bandeja de Consultas.png">
</div>


> el chat se abre cuando seleciono un card de la bandeja de consultas

<div align="center">
    <img src="resources/communication/chat.png">
</div>

> Modal para decidir si el enfermero quiere cerrar una consulta (ocurre al momento de presionar el btn de cerrar)

<div align ="center">
<img src="resources/communication/modal-decision-cerrar.png">
</div>


#### Frame sin Consultas

> caso de que el enfermero no tiene una consulta de las madres de un paciente en la bandeja de consultas

<div aling ="center">
<img src="resources/communication/Sin Consultas.png">
</div>

#### Frame de Sin Pacientes

> caso de que el enfermero no tiene enfermeros en su cartera

<div align ="center">
<img src="resources/communication/Sin pacientes asignados 0.png">
</div>

#### Frame Sin Resultados de Busqueda

<div align ="center">
<img src="resources/communication/Sin resultados de Busqueda.png">
</div>


Conectar los siguientes **Endpoints**:


- **GET /communication/consultations/nurse?searchTerm=**

**Escenario 1: Con consultas activas**

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

**Escenario 2: Tiene pacientes asignados pero NO tiene consultas activas** -> Mostrar frame de Sin Consultas

```json
{
    "consultations": [],
    "message": "No tienes consultas activas aún",
    "detail": "Las madres pueden iniciar consultas para sus hijos. Cuando una madre inicie una consulta, aparecerá aquí.",
    "status": "NO_CONSULTAS"
}
```

**Escenario 3: NO tiene pacientes asignados en su cartera** -> Mostrar Frame de Sin Pacientes

```json
{
    "consultations": [],
    "message": "No tienes pacientes asignados en tu cartera",
    "detail": "Puedes asignar pacientes a tu cartera desde el módulo de pacientes. Ve a 'Pacientes' y selecciona 'Asignar a mi cartera'.",
    "action": "Asignar pacientes",
    "status": "SIN_PACIENTES"
}
```

**Escenario 4: Búsqueda sin resultados** -> Mostrar Frame de Sin resultados de busqueda

```json
{
    "consultations": [],
    "message": "No se encontraron consultas que coincidan con tu búsqueda",
    "detail": "No hay consultas con \"Carlos\" en el nombre del paciente o de la madre. Intenta con otro término.",
    "searchTerm": "Carlos",
    "status": "BUSQUEDA_SIN_RESULTADOS"
}
```

> Ver mas: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/deployment-test/src/context/comunication-management/Documentacion.md#8-obtener-consultas-activas-de-una-enfermera-bandeja-de-consultas)



- **POST /messages**

Envía un mensaje dentro de una teleconsulta activa.


```json
{
    "consultationId": "string",
    "senderId": "string",
    "senderRole": "MOTHER | NURSE",
    "content": "string"
}
```
> Ver mas: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/comunication-management/Documentacion.md#2-enviar-mensaje-madre-o-enfermera)


- **GET /chat/:consultationId**

Abri chat cuando seleciono una consulta desde la bandeja de consultas

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

> Ver mas: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/comunication-management/Documentacion.md#6-obtener-chat-de-consulta-madre-o-enfermera)


### Seccion Pacientes

Busqueda de la madre por dni


<div align="center">
<img src="resources/patient/Pacientes-Serch.png">
</div>

### Pacientes de la Madre

<div align="center">
<img src="resources/patient/Pacientes registados por la madre.png">
</div>


<div align="center">
<img src="resources/patient/Pacientes registados por la madre-1.png">
</div>

### Caso que la madre no tenga pacientes

<div align="center">
<img src="resources/patient/CASO QUE NO HAY PACIENTES REGISTRADOS POR LA MADRE.png">
</div>

### Caso que cuando presiona el btn de presionar (asignar a mi cartera a un paciente) y dicho enfermero que lo ejecuta no tiene una posta assignada en ella.

<div align="center">
<img src="resources/patient/Group 205.png">
</div>

Conectar los siguientes **Endpoints**:


- **GET /mother/search/{dni}**

```json
{
  "motherId": "550e8400-...",
  "fullName": "Diana Carrillo",
  "dni": "12345678"
}
```
> Ver mas [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-mothersearchdni--buscar-madre-por-dni)

- **GET /mother/{motherId}**

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


> Ver mas [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-mothermotherid--listar-pacientes-por-madre)


- **POST /assign-nurse**


**Request body:**

```json
{ "patientId": "660e8400-e29b-41d4-a716-446655440001" }

```

**Response 200 Ok**

```json
{ "message": "Patient assigned successfully" }
```

**Error 404**

```json
{ "message": "Nurse is not assigned to any facility" }
```


> Ver mas [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#post-assign-nurse--asignarse-un-paciente)

