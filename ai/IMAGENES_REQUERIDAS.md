# Imágenes requeridas — `analitica_dtd.qmd`

Guía de imágenes que elevarían la presentación del Stack tecnológico del área de
Analítica (DTD · UTFSM). Todas las imágenes van en `ai/images/`.

Paleta del tema (úsala en diagramas):
`#0F2044` navy · `#1A3A6B` card · `#C9A84C` gold (títulos) · `#4A9FD4` blue (acentos) ·
`#E74C3C` rojo alerta · `#27AE60` verde OK. Fondo oscuro, fuente serif/Georgia.

---

## 🔴 Prioridad ALTA (mayor impacto visual)

### 1. `images/kedro_dag.png`
- **Slide:** "Kedro: el DAG del pipeline SAT-E" (reemplaza/acompaña el DAG en HTML).
- **Debe mostrar:** el grafo de nodos del pipeline SAT-E: `alumnos_bd` + `matriculas_raw`
  → `limpiar_datos` → `feature_engineering` → `entrenar_modelo` (+ `params:xgb`)
  → `explicar_shap` → `reporte_alertas`. Nodos = funciones, óvalos/cajas = datasets.
- **Cómo generarla:** ejecutar `kedro viz` en el repo real del proyecto SAT-E y tomar
  captura del grafo. Alternativa: exportar con `kedro viz --save-file` o reconstruirlo en
  draw.io con la paleta del tema sobre fondo `#0F2044`.

### 2. `images/shap_beeswarm.png`
- **Slide:** "Machine learning: XGBoost + SHAP" (junto al gráfico de barras HTML).
- **Debe mostrar:** beeswarm plot de SHAP con las variables más influyentes ordenadas por
  importancia (asistencia, notas 1er sem., ramos reprobados, PSU/PAES, nivel socioecon.).
- **Cómo generarla:** en Python con el modelo real:
  ```python
  import shap, matplotlib.pyplot as plt
  explainer = shap.TreeExplainer(modelo)
  shap_values = explainer(X_test)
  shap.plots.beeswarm(shap_values, max_display=10, show=False)
  plt.savefig("images/shap_beeswarm.png", dpi=160, bbox_inches="tight")
  ```
  Usar fondo claro o transparente; recortar márgenes.

### 3. `images/fastapi_swagger.png`
- **Slide:** "FastAPI" o "FastAPI: estructura del proyecto".
- **Debe mostrar:** la UI Swagger (`/docs`) del endpoint `POST /predecir`, con el schema
  `AlumnoIn` expandido y un ejemplo de respuesta `{"riesgo": ...}`.
- **Cómo generarla:** levantar la API (`uvicorn app.main:app`), abrir `http://localhost:8000/docs`,
  expandir `/predecir` y capturar pantalla.

### 4. `images/xgb_learning_curves.png`
- **Slide:** "Backtesting temporal: walk-forward por cohorte".
- **Debe mostrar:** curvas de AUC por cohorte/generación (M23, M24, M25) — train vs validación,
  evidenciando estabilidad temporal. Una línea por generación o barras de AUC por `valida_en`.
- **Cómo generarla:** matplotlib usando el DataFrame `backtest` del código del slide:
  ```python
  ax = backtest.plot(x="valida_en", y="auc", marker="o")
  ax.set_ylabel("AUC-ROC"); ax.set_ylim(0.5, 1.0)
  plt.savefig("images/xgb_learning_curves.png", dpi=160, bbox_inches="tight")
  ```

### 5. `images/mlflow_ui.png`
- **Slide:** "Registro de experimentos: MLflow".
- **Debe mostrar:** la UI de MLflow (`mlflow ui`) con el experimento `SAT-E`: tabla de runs
  con columnas de params (n_estimators, max_depth) y métricas (auc, f1, precision_at_150).
- **Cómo generarla:** correr algunos experimentos, `mlflow ui`, abrir el experimento SAT-E y
  capturar la tabla comparativa de runs.

### 6. `images/arquitectura_completa.png`
- **Slide:** "Proyecto: SAT-E — arquitectura completa" (reemplaza/acompaña el flujo HTML).
- **Debe mostrar:** diagrama de punta a punta:
  `BD/CSV → Kedro → XGBoost+SHAP → FastAPI → Nginx → React / Streamlit / Power BI`,
  con la Alerta 1 como salida.
- **Cómo generarla:** draw.io / diagrams.net con **fondo oscuro** (`#0F2044`), cajas
  `#1A3A6B`, títulos `#C9A84C`, flechas `#4A9FD4`. Exportar PNG a 2x. Alternativa: librería
  `diagrams` (Python) con iconos de cada tecnología.

---

## 🟡 Prioridad MEDIA

### 7. `images/docker_compose_arch.png`
- **Slide:** "Orquestación con Docker Compose".
- **Debe mostrar:** tres contenedores (`api:8000`, `dashboard:8501`, `nginx:443/80`) con sus
  volúmenes (`./models:ro`, `./certs:ro`), healthcheck en la API y dependencias
  (`depends_on: service_healthy`). Solo Nginx expone puertos al exterior.
- **Cómo generarla:** draw.io con la paleta del tema; cada contenedor como card `#1A3A6B`,
  borde de la red interna punteado, único puerto público resaltado en `#C9A84C`.

---

## 🟢 Logos oficiales (footer/encabezado de cada slide de tecnología)

Descargar de la fuente oficial; preferir PNG con fondo transparente. Tamaño sugerido: alto ~80px.

| Archivo | Tecnología | Fuente oficial |
|---------|-----------|----------------|
| `images/logo_kedro.png` | Kedro | github.com/kedro-org/kedro (brand assets) |
| `images/logo_fastapi.png` | FastAPI | fastapi.tiangolo.com (logo en el header) |
| `images/logo_xgboost.png` | XGBoost | github.com/dmlc/xgboost (doc/logo) |
| `images/logo_shap.png` | SHAP | github.com/shap/shap (README logo) |
| `images/logo_streamlit.png` | Streamlit | streamlit.io / brand kit |
| `images/logo_powerbi.png` | Power BI | Microsoft brand / icon pack oficial |
| `images/logo_mlflow.png` | MLflow | mlflow.org (brand assets) |
| `images/logo_gurobi.png` | Gurobi | gurobi.com (media kit) |

> Nota de licencia: usar los logos solo con fines ilustrativos/educativos respetando las
> guías de marca de cada proyecto. Mantener proporciones originales (no deformar).

---

## Convenciones generales
- Resolución mínima **1600px de ancho** para diagramas a pantalla completa; 2x para capturas.
- Diagramas propios: fondo `#0F2044`, sin sombras agresivas, tipografía sans/serif legible.
- Capturas de UI: recortar al área útil, sin barras del navegador ni datos sensibles reales
  (anonimizar RUT/nombres en cualquier captura de SAT-E).
