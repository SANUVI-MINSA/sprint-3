### Dyron

#### Seccion de Historial - Añadir Control de Hemoglobina

> Mira en la seccion de historial se obtiene una lista de pacientes asignados a la cartera por parte del enfermero que
> lo fue asignado en la seccion pacientes (que lo esta haciendo ariana)

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Selecionar%20Paciente%20Historial%20Medico.png">
</div>

> Seccion de Historial de medico con btn de ver y actualizar
> estos btn se habilitan cuando ya se registo un historial medico por parte del enfermero a un paciente. 

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Selecionar%20Paciente%20Historial%20Medico%20(1).png">
</div>

> Frame sin pacientes asignados
> Se muestra en la seccion de historial medico el cual se mostrar si el enfermo no asigno a un paciente a su cartera
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Selecionar%20Paciente%20Historial%20Medico%203.png">
</div>

> Frame de sin pacientes assignadosen en la cartera en control de hemoglobina
> Se muestra si no hay pacientes assignados por parte del enfermero en su cartera

<div  align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Control%20de%20hemoglobina-sin%20pacientes.png">
</div>

> Frame de actualizar
> Se muestra el frame de actualizar un historial medico, por parte del enfermero el cual se seleciona por el btn de actualizar de un card de la lista de pacientes en la seccion de historial medico.

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Actualizar.png">
</div>

> Registrar Historial medico del paciente selecionado de la lista pacientes asignados a la cartera por parte del enfermero

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Mateo-Historial%20Medico.png">
</div>

> Modal para el registo de Antecedentes
> Este modal es para registrar 

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Background+Border+Shadow%20(1).png">
</div>

> Modal Para el registro de sintomas
> Este modal es para registrar sintomas en el historial medico

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Background+Border+Shadow.png">
</div>

> Frame de Historial medico creado por primera vez
> (Si es creado por primera vez no tiene registro de controles de hemoglobina el cual se da presencia de dicho btn en si)

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%203.png">
</div>

> Frame de Control de Hemoglobina
> Primer frame de lista de pacientes asignados a la cartera del paciente en el contro de hemoglobina para selecionar el paciente y registrar el contro de hemoglobina

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Control%20de%20hemoglobina.png">
</div>

> Frame de Falta de Historial medico
> al momento de selecionar al paciente de la lista de contro de hemoglobina (que es la lista de pacientes que estan en la cartera del enfermero),
> si uno no tiene un historial medico no se le podra registrar el contro de hemoglobina
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%2072.png">
</div>

> Frame de Nuevo Control o Registo de Control de hemoglobina
> Aca una vez de que el paciente tenga un historial medico, se permitira a registra el control de hemoglobina y no se mostrara el frame de falta historial medico

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%204.png">
</div>

> una vez registrado la hemoglobina ya se por primera vez desde el historial medico o en la seccion home en accesos rapidos en el btn de **registrar control**
> se vera el ultimo registro de hemoglobina reciente en si en el card de hemoglobina el cual tambien desaperece el btn de realizar primer control, por que ya se registro el primer control.
> se ver el btn de descargar el cual permite descargar el historial medico en pdf

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%201.png">
</div>

> Historial de Control de Hemoglobina
> En este frame se ve el historial de controles de hemoglobina, viendo el promedio, la evolucion en si datos calculados del backend,
> esta el btn de descargar el cual tambien descargar el historial de control de hemoglobina, tambien esta el btn de añadir un nuevo control
> el cual nos redireciona al frame de Nuevo Control o Registo de Control de hemoglobina, el cual registramos un nuevo control de hemoglobina en si.

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%207.png">
</div>

> Historial de contol de hemoglobina
> Muestra de otros historiales registrados

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/iPhone%2017%20-%202.png">
</div>

**Endpoints para conectar**

- **GET patients/nurse**

este endpoints lista los pacientes en la cartera del enfermero, se utilizara en los frames de
la seccion de historial medico y control de hemoglobina para selecionar al paciente para registrar un historial medico o un registro de control de hemoglobina a un paciente.

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

caso de que hay un arreglo vacion mostrar el frame de si pacientes assignados y con el btn de assignar pacientes que redirreciona a la seccion pacientes para asignar a un paciente a la cartera de un enfermero
tando en la seccion de historial medico como el control de hemoglobina

