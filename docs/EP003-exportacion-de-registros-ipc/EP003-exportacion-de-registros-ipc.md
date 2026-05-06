# EP003 — Exportacion de registros IPC

Esta epica cubre la salida operativa de la informacion consultada en pantalla para su uso externo o revision manual.

## Definition of Ready (DoR)

- [ ] La User Story esta redactada con narrativa, precondicion y postcondicion alineadas al proceso de IPC manual.
- [ ] La User Story tiene trazabilidad explicita a su epica y a los requerimientos funcionales de origen del analisis consolidado.
- [ ] Los criterios de aceptacion estan definidos con al menos un escenario de camino feliz y uno alternativo o de error.
- [ ] El periodo funcional alcanzado por la historia esta claro, considerando que la operatoria aplica desde diciembre de 2026 en adelante.
- [ ] Las dependencias con datos provenientes de TU190, vigencia del IPC o uso en Balance AXI estan identificadas cuando correspondan.
- [ ] No existen dudas funcionales abiertas con el referente de negocio o el analista funcional para la historia a planificar.
- [ ] La historia puede ser estimada por el equipo sin requerir definiciones adicionales de alcance.

### US003001 — Exportar la grilla filtrada de IPC

**Precondicion**
El usuario ejecuto una consulta de IPC y la grilla presenta resultados segun los filtros seleccionados.

**Narrativa**
Como Usuario de Informativas quiero exportar a Excel la grilla filtrada para poder trabajar la informacion fuera del sistema.

**Postcondicion**
El sistema genera un archivo Excel con el contenido de la grilla filtrada en pantalla.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- La pantalla IPC expone la accion Exportar.
- Al accionar Exportar, el sistema genera un archivo Excel con los registros visibles en la grilla filtrada.
- El nombre del archivo exportado es "AAAAMM_IPC_SCI".
- Las columnas del archivo exportado mantienen el mismo formato y orden que la grilla en pantalla.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Exportacion exitosa de la consulta actual**
```gherkin
Given el usuario visualiza una grilla de IPC resultante de una consulta
When el usuario acciona la opcion Exportar
Then el sistema genera un archivo Excel llamado "AAAAMM_IPC_SCI"
And el archivo conserva el mismo orden y formato de columnas que la grilla
```

**Escenario 2: Exportacion sin registros visibles**
```gherkin
Given el usuario ejecuto una consulta sin resultados visibles en la grilla
When el usuario acciona la opcion Exportar
Then el sistema genera el archivo de exportacion correspondiente a la consulta aplicada
And el contenido del archivo refleja la ausencia de registros para ese filtro
```