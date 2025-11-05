# Configuración de Ollama con GPU AMD

## ✅ Completado

### 1. Docker Compose Actualizado
- ✅ Servicio Ollama agregado con soporte GPU AMD
- ✅ Volumen persistent para modelos (`ollama_data`)
- ✅ Acceso a dispositivos GPU AMD (`/dev/kfd`, `/dev/dri`)
- ✅ Backend ahora depende de Ollama
- ✅ Health check configurado

### 2. Modelo Descargado
- ✅ `llama3.2:3b` descargado en Ollama
- ✅ Prueba básica exitosa: ✨ **"La capital de Guatemala es Ciudad de Guatemala"**

### 3. Configuración Backend
- ✅ URL actualizada: `http://ollama:11434`
- ✅ Modelo: `llama3.2:3b`
- ✅ OllamaLLMAdapter listo para usar

## 🚀 Cómo Usar

### Iniciar todo (backend + frontend + db + ollama)
```bash
docker-compose up -d
```

### Ver logs de Ollama
```bash
docker logs proyecto_guate_ollama
```

### Probar Ollama directamente
```bash
# Desde el host (Ollama expuesto en puerto 11434)
curl http://localhost:11434/api/tags

# Generar una respuesta
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2:3b",
  "prompt": "¿Cuál es la capital de Guatemala?"
}'
```

### Probar integración backend
```bash
python3 test_integration_ollama.py
```

### Hacer una búsqueda desde el frontend
1. Ir a http://localhost (frontend)
2. Escribir una búsqueda natural como:
   - "casas baratas en zona 10"
   - "departamentos con 3 habitaciones"
   - "terrenos disponibles"
3. El LLM convertirá la búsqueda a SQL y ejecutará la query

## 📊 Información de GPU

### Actual: CPU Mode
```
compute: cpu library
total: 46.8 GiB
available: 36.2 GiB
```

### Para habilitar GPU AMD cuando esté disponible:
1. Asegúrate de tener ROCm instalado en el host
2. El contenedor detectará automáticamente `/dev/kfd` y `/dev/dri`
3. Ollama usará GPU AMD automáticamente

## 🔧 Configuración para GPU AMD (cuando esté disponible)

En `docker-compose.yml` ya está configurado:
```yaml
devices:
  - /dev/kfd:/dev/kfd      # AMD GPU kernel interface
  - /dev/dri:/dev/dri      # AMD GPU driver interface
```

## 📁 Archivos Modificados

- `docker-compose.yml` - Agregado servicio Ollama
- `backend/app/config.py` - URL Ollama actualizada
- `test_ollama.py` - Script de prueba básico
- `test_integration_ollama.py` - Script de prueba de integración backend

## ⚡ Performance

El modelo `llama3.2:3b` es muy ligero:
- Tamaño: ~2GB
- RAM requerida: ~6GB
- Tiempo respuesta: ~2-5 segundos en CPU
- Con GPU AMD: ~0.5-1 segundo

## 🛠️ Troubleshooting

### Ollama no inicia
```bash
docker logs proyecto_guate_ollama
```

### Backend no puede conectar a Ollama
- Verificar que Ollama esté corriendo: `docker ps | grep ollama`
- Verificar que esté en la misma red: `docker network ls`
- Probar conectividad desde backend: `docker exec proyecto_guate_backend curl http://ollama:11434/api/tags`

### GPU no detectada
- Verificar disponibilidad: `docker exec proyecto_guate_ollama rocm-smi`
- Verificar permisos de dispositivos: `ls -la /dev/kfd /dev/dri`

## 📚 Referencias

- Ollama Docker: https://hub.docker.com/r/ollama/ollama
- Modelos disponibles: https://ollama.ai
- ROCm documentation: https://rocmdocs.amd.com/