```json
  []
```
> Ver mas info: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-nurse--listar-pacientes-asignados)

- **POST /medical-record**

endpoint para crear el historial medico de un paciente selecionado del **patients/nurse**

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
**Response 201 Created:**

caso de que fue creado un historial medico mostrar los btons desde la lista pacientes asignados por el enfermero **patients/nurse**
los btns de ver historial y actualizar

```json
{ "message": "Medical record created successfully" }
```

> Ver mas info [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#post-medical-record--crear-historia-cl%C3%ADnica)


- **GET /{patientId}/medical-record** 

este endpoint devuelve los datos del paciente el historial clinico y lo contoles en si
justamente es para el historial medico de un paciente en si.

<br>
<br>

en el json te deje un <- Importante, es para que cuando crees por primera vez un registro de control de hemoglobina.
(recuerda la imagen de Frame de Historial medico creado por primera vez el cual en el card de hemoglobina esta el btn de realizar primer control que redireciona al frame de registrar el control de hemoglobina del paciente de dicho historial medico y para esa redireccion de dicho paciente puedes utilizar el **patientId** para registrar el control de hemoglobina de dicho paciente de historial medico)

> bueno tambien el registro de control de hemoglobina puede hacerlo desde home en la parte de acceso rapidos en la opcion registrar control

```json
{
  "patient": {
    "id": "072a086a-68c4-4952-bbf8-0362d23d3a22", <- usar para la redireecion
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
    "hemoglobinLevel": null, -> Importante
    "weight": 12.5,
    "height": 85,
    "gender": "MALE",
    "antecedentes": [
      {
        "type": "alergia",
        "description": "Penicilina"
      }
    ],
    "motivoConsulta": "Control de rutina",
    "observaciones": "Paciente en buen estado general",
    "controls": [], -> Importante
    "patientId": "072a086a-68c4-4952-bbf8-0362d23d3a22",
    "nurseId": "6a22a5f92b5b07eee90589aa",
    "sintomas": [
      "fiebre",
      "tos"
    ]
  }
}
```

una vez que ya se registro un control de hemoglobina (con el endpoint de acontinuacion que vamos hablar),  
no se mostrara el btn de registrar primer control ya que tendremos controles de hemoglobina y se mostrar el control mas reciente con el **hemoglobinLevel** y un btn de ver historial (que se explicare mas adelante el documento) en el card.
(mirar el frame que se mostro en las imagenes de arriba)

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
    "hemoglobinLevel": 20, <- Importante
    "weight": 12.5,
    "height": 85,
    "gender": "FEMALE",
    "antecedentes": [
      {
        "type": "alergia",
        "description": "Penicilina"
      }
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
    ], <- Importante
    "patientId": "0c311ed8-ac1e-43d3-ba9c-d07518c23912",
    "nurseId": "6a22a5f92b5b07eee90589aa",
    "sintomas": [
      "fiebre",
      "tos"
    ]
  }
}
```

> Ver mas info [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-patientidmedical-record--historia-cl%C3%ADnica-completa)

- **PUT /medical-record/update**

Este endpoint actualiza el historial medico recuerdas el btn que se habilita cuando se crea un historial medico o se registra.
Pues de dicho historial del paciente podemos actualizarlo y podemos ver los datos actualizados con el endpoint de **/{patientId}/medical-record**

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
### Response 200 OK:

```json
{ "message": "Medical record updated successfully" }
```

> Ver mas info [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#put-medical-recordupdate--actualizar-historia-cl%C3%ADnica)

- **POST /hemoglobin-control**

Este endpoint se encarga del registro de control de hemoglobina el cual se da de 3 maneras que los podras ver en el flujo (Observar los flujos).

```json
{
  "patientId": "660e8400-e29b-41d4-a716-446655440001",
  "hemoglobinLevel": 11.2
}
```

### Response 200 OK:

```json
{ "message": "Hemoglobin control registered successfully" }
```

> Ver mas info [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#post-hemoglobin-control--registrar-control-de-hemoglobina)


- **GET /medical-record/{medicalRecordId}/controls**

Este endpoint es pare ver el historial de controles de hemoglobina de un historial medico
el cual en el frame donde se ve el historial medica ya habiendo dado el primer control, registro el control desde home en registrar control en acceso rapidos o en el mismo historial de control de hemoglobina cuando se presiona el btn de añadir nuevo control. 
es en el frame donde vemos el historial medico en el card de hemoglobina hay un btn que redirreciona al historial el cual se puede ver dicho historial medico con el promedio y evolucion.

#### Response 200 OK (con datos):


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

#### Response 200 OK (sin datos):

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

> Ver mas info: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-medical-recordmedicalrecordidcontrols--historial-de-controles)

- **GET /{patientId}/medical-record/check**

> Verifica si un paciente ya tiene una historia clínica registrada. Este endpoint es útil para validar si se puede registrar un control de hemoglobina.
> Este endpoint debe llamarse antes de mostrar el formulario de registro de hemoglobina. Si hasMedicalRecord es false, se debe mostrar un mensaje indicando que primero debe crearse el historia clínico del paciente seleccionado 
> y pues aparecera un btn de **Registrar Historial Medico** que lo redirreciona al formulario de registrar historial medico del paciente que se seleciono (te puedes ayudar del id del paciente que se obtiene de este endpoint)

#### Response 200 OK (con historia clínica):

```json
{
  "patientId": "0c311ed8-ac1e-43d3-ba9c-d07518c23912",
  "hasMedicalRecord": true,
  "medicalRecordId": "880e8400-e29b-41d4-a716-446655440002"
}
```

#### Response 200 OK (sin historia clínica):

```json
{
  "patientId": "0c311ed8-ac1e-43d3-ba9c-d07518c23912",
  "hasMedicalRecord": false
}
```

> Ver mas info: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-patientidmedical-recordcheck--verificar-si-tiene-historia-cl%C3%ADnica)

- **GET /medical-record/{medicalRecordId}/pdf** — Descargar historia clínica (PDF)

> Genera y descarga la historia clínica completa en PDF.

#### Response 200 OK 

```
Content-Type: application/pdf
Content-Disposition: attachment; filename=medical-record.pdf

