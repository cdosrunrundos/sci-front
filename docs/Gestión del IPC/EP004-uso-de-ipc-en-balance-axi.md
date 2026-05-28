# EP004 — Uso de IPC en Balance AXI

Esta epica cubre la aplicacion del IPC vigente en el Balance AXI Actual y las restricciones funcionales cuando el balance se apoya en un IPC cargado manualmente.

## Definition of Ready (DoR)

- [ ] La User Story esta redactada con narrativa, precondicion y postcondicion alineadas al proceso de IPC manual.
- [ ] La User Story tiene trazabilidad explicita a su epica y a los requerimientos funcionales de origen del analisis consolidado.
- [ ] Los criterios de aceptacion estan definidos con al menos un escenario de camino feliz y uno alternativo o de error.
- [ ] El periodo funcional alcanzado por la historia esta claro, considerando que la operatoria aplica desde diciembre de 2026 en adelante.
- [ ] Las dependencias con datos provenientes de TU190, vigencia del IPC o uso en Balance AXI estan identificadas cuando correspondan.
- [ ] No existen dudas funcionales abiertas con el referente de negocio o el analista funcional para la historia a planificar.
- [ ] La historia puede ser estimada por el equipo sin requerir definiciones adicionales de alcance.

### US004001 — Aplicar el IPC vigente al Balance AXI Actual

**Precondicion**
Existe un Balance AXI Actual para un periodo en trabajo y existe un unico registro IPC vigente para ese periodo.

**Narrativa**
Como Usuario de Balance quiero que el sistema tome el IPC vigente del periodo para construir el Balance AXI Actual con el valor aplicable.

**Postcondicion**
El Balance AXI Actual utiliza el IPC vigente del periodo en trabajo, sea de origen manual o automatico.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- El sistema identifica el registro IPC en estado Vigente correspondiente al periodo en trabajo.
- El Balance AXI Actual utiliza ese registro IPC vigente para el trabajo preliminar del balance.
- El origen del IPC vigente puede ser manual o automatico sin alterar la seleccion del registro aplicable.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Aplicacion del IPC vigente al balance del periodo**
```gherkin
Given existe un Balance AXI Actual para un periodo en trabajo
And existe un unico IPC en estado Vigente para ese periodo
When el usuario trabaja sobre el balance actual
Then el sistema utiliza el IPC vigente del periodo
And aplica ese valor al trabajo preliminar del balance
```

**Escenario 2: Seleccion del IPC vigente independientemente del origen**
```gherkin
Given existe un IPC vigente para el periodo en trabajo
And el IPC vigente puede ser manual o automatico
When el sistema prepara el Balance AXI Actual
Then el sistema toma el registro que se encuentra vigente
And no altera la seleccion por el origen del dato
```

### US004002 — Restringir el uso de IPC manual al Balance AXI Actual del mismo mes

**Precondicion**
Existe un IPC manual vigente y el usuario trabaja sobre un Balance AXI.

**Narrativa**
Como Usuario de Balance quiero que el IPC manual solo pueda utilizarse en el Balance AXI Actual del mes informado para evitar usos fuera del alcance definido.

**Postcondicion**
El IPC manual queda habilitado solo para el Balance AXI Actual correspondiente al mismo mes del periodo del IPC.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- Un IPC manual puede utilizarse unicamente en el Balance AXI Actual.
- El sistema solo permite asociar el IPC manual al balance del mismo mes senalado por ese IPC.
- El sistema no habilita el uso del IPC manual en otros balances o periodos distintos.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Uso permitido de IPC manual en el mes correspondiente**
```gherkin
Given existe un IPC manual vigente para un periodo
When el usuario trabaja sobre el Balance AXI Actual del mismo mes
Then el sistema permite utilizar ese IPC manual en ese balance
And mantiene el uso restringido a ese contexto
```

**Escenario 2: Rechazo de uso de IPC manual fuera del alcance permitido**
```gherkin
Given existe un IPC manual vigente para un periodo
When el usuario intenta utilizarlo en otro balance o en un periodo distinto
Then el sistema no permite ese uso
And mantiene la restriccion al Balance AXI Actual del mismo mes
```

### US004003 — Impedir presentaciones con IPC manual

**Precondicion**
El Balance AXI Actual del periodo esta asociado a un IPC manual.

**Narrativa**
Como Usuario de Balance quiero que el sistema impida generar una presentacion cuando el balance usa un IPC manual para evitar presentar informacion construida con un dato provisorio.

**Postcondicion**
La presentacion no se genera y el usuario recibe un mensaje de error explicito.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- Si el Balance AXI Actual esta asociado a un IPC manual, el sistema impide generar una presentacion.
- Ante el intento de generacion, el sistema muestra el mensaje "No esta permitido generar una presentacion asociada a un IPC manual".
- Si el Balance AXI Actual utiliza un IPC automatico vigente, la restriccion anterior no aplica.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Bloqueo de presentacion con IPC manual**
```gherkin
Given el Balance AXI Actual esta asociado a un IPC manual
When el usuario intenta generar una presentacion
Then el sistema impide la generacion
And muestra el mensaje "No esta permitido generar una presentacion asociada a un IPC manual"
```

**Escenario 2: Generacion permitida con IPC no manual**
```gherkin
Given el Balance AXI Actual esta asociado a un IPC vigente no manual
When el usuario intenta generar una presentacion
Then el sistema permite continuar con la generacion
And no muestra el mensaje de restriccion por IPC manual
```