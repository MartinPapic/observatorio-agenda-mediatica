# 🛰️ Observatorio de Agenda Mediática

Instrumento técnico y público para **auditar la estructura de la cobertura noticiosa** mediante métricas reproducibles: tiempo, temas, actores y dinámica editorial. El observatorio **no evalúa opiniones ni veracidad**; mide **estructura y recurrencia**.

---

## 🎯 Objetivo

Proveer evidencia cuantitativa y verificable sobre la agenda mediática a través de:

* Medición de **tiempo de cobertura por tema**
* **Presencia de actores** e instituciones
* **Dinámica editorial** (persistencia, ciclos, cambios)
* Publicación de **informes** y **datasets abiertos**

Diseñado para uso institucional, académico y ciudadano.

---

## 🧭 Principios metodológicos

* **Neutralidad operacional**: no se infiere sesgo ni intencionalidad.
* **Reproducibilidad**: métricas y categorías públicas.
* **Transparencia**: metodología, supuestos y límites documentados.
* **Privacidad**: no identificación biométrica; roles editoriales, no identidades.

---

## 🧱 Arquitectura (alto nivel)

```
Captura (batch)
→ Segmentación editorial
→ Diarización por rol
→ Transcripción con timestamps
→ Clasificación temática jerárquica
→ Cálculo de indicadores
→ Publicación (API + Frontend)
```

* **Batch-first** (no tiempo real)
* Componentes desacoplados
* GPU solo cuando aporta valor

---

## 🧩 Stack tecnológico

### Frontend

* **SvelteKit** (static + SSR liviano)
* Visualizaciones simples (líneas, barras, áreas)
* Hosting estático (Vercel/Netlify)

### Backend

* **FastAPI (Python)**
* Endpoints read-only
* Cache opcional (Redis)

### Pipeline

* **Prefect OSS** (orquestación)
* Contenedores on-demand
* GPU spot para ASR/diarización

### Datos

* **Postgres** (+ pgvector opcional)
* Object Storage (audio y artefactos)

---

## 📊 Indicadores

### Agenda y tiempo

* % de tiempo por tema
* Ranking diario/semanal
* Entropía / concentración temática

### Actores

* Tiempo de mención por institución
* Voz directa vs indirecta
* Diversidad de fuentes (conteo)

### Dinámica

* Persistencia de temas
* Aparición/desaparición
* Cambios interdiarios

> Los indicadores se calculan sobre **segmentos noticiosos**, no sobre frases aisladas.

---

## 🗂️ Modelo de datos (resumen)

* `media_outlet`
* `broadcast`
* `segment` (inicio, fin, duración)
* `topic` (jerárquico)
* `actor` (institución/rol)
* `metrics_daily`
* `metrics_weekly`

Los textos completos no son públicos por defecto; se publican **agregados**.

---

## 🔐 Aspectos legales y éticos

* Fuentes públicas (streams oficiales)
* Sin identificación de personas
* Roles editoriales (conductor, invitado, voz en off)
* Declaración ética y registro de cambios metodológicos

---

## 🚀 Puesta en marcha (local)

### Requisitos

* Python 3.10+
* Docker
* FFmpeg

### Pasos

1. Clonar repositorio
2. Crear entorno virtual
3. Configurar variables de entorno
4. Levantar Postgres
5. Ejecutar pipeline de prueba

*(Instrucciones detalladas en `/docs/setup.md`)*

---

## 📅 Roadmap

### MVP (0–60 días)

* 3 medios
* 1 noticiero diario
* 5 categorías temáticas
* Dashboard público
* Informe semanal

### 6–12 meses

* Más medios
* Históricos comparables
* API pública de datasets
* Comité asesor

---

## 📄 Licencia

* Código: MIT
* Metodología: CC BY 4.0
* Datasets: CC BY-NC (salvo indicación)

---

## 🤝 Contribuciones

Se aceptan issues y PRs, especialmente en:

* Mejora de segmentación editorial
* Nuevos indicadores
* Documentación metodológica

---

## 📬 Contacto

Para colaboraciones institucionales o académicas, abrir un issue o contactar a los mantenedores.

---

> *Un observatorio no opina: **mide**. La interpretación queda en manos de la sociedad.*
