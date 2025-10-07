# 🧭 Guía práctica: Exploración de datos con OpenSearch

Bienvenido 👋  
Este proyecto es una **demostración paso a paso** de cómo usar **OpenSearch** en tu computador para explorar datos y crear dashboards interactivos.  
No necesitas experiencia previa en programación o desarrollo, solo seguir las instrucciones.

---

## 🧰 Qué es OpenSearch
**OpenSearch** es una herramienta open source (gratuita) que permite buscar, visualizar y analizar información.  
Se usa en empresas para crear buscadores, reportes y paneles de datos (dashboards) en tiempo real.

En esta guía aprenderás a:
1. Encender OpenSearch en tu computador (sin instalar nada complicado).  
2. Cargar un pequeño conjunto de datos.  
3. Crear visualizaciones (gráficas y métricas).  
4. Armar un dashboard interactivo con filtros.

---

## 🚀 Empezar en 3 pasos

### 🪄 Paso 1: Encender OpenSearch

1. Abre tu **terminal** dentro de la carpeta del proyecto:
   ```bash
   cd opensearch_mision
Enciende el entorno con:

bash
Copiar código
docker-compose up -d
Espera unos segundos hasta que ambos servicios estén "healthy":

bash
Copiar código
docker ps
✅ Cuando todo esté listo:

OpenSearch corre en: https://localhost:9200

OpenSearch Dashboards (interfaz visual) corre en:
👉 http://localhost:5601

🧾 Paso 2: Cargar los datos
Entra al panel de OpenSearch Dashboards:

arduino
Copiar código
http://localhost:5601
En el menú lateral selecciona Dev Tools.

Copia y pega el siguiente bloque (luego presiona el botón ▶ para ejecutarlo):

json
Copiar código
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

POST _bulk
{ "index": { "_index": "usuarios", "_id": "1" } }
{ "id":"1","nombre":"Laura","edad":28,"ciudad":"Bogotá" }
{ "index": { "_index": "usuarios", "_id": "2" } }
{ "id":"2","nombre":"Carlos","edad":35,"ciudad":"Medellín" }
{ "index": { "_index": "usuarios", "_id": "3" } }
{ "id":"3","nombre":"Ana","edad":22,"ciudad":"Cali" }

POST usuarios/_refresh
GET usuarios/_count
Si todo sale bien, verás algo como:

json
Copiar código
{
  "count": 3,
  "_shards": { "total": 1, "successful": 1 }
}
📊 Paso 3: Crear tus visualizaciones
En el menú lateral, entra a Dashboards → Create visualization.

Escoge el tipo de gráfico que quieras:

Bar chart → para ver usuarios por ciudad

Pie chart → para ver la distribución por edad

Metric → para mostrar el número total de usuarios

Cada vez que crees una visualización, guarda con un nombre, por ejemplo:

Usuarios por ciudad

Distribución de edades

Total de usuarios

🧩 Paso 4: Construir tu dashboard
Entra a Dashboards → Create dashboard

Haz clic en Add visualization

Agrega las tres visualizaciones anteriores.

Organízalas como quieras y guarda el dashboard con el nombre:

nginx
Copiar código
Dashboard de Usuarios
Listo ✅
Ya puedes interactuar con los datos, ver cuántos usuarios hay por ciudad o edad, y filtrar de forma dinámica.

🔍 Añadir filtros (búsqueda facetada)
Dentro de tu dashboard, haz clic en Add control.

Elige Options list.

En Field, selecciona ciudad o edad.

Activa la opción Allow multiple selections.

Guarda el dashboard otra vez.

Ahora podrás filtrar tus gráficos por ciudad o edad sin escribir consultas.

🧠 Qué aprendiste
✔ Cómo encender OpenSearch localmente con Docker
✔ Cómo cargar datos y crear un índice
✔ Cómo visualizar información con gráficas
✔ Cómo crear un dashboard con filtros facetados

🧹 Para apagar el entorno
Cuando termines:

bash
Copiar código
docker-compose down
Y si quieres volver a iniciarlo:

bash
Copiar código
docker-compose up -d
