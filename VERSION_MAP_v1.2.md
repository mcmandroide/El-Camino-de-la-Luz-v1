# El Camino de la Luz - Mapa de Versiones v1.2 / v4
> Columna vertebral documental que une Publicación (GitHub/Zenodo) con Investigación (Kaggle).
> Fecha: 2026-08-07

| Artefacto | Versión Lógica | Versión Técnica Zenodo/Kaggle | Propósito | Identificador Citable | Estado al 2026-08-07 |
|---|---|---|---|---|---|
| **Dataset Maestro Público** | v1.2 | Zenodo v4 | Publicación abierta, citable, 2003–2024, 28800x17, corrección de documentación | DOI v4: 10.5281/zenodo.21842130 / DOI concepto: 10.5281/zenodo.21541280 | Publicado - Corrección de documentación |
| **Dataset Maestro Público** | v1.0 | Zenodo v1 | Primera publicación | DOI v1: 10.5281/zenodo.21541281 | Histórico - reemplazado |
| **Dataset Maestro Kaggle** | v5 | Kaggle Dataset v5 | Línea base experimental para congelar hipótesis | DATASET_MAESTRO_V10_FINAL_5CAPAS.csv (28,800x17) + SHA-256 | Congelado |
| **Hipótesis** | v5.0-Frozen | - | Predicción formal eclipse 2026-08-12 out-of-sample | SHA-256 de hypotheses_v5.0-frozen.json | Congelada |
| **Validation Engine** | v1.0 | - | Evaluación reproducible de predicciones | Spec en validation_engine_v1.py | Congelado |
| **Dry Run** | histórico 2003/2017/2024 | - | Prueba operacional del pipeline | Sidecars con hashes | Ejecutado |
| **Eclipse 2026-08-12** | - | - | Evento out-of-sample real | Pendiente observación NASA OMNI / GFZ | Futuro - no en histórico |
| **Discovery Engine** | v7 | - | Fase 7: Causalidad / temporalidad sin hipótesis previas | Pendiente | Siguiente fase |

## Regla de oro para Fase 7

MEDICIÓN DIRECTA (Bz_GSM, SYM_H, FlowSpeed, ProtonDensity) -> 100% trazable
  ↓
VARIABLE DERIVADA (dSYM_H_dt) -> cálculo directo
  ↓
PROXY ESTIMADO (_proxy_) -> fórmula heurística, NO medición GNSS/satélite/red eléctrica directa
  ↓
ÍNDICE / MÉTRICA DE RESPUESTA
  ↓
INFERENCIA

Cada salto debe quedar identificado en cualquier tabla, figura o texto de Fase 7.
