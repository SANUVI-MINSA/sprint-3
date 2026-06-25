### Sebastian

#### Home

<div align ="center">
    <img src="resources\Menu-Ferova-Clinic.png">
</div>

### Ver Todas las postas

<div align="center">
<img src="resources/Historial de citas por parte del enfemero.png">
</div>

Conectar los siguientes **Endpoints**:



- **GET /appointments/nurse/top** -> Agendas de Postas

```json
{
  "success": true,
  "count": 4,
  "data": [
    {
      "appointmentId": "apt_001",
      "patientId": "pat_001",
      "patientName": "Juan Pérez Gómez",
      "facilityId": "fac_001",
      "facilityName": "Posta Médica Los Algarrobos",
      "appointmentDate": "2026-06-25",
      "appointmentTime": "09:00",
      "status": "CONFIRMED"
    },
    {
      "appointmentId": "apt_002",
      "patientId": "pat_002",
      "patientName": "María Rodríguez López",
      "facilityId": "fac_001",
      "facilityName": "Posta Médica Los Algarrobos",
      "appointmentDate": "2026-06-25",
      "appointmentTime": "11:00",
      "status": "CONFIRMED"
    },
    {
      "appointmentId": "apt_003",
      "patientId": "pat_003",
      "patientName": "Carlos García Mendez",
      "facilityId": "fac_001",
      "facilityName": "Posta Médica Los Algarrobos",
      "appointmentDate": "2026-06-26",
      "appointmentTime": "10:00",
      "status": "CONFIRMED"
    }
  ]
}
```

> Ver mas Info: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/Healthy-Facility/Health-facilities.md#15-get-appointmentsnursetop--top-citas-m%C3%A1s-pr%C3%B3ximas)

- **GET /risk-overview** -> Cuadro de Semaforo + Total de pacientes

```json
{
  "summary": {
    "HIGH":   { "count": 2, "description": "score mayor de 70" },
    "MEDIUM": { "count": 5, "description": "score entre 30 y 70" },
    "LOW":    { "count": 8, "description": "score menor de 30" },
    "total": 15
  }
}
```
> Ver mas Info: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/treatment-tracking/treatment-tracking.md#get-risk-overview--resumen-de-riesgo)

- **GET /appointments/nurse** -> Ver Todas

```json
[
  {
    "appointmentId": "uuid",
    "patientId": "uuid",
    "appointmentDate": "2026-06-10",
    "appointmentTime": "09:00",
    "status": "CONFIRMED"
  },
  {
    "appointmentId": "uuid",
    "patientId": "uuid",
    "appointmentDate": "2026-06-10",
    "appointmentTime": "11:00",
    "status": "CONFIRMED"
  }
]
```

> Ver mas Info: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/Healthy-Facility/Health-facilities.md#12-get-appointmentsnurse--horario-de-citas-de-la-enfermera)


- **GET /nurse/my-facility**

```json
{
  "success": true,
  "data": {
    "facilityName": "Posta Médica Los Algarrobos"
  }
}
```
Caso de que no tenga un posta assignado aun por parte del enfermero.

```json
{
"success": false,
"message": "No tienes una posta asignada actualmente"
}
```

> Ver mas Info: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/deployment-test/src/context/Healthy-Facility/Health-facilities.md#16-get-nursemy-facility--mi-posta-asignada)
