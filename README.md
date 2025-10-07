# ejercicio_opersearch

# 🧪 Ejercicio Práctico — OpenSearch con instalación local y faceted search

## 📍 Contexto
Este proyecto tiene como objetivo implementar un entorno completo de **OpenSearch** en local utilizando **Docker Compose**, realizar la **ingesta de un dataset de ejemplo**, y construir un **dashboard interactivo** con capacidades de **búsqueda facetada**.

OpenSearch es una plataforma **open source** para búsqueda y analítica de datos, derivada de Elasticsearch, que permite crear visualizaciones, análisis y dashboards sobre datos indexados.

---

## 🎯 Objetivos del ejercicio
1. Instalar y ejecutar OpenSearch y OpenSearch Dashboards en un entorno local mediante Docker Compose.  
2. Cargar un dataset de ejemplo (en este caso, `usuarios`) en un índice de OpenSearch.  
3. Crear un dashboard interactivo con visualizaciones básicas.  
4. Implementar búsqueda facetada (filtros dinámicos) para explorar los datos.

---

## 🔧 Requisitos técnicos
- **Docker** y **Docker Compose** instalados  
- **Git** para clonar o subir el proyecto  
- Acceso al puerto `9200` (OpenSearch) y `5601` (OpenSearch Dashboards)

---

## ⚙️ Instalación y ejecución

### 1️⃣ Clonar el repositorio
```bash
git clone https://github.com/AnglPinzon/opensearch_mision.git
cd opensearch_mision

Levantar los contenedores
docker-compose up -d


📍 Esto iniciará dos servicios:

opensearch (motor de búsqueda)

opensearch-dashboards (interfaz visual)

Asegúrate de que ambos estén en estado healthy (docker ps).

🗂️ Dataset de ejemplo
Creación del índice usuarios

Desde Dev Tools en OpenSearch Dashboards:

PUT usuarios
{
  "settings": { "number_of_shards": 1, "number_of_replicas": 0 },
  "mappings": {
    "properties": {
      "id": { "type": "keyword" },
      "nombre": { "type": "text" },
      "edad": { "type": "integer" },
      "ciudad": { "type": "keyword" }
    }
  }
}

Inserción de datos
POST _bulk
{ "index": { "_index": "usuarios", "_id": "1" } }
{ "id":"1","nombre":"Laura","edad":28,"ciudad":"Bogotá" }
{ "index": { "_index": "usuarios", "_id": "2" } }
{ "id":"2","nombre":"Carlos","edad":35,"ciudad":"Medellín" }
{ "index": { "_index": "usuarios", "_id": "3" } }
{ "id":"3","nombre":"Ana","edad":22,"ciudad":"Cali" }

📊 Creación de visualizaciones

Desde OpenSearch Dashboards → Dashboards → Create visualization:

1️⃣ Usuarios por ciudad (barras)

Y-axis: Count

X-axis: Terms → Field: ciudad

2️⃣ Distribución de edades (circular)

Metric: Count

Split slices: Terms → Field: edad

3️⃣ Total de usuarios (métrica)

Metric: Count

Guarda las tres visualizaciones.

🧩 Dashboard

Entra a Dashboards → Create Dashboard

Agrega las tres visualizaciones

Organízalas visualmente

Guarda el dashboard con el nombre:

Dashboard de Usuarios

🔍 Faceted Search

Para añadir búsqueda facetada (filtros dinámicos):

En el dashboard, haz clic en Add control

Elige Options list

Configura campos como:

ciudad

edad

Activa la opción de multiselect para permitir combinaciones.

🧠 Resultados esperados

✅ Entorno de OpenSearch funcionando en local.
✅ Dataset usuarios cargado exitosamente.
✅ Dashboard funcional con visualizaciones.
✅ Filtros facetados activos para navegación dinámica.

📘 Comandos útiles
Apagar los servicios
docker-compose down

Ver estado
docker ps

Ver logs
docker-compose logs -f opensearch
docker-compose logs -f opensearch-dashboards

🧩 Estructura del proyecto
opensearch_mision/
├── docker-compose.yml
├── .env
├── README.md
├── sense.json
└── dataset/
    └── usuarios.json
