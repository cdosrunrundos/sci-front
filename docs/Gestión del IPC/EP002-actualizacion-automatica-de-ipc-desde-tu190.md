# EP002 — Actualizacion automatica de IPC desde TU190

Esta epica cubre la incorporacion automatica de registros informados por TU190 y las reglas de reemplazo de la vigencia existente para un periodo.

## Definition of Ready (DoR)

- [ ] La User Story esta redactada con narrativa, precondicion y postcondicion alineadas al proceso de IPC manual.
- [ ] La User Story tiene trazabilidad explicita a su epica y a los requerimientos funcionales de origen del analisis consolidado.
- [ ] Los criterios de aceptacion estan definidos con al menos un escenario de camino feliz y uno alternativo o de error.
- [ ] El periodo funcional alcanzado por la historia esta claro, considerando que la operatoria aplica desde diciembre de 2026 en adelante.
- [ ] Las dependencias con datos provenientes de TU190, vigencia del IPC o uso en Balance AXI estan identificadas cuando correspondan.
- [ ] No existen dudas funcionales abiertas con el referente de negocio o el analista funcional para la historia a planificar.
- [ ] La historia puede ser estimada por el equipo sin requerir definiciones adicionales de alcance.

### US002001 — Registrar IPC automatico desde TU190

**Precondicion**
El SCI recibe un nuevo valor de IPC desde la interfaz TU190 para un periodo alcanzado por la funcionalidad.

**Narrativa**
Como Responsable del proceso informativo quiero que el SCI registre automaticamente los IPC recibidos desde TU190 para evitar la carga manual cuando exista dato oficial.

**Postcondicion**
Existe un nuevo registro de IPC creado automaticamente con usuario de alta "Sistema".

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- Al recibir un nuevo IPC desde TU190, el SCI crea automaticamente un registro para el periodo informado.
- El alta automatica no requiere intervencion manual del usuario.
- El campo Usuario del registro automatico se informa con el valor "Sistema".

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Alta automatica exitosa de IPC desde TU190**
```gherkin
Given el SCI recibe un nuevo IPC desde TU190 para un periodo habilitado
When el dato es procesado por el sistema
Then el sistema crea un nuevo registro de IPC para ese periodo
And informa "Sistema" como usuario de alta
```

**Escenario 2: Recepcion de IPC para un periodo fuera del alcance funcional**
```gherkin
Given el SCI recibe un IPC para un periodo anterior a diciembre de 2026
When el dato es evaluado por la operatoria de IPC manual
Then el sistema no lo considera dentro del alcance de esta funcionalidad
And la operatoria vigente de IPC manual no se aplica sobre ese periodo
```

### US002002 — Sustituir la vigencia por un IPC de TU190

**Precondicion**
Existe un registro de IPC vigente para el periodo informado y el SCI recibe un nuevo IPC desde TU190 para ese mismo periodo.

**Narrativa**
Como Responsable del proceso informativo quiero que el IPC recibido desde TU190 pase a ser el registro vigente del periodo para que el SCI utilice el dato oficial mas reciente.

**Postcondicion**
El nuevo registro de TU190 queda en estado Vigente y el registro vigente anterior queda en estado Baja.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- Si existe un registro manual vigente para el periodo y llega un IPC desde TU190, el sistema da de baja el registro manual previo.
- Si excepcionalmente el registro vigente previo tambien fuera automatico, el nuevo registro automatico lo sustituye y el anterior queda en Baja.
- Luego de la recepcion del nuevo IPC desde TU190, solo un registro queda en estado Vigente para el periodo.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Reemplazo de registro manual vigente por IPC oficial**
```gherkin
Given existe un registro manual vigente para un periodo
And el SCI recibe un nuevo IPC desde TU190 para ese mismo periodo
When el sistema procesa el nuevo IPC
Then el registro manual previo pasa a estado Baja
And el nuevo registro de TU190 queda en estado Vigente
```

**Escenario 2: Sustitucion excepcional de automatico por automatico**
```gherkin
Given existe un registro automatico vigente para un periodo
And el SCI recibe un nuevo IPC desde TU190 para ese mismo periodo
When el sistema procesa el nuevo IPC
Then el registro automatico previo pasa a estado Baja
And el nuevo registro automatico queda como unico vigente del periodo
```