[Archivo PDF binario]
```

> Ver mas info: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-medical-recordmedicalrecordidpdf--descargar-historia-cl%C3%ADnica-pdf)

- **GET /medical-record/{medicalRecordId}/hemoglobin-report** — Reporte de hemoglobina (PDF)

> Genera y descarga el reporte de evolución de hemoglobina en PDF.

#### Response 200 OK

```
Content-Type: application/pdf
Content-Disposition: attachment; filename=hemoglobin-report.pdf

[Archivo PDF binario]
```
> Ver mas info: [Link](https://github.com/SANUVI-MINSA/backend-ferova/blob/develop/src/context/patient-management/Documentation.md#get-medical-recordmedicalrecordidhemoglobin-report--reporte-de-hemoglobina-pdf)

#### Flujos UX

##### Scenario 1: Crear, Actualizar y Ver Historial Medico

> Este flujo representa la creacion actualizacion y observacion
> Desde Home navegamos a historial medico en el nos da la lista de pacientes que estan en la cartera del medico
> Seleciona un paciente del historial y me lleva al registro de un historial medico una vez creado
> se activa dos btns el cual nos permite ver la creacion del registro de historial medico.
> y actualizacion de un historial medico del paciente selecionado en si.

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Group%20271.png">
</div>

##### Scenario 2: Registro de primer control de hemoglobina desde historial medico creado por primera vez

> Registrar o añadir un control de hemoglobina por primera vez de un historial medico recien creado

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Group%20272.png">
</div>

#### Scenario 3: Registro de hemoglobina desde el historial de controles de hemgolbina

> Registrar desde el historial medico un nuevo control
>

<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Group%20273.png">
</div>

#### Scenario 4: Registro de hemoglobina desde los accesos rapidos desde el home
> Desde home en accesos podemos registrar un control de hemoglobina a un pacientes
> de nuestra lista de pacientes assignados selecionamos uno y nos permitira registrar
> un control de hemoglobina al paciente selecionado, y se presenta un frame de celebracion
> y volvemos a la lista de pacientes de la cartera del enfermero de la seccion de control de hemoglobina.
> 
> Caso contrario de que al momento de seleccionar dicho paciente no tiene un historial medico aparece el frame
> de que falta un historial medico para ese paciente que selecionamos con un btn d registrar
> el historial medico de dicho paciente.
<div align="center">
<img src="resources/historial-medico-control-de-hemoglobina/Group%20274.png">
</div>
