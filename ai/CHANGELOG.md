# CHANGELOG — `analitica_dtd.qmd`

Mejora exhaustiva de la presentación del Stack tecnológico del área de Analítica (DTD · UTFSM).
Se pasó de **~22 slides a ~38 slides**, profundizando en código real del contexto SAT-E/DTD y
agregando una nueva sección de calidad y reproducibilidad. Sin animaciones incrementales;
estilo, paleta y patrón de 2 columnas mantenidos.

## Slides NUEVAS

### Sección 1 · Capa de datos
- **Validación y limpieza con pandas** — merge `validate="1:1"` de fuentes heterogéneas,
  casting/`fillna`, y validación de esquema con `pandera` (`DataFrameSchema`, `lazy=True`).

### Sección 2 · Capa de modelos
- **Backtesting temporal: walk-forward por cohorte** — loop M23→M24→M25 entrenando en el
  pasado y validando en la generación siguiente, con AUC por cohorte.
- **Métricas de evaluación: ¿qué medimos?** — AUC-ROC, F1 y `precision@K` (función propia),
  con callout-important explicando por qué precision@K supera a accuracy en eventos raros.
- **Optimización: el modelo MILP del scheduler** — formulación matemática formal en LaTeX
  (`$$`) + código `gurobipy` con 3 restricciones (asignación única, sala sin choque, capacidad).
- **Kedro: el Data Catalog** — `catalog.yml` con `CSVDataset`, `SQLTableDataset`,
  `ParquetDataset` y `PickleDataset` (`versioned: true`).
- **Kedro: el DAG del pipeline SAT-E** — DAG visual en HTML (estilo del tema) con los nodos
  del pipeline de extremo a extremo.

### Sección 3 · Backend y servicios
- **FastAPI: estructura del proyecto** — árbol de carpetas `routers/ schemas/ models/
  services/ core/` + ejemplo de `APIRouter`.
- **FastAPI: autenticación con OAuth2 / JWT** — `OAuth2PasswordBearer`, validación de Bearer
  token con `jose.jwt`, dependencia `usuario_actual` que protege endpoints.
- **Orquestación con Docker Compose** — YAML con servicios `api`, `dashboard`, `nginx`;
  `expose`, `volumes :ro`, `healthcheck` y `depends_on: service_healthy`.

### Sección 4 · Capa de presentación
- **Streamlit: estado con `st.session_state`** — persistencia de filtros (campus, umbral)
  entre reruns.
- **Streamlit ↔ FastAPI: consumir el modelo** — `requests.get` con Bearer token y
  `@st.cache_data(ttl=300)`.

### Sección 6 · Control de calidad y reproducibilidad (NUEVA SECCIÓN)
- **Portada de sección** — divider con `background_slides3.png` (opacity 0.3).
- **Control de versiones: Git + GitHub** — branching `main/develop/feature/*`, PR + review +
  CI, tags de release; diagrama de ramas en HTML.
- **Testing en pipelines de datos** — `pytest` (lógica) + `great_expectations` (datos).
- **Drift detection: KS test y PSI** — `scipy.stats.ks_2samp` + función `psi` propia con
  umbrales de interpretación.
- **Registro de experimentos: MLflow** — `log_params`, `log_metrics`, `sklearn.log_model`
  con Model Registry.

## Slides MODIFICADAS
- **Portada de sección "Proyectos destacados"** — renumerada de *Sección 5* a *Sección 7*
  por la inserción de la nueva Sección 6.

## Sin cambios
- Title, ¿Qué hace el área?, dividers de Secciones 1–4, Fuentes de datos, ML XGBoost+SHAP,
  Ejemplo SAT-E, Modelos estadísticos y optimización, Pipelines Kedro+pandas, FastAPI, Nginx,
  Streamlit, React+MUI, Power BI, ¿Cuándo usar qué?, SAT-E arquitectura, USM Scheduler,
  Recursos y referencias, ¿Preguntas?

## Notas técnicas
- `incremental: false` y el resto del front-matter YAML intactos.
- Todas las slides nuevas siguen el patrón de 2 columnas (texto izquierda / código o HTML
  derecha) y la paleta del tema en los bloques HTML.
- Verificado con `quarto render analitica_dtd.qmd --to revealjs` → *Output created* sin errores.
- Ver `IMAGENES_REQUERIDAS.md` para las imágenes recomendadas (kedro_dag, shap_beeswarm,
  fastapi_swagger, etc.).
