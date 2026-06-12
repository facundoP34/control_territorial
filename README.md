# 🌎 Control Territorial / Barrido Comercial
Proyecto para empresa de consumo masivo

# 📌 Contexto del Proyecto
Importante compañía multinacional apuesta a mejorar su capilaridad en la ciudad de Córdoba, conjunto a eficientizar su diseño logístico.

# 📌 Problema Que Resuelve
Problema de subcobertura, la compañía maneja un padrón de clientes desactualizado y desconoce los cambios en el tejido comercial de los últimos años. Por tanto, está perdiendo potenciales clientes.

# 🎯 Business Questions
* ¿Cuál es el Market Share actual en la zona de interés? 
* ¿Estamos atendiendo a la totalidad de los PDV objetivo? 
* ¿Cuántos PDV activos no registrados hay en la zona de interés? 
* ¿Cuál es el potencial de ventas incremental de aumentar la cuota de mercado?

# 🧰 Tech Stack
  * Lenguajes: Python (librerías: pandas, requests)
  * Análisis Geoespacial: QGIS
  * APIs: Google Maps API (Nearby Search, Place Details y Text Search), OpenStreetMap (`Overpass API`)
    
# 🏗️  Arquitectura
Para economizar el costo del proyecto, pero sin que esto degrade la extracción de datos, primero recurrí a OSM, una fuente abierta. Esto permite localizar las zonas de mayor densidad comercial. Este punto fue clave para definir una matriz de extracción a medida del área de observación que no deje afuera a PDV de interés ya sea por quedar entre vacíos de los radios de observación o por saturación de PDV en la zona.

# 🏗️  Pipeline de Datos
* Extracción: El algoritmo recorre la matriz predefinida. Para cada radio/área, ejecuta las consultas a los endpoints de Google Maps, gestionando de forma automática la paginación (`next_page_token`).
* Transformación y Desduplicación: con **Python (Pandas)**, el sistema procesa las respuestas en JSON, normaliza los campos de dirección/coordenadas y aplica una lógica de desduplicación para eliminar solapamientos generados por la cercanía de los radios de búsqueda.
* El resultado final es una **matriz de datos estandarizada y georreferenciada**, lista para ser integrada en el sistemas de información geográfica (QGIS).

# ✅ Conclusión
