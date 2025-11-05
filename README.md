# 🤖 aiPropertySearch

**Búsqueda de propiedades con IA - Habla, no codifiques**

Sistema inteligente que traduce consultas en lenguaje natural a SQL. Busca propiedades como hablas, sin necesidad de conocer SQL ni sintaxis de bases de datos.

```
"Casas de 3 habitaciones en zona 10" → SQL generado automáticamente → Resultados
```

## 📂 Repositorios del Proyecto

| Componente | Repositorio |
|-----------|-------------|
| **Orquestación (Este)** | [aiPropertySearch](https://github.com/FrankOrozcoGT/aiPropertySearch) |
| **Backend (FastAPI + Ollama)** | [aiPropertySearch-backend](https://github.com/FrankOrozcoGT/aiPropertySearch-backend) |
| **Frontend (Vue.js 3)** | [aiPropertySearch-frontend](https://github.com/FrankOrozcoGT/aiPropertySearch-frontend) |


## ✨ Características Principales

- 🤖 **IA Integrada**: Ollama LLM traduce lenguaje natural a SQL
- 🛡️ **100% Seguro**: SQL injection imposible con parámetros separados
- 🔍 **Búsqueda Inteligente**: Entiende consultas complejas en lenguaje natural
- 💻 **UI Moderna**: Vue.js 3 + TailwindCSS
- ⚡ **Ultra Rápido**: FastAPI asincrónico + Vite
- 🐳 **Docker Ready**: Levanta todo con un comando
- 📊 **SQL Transparente**: Visualiza las consultas generadas
- 📚 **Documentación Automática**: Swagger + ReDoc

## 📦 Stack Tecnológico Completo

### Backend
- **FastAPI** - Framework web asincrónico
- **Python 3.11+** - Lenguaje principal
- **Ollama** - LLM local para NLP
- **MySQL 8.0+** - Base de datos normalizada
- **SQLAlchemy** - Validación de SQL
- **Uvicorn** - ASGI server

### Frontend
- **Vue.js 3** - Framework JavaScript
- **Vite** - Build tool ultrarrápido
- **TailwindCSS** - Utilidades CSS
- **TypeScript** - Type safety
- **Nginx** - Servidor web (producción)

### DevOps
- **Docker** - Contenedorización
- **Docker Compose** - Orquestación
- **MySQL** - Base de datos
- **Ollama** - LLM local

## 📋 Estructura del Proyecto

```
aiPropertySearch/
├── backend/                         # API FastAPI + Ollama
│   ├── app/
│   │   ├── domain/                 # Lógica de negocio (Hexagonal)
│   │   ├── infrastructure/         # Adaptadores (LLM, DB)
│   │   ├── presentation/           # Rutas HTTP
│   │   └── main.py                 # FastAPI app
│   ├── persistencia/
│   │   ├── schema.sql              # Estructura BD
│   │   └── seed_data.sql           # Datos de ejemplo
│   ├── requirements.txt
│   ├── Dockerfile
│   └── README.md
│
├── frontend/                        # UI Vue.js 3
│   ├── src/
│   │   ├── application/            # Use cases
│   │   ├── domain/                 # Modelos de negocio
│   │   ├── infrastructure/         # Adaptadores HTTP
│   │   ├── presentation/           # Componentes Vue
│   │   └── App.vue
│   ├── Dockerfile
│   ├── package.json
│   ├── vite.config.js
│   └── README.md
│
├── docker/
│   ├── Dockerfile.ollama           # Imagen Ollama personalizada
│   └── ollama-init.sh
│
├── docker-compose.yml              # Orquestación completa
├── OLLAMA_SETUP.md                 # Guía de Ollama
└── README.md                       # Este archivo
```

## 🚀 Inicio Rápido

### Opción 1: Docker Compose (Recomendado - 30 segundos)

```bash
# Clonar repositorio
git clone https://github.com/FrankOrozcoGT/aiPropertySearch-backend.git
cd aiPropertySearch-backend

# Levantar todo
docker-compose up -d

# Verificar servicios
docker-compose ps
```

**Acceso:**
- Frontend: http://localhost
- Backend API: http://localhost:8000
- API Docs: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

### Opción 2: Instalación Local

Ver READMEs específicos:
- [Backend](./backend/README.md) - Instrucciones Python + FastAPI
- [Frontend](./frontend/README.md) - Instrucciones Node.js + Vue

## 📖 Requisitos

### Para Docker (Recomendado)
- **Docker** 20.10+
- **Docker Compose** 2.0+

### Para Local
- **Python** 3.11+ (backend)
- **Node.js** 18+ (frontend)
- **MySQL** 8.0+
- **Ollama** (para LLM)

## 🎯 Ejemplos de Búsqueda

Prueba estas consultas en la aplicación:

```
"Casas de 3 habitaciones en zona 10"
```
✅ Busca casas | ✅ Filtra por habitaciones | ✅ Ubicación específica

```
"Departamentos baratos menores a Q100,000"
```
✅ Filtra por tipo | ✅ Precio máximo especificado

```
"Propiedades cerca de colegio y parque"
```
✅ Busca amenidades | ✅ Distancia cercana

```
"Terrenos grandes en zona 18"
```
✅ Filtra por área | ✅ Zona específica

```
"Oficinas con 2 baños"
```
✅ Tipo específico | ✅ Número de baños

## 📝 Instalación Paso a Paso

### 1. Clonar Repositorios

```bash
# Backend + Frontend
git clone https://github.com/FrankOrozcoGT/aiPropertySearch-backend.git
cd aiPropertySearch-backend

# Frontend (si necesitas acceso separado)
git clone https://github.com/FrankOrozcoGT/aiPropertySearch-frontend.git
```

### 2. Configurar Variables de Entorno

**Backend (.env):**
```env
DB_HOST=db
DB_PORT=3306
DB_USER=root
DB_PASSWORD=password
DB_NAME=propiedades
OLLAMA_URL=http://ollama:11434
OLLAMA_MODEL=mistral
API_PREFIX=/api/v1
```

**Frontend (.env.local):**
```env
VITE_API_URL=http://localhost:8000
VITE_API_PREFIX=/api/v1
```

### 3. Iniciar Servicios

#### Con Docker Compose (TODO en UNO)
```bash
docker-compose up -d
```

#### Sin Docker (Servicios Separados)

**Terminal 1 - Backend:**
```bash
cd backend
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
uvicorn app.main:app --reload
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm install
npm run dev
```

**Terminal 3 - Servicios:**
```bash
# MySQL
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password mysql:8.0

# Ollama
docker run -d -p 11434:11434 ollama/ollama
ollama pull mistral
```

### 4. Importar Datos

```bash
# Con Docker
docker exec -i proyecto_guate_db mysql -u root -ppassword propiedades < backend/persistencia/schema.sql
docker exec -i proyecto_guate_db mysql -u root -ppassword propiedades < backend/persistencia/seed_data.sql

# Sin Docker
mysql -u root -p propiedades < backend/persistencia/schema.sql
mysql -u root -p propiedades < backend/persistencia/seed_data.sql
```

### 5. Acceder a la Aplicación

- **Frontend:** http://localhost:5173 (local) o http://localhost (Docker)
- **Backend API:** http://localhost:8000
- **API Docs:** http://localhost:8000/docs
- **ReDoc:** http://localhost:8000/redoc

## 🏗️ Arquitectura General

```
┌─────────────────────────────────────────────────────┐
│                  Frontend (Vue.js)                  │
│            http://localhost:5173                    │
└────────────────────┬────────────────────────────────┘
                     │ HTTP (JSON)
                     │
┌────────────────────▼────────────────────────────────┐
│              Backend API (FastAPI)                  │
│            http://localhost:8000                    │
│  ┌──────────────────────────────────────────────┐   │
│  │ /api/v1/search → Natural Language Query      │   │
│  └──────────────┬──────────────────────────────┘   │
└─────────────────┼────────────────────────────────────┘
                  │
         ┌────────┴───────┐
         │                │
    ┌────▼────┐      ┌────▼────┐
    │  Ollama  │      │  MySQL   │
    │   LLM    │      │   BD     │
    └──────────┘      └──────────┘
```

## 🛡️ Seguridad

### SQL Injection - PROTEGIDO ✅

```python
# ✅ SEGURO: Parámetros separados
sql = "SELECT * FROM propiedades WHERE precio < %s"
params = [100000]
db.execute(sql, params)

# ❌ INSEGURO: Interpolación (NO USAR)
sql = f"SELECT * FROM propiedades WHERE precio < {user_input}"
```

**Protecciones:**
1. Parámetros separados del SQL
2. Validación con SQLAlchemy
3. Palabras clave bloqueadas (DROP, DELETE, UPDATE, etc.)
4. Placeholders MySQL con escape automático

## 🐳 Gestión de Docker

### Ver estado

```bash
docker-compose ps
```

### Ver logs

```bash
# Todos los servicios
docker-compose logs -f

# Solo backend
docker-compose logs -f backend

# Solo frontend
docker-compose logs -f frontend

# Solo BD
docker-compose logs -f db
```

### Reiniciar servicios

```bash
# Todos
docker-compose restart

# Específico
docker-compose restart backend
```

### Parar y eliminar

```bash
# Parar
docker-compose down

# Parar y eliminar volúmenes (CUIDADO: pierde datos)
docker-compose down -v
```

## 🔍 Solución de Problemas

### Backend no inicia

```bash
# Ver logs de error
docker-compose logs backend

# Verificar Puerto 8000
lsof -i :8000

# Reiniciar
docker-compose restart backend
```

### Frontend no conecta

```bash
# Verificar Backend está corriendo
curl http://localhost:8000/health

# Revisar consola del navegador (F12)
# Verificar URL en .env.local
```

### BD no tiene datos

```bash
# Reimportar schema y seed
docker-compose exec db mysql -u root -ppassword propiedades < backend/persistencia/schema.sql
docker-compose exec db mysql -u root -ppassword propiedades < backend/persistencia/seed_data.sql
```

### Ollama no conecta

```bash
# Verificar Ollama está corriendo
curl http://localhost:11434

# Ver logs
docker-compose logs ollama

# Descargar modelo
docker-compose exec ollama ollama pull mistral
```

## 📚 Documentación Completa

- **Backend:** Ver [backend/README.md](./backend/README.md)
- **Frontend:** Ver [frontend/README.md](./frontend/README.md)
- **Ollama Setup:** Ver [OLLAMA_SETUP.md](./OLLAMA_SETUP.md)
- **API Docs:** http://localhost:8000/docs (Swagger)
- **Architecture:** Ver [backend/ARCHITECTURE.md](./backend/ARCHITECTURE.md)
- **Secuencias:** Ver [backend/SEQUENCE_DIAGRAM.md](./backend/SEQUENCE_DIAGRAM.md)

## 🚀 Despliegue en Producción

```bash
# 1. Configurar .env para producción
cp .env.example .env
# Editar con valores de producción

# 2. Build de imágenes
docker-compose build --no-cache

# 3. Levantar en background
docker-compose up -d

# 4. Verificar salud
curl http://tu-dominio/health
curl http://tu-dominio:8000/health
```

## 🤝 Contribuir

1. Fork el repositorio
2. Crear rama: `git checkout -b feature/nueva-funcionalidad`
3. Hacer cambios
4. Commit: `git commit -am 'Add nueva-funcionalidad'`
5. Push: `git push origin feature/nueva-funcionalidad`
6. Pull request

## 📄 Licencia

MIT

## 🆘 Contacto

**Autor:** Frank Orozco  
**Email:** frank.orozco.11.87@gmail.com  
**GitHub:** [@FrankOrozcoGT](https://github.com/FrankOrozcoGT)

## 📍 Repositorios

- **Backend:** https://github.com/FrankOrozcoGT/aiPropertySearch-backend
- **Frontend:** https://github.com/FrankOrozcoGT/aiPropertySearch-frontend
- **video:** https://youtu.be/9FHBESj1Yfk

---

**Estado:** ✅ Funcional | En desarrollo activo  
**Última actualización:** Noviembre 2025  
**Versión:** 1.0.0
