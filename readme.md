# El Camino de la Luz v1.1 - Dataset Maestro 5 Capas

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21541281.svg)](https://doi.org/10.5281/zenodo.21541281)
**DOI:** https://doi.org/10.5281/zenodo.21541281

Dataset unificado de 28,800 filas x 17 columnas de clima espacial 2003-2024, con 5 capas: 3 de datos medidos (eventos solares, medio interplanetario y geomagnético) y 2 de estimaciones derivadas (GNSS y arrastre satelital/GICs). Ver la sección **"Naturaleza de los datos"** más abajo antes de usar este dataset en modelos o análisis.

## Novedades en v1.1 respecto a v1

- Se documenta el porcentaje real de datos faltantes por columna (antes no se mencionaba).
- Se aclara explícitamente que las columnas con sufijo `_proxy_` son **estimaciones derivadas por fórmula**, no mediciones directas de instrumentos.
- Se corrige/retira una cifra de satélites afectados en 2003 que no pudo verificarse en fuentes publicadas.
- Se corrige la cifra de pérdida de altitud de Starlink en mayo 2024, que estaba sobreestimada frente a la literatura publicada.
- Se agregan citas a las fuentes usadas para los datos de contexto histórico.

## Archivo principal
`DATASET_MAESTRO_V10_FINAL_5CAPAS.csv` — Un solo CSV listo para Python / Excel / ML

## Columnas (17)

### Capa 1-2: Datos medidos (NASA OMNI / GFZ Potsdam)
| Columna | Descripción | Completitud |
|---|---|---|
| `UTC` | Fecha y hora universal | 100% |
| `Bz_GSM` | Campo magnético interplanetario, componente Z (GSM), nT | ~76-92% según evento |
| `SYM_H` | Índice de actividad geomagnética de alta resolución (1-min), nT | 100% |
| `AE`, `AL`, `AU` | Índices de electrojet auroral, nT | **~25% (75% de datos faltantes)** |
| `B_MAG` | Magnitud del campo magnético total, nT | **~17% (83% de datos faltantes)** |
| `FlowSpeed` | Velocidad del viento solar, km/s | ~63-69% |
| `ProtonDensity` | Densidad de protones del viento solar, n/cc | ~63-69% |
| `source_file` | Trazabilidad: de qué evento viene cada fila | 100% |

**Nota sobre completitud:** las columnas `AE`, `AL`, `AU` y `B_MAG` tienen huecos considerables. Esto es una limitación real de las fuentes públicas para estos periodos históricos, no un error de procesamiento. Si tu análisis depende fuertemente de estas variables, filtra o imputa con cuidado antes de usarlas.

### Capa 3-5: Estimaciones derivadas (proxies, NO mediciones directas)
| Columna | Qué representa | Cómo se calcula |
|---|---|---|
| `phase_slip_proxy_per_hour` | Estimación de saltos de fase en receptores GNSS | Proxy heurístico basado en la actividad geomagnética del periodo, no en datos reales de receptores GNSS |
| `jitter_proxy_ns`, `timing_error_proxy_ns` | Estimación de error de sincronización GNSS | Ídem — derivado, no medido |
| `drag_proxy_m_day` | Estimación de arrastre atmosférico sobre satélites LEO | Proxy simplificado, no telemetría real de satélites |
| `anomaly_proxy_count` | Conteo estimado de anomalías satelitales | Proxy, no un registro de anomalías reportadas |
| `dSYM_H_dt` | Derivada temporal de SYM_H (dato real, calculado directamente de la columna medida) | Cálculo directo, no proxy |
| `gic_proxy_A` | Estimación de corriente geomagnéticamente inducida (GIC) | Proporcional a `\|dSYM_H/dt\|` — es la aproximación estándar en la literatura de que GIC escala con dB/dt, pero **no reemplaza una medición real de una red eléctrica específica** |

**Importante:** estas 5 columnas son útiles como variables derivadas para modelado (por ejemplo, como features de un modelo de ML que busque correlación entre actividad geomagnética y riesgo operacional), pero no deben citarse como mediciones reales de GNSS, satélites o redes eléctricas. Si tu uso requiere datos medidos reales de estas capas, considera fuentes especializadas (p. ej. IGS/RINEX para GNSS, TLE/space-track.org para arrastre satelital, o reportes de operadores de red para GICs reales).

## Trazabilidad `source_file`

| Archivo | Filas | Evento | Contexto histórico (con fuente) |
|---|---|---|---|
| `Halloween2003.csv` | 12,960 | Tormenta G5, oct. 2003 | Dst mínimo -383 nT; apagón de ~1 hora para ~50,000 usuarios en Malmö, Suecia, el 30 de octubre de 2003 (Pulkkinen et al. 2005, *Space Weather*; Wikipedia). El número exacto de satélites afectados varía según la fuente (28 dañados / 2 perdidos según spacetoday.org; ~59% de las naves reportantes según Gopalswamy 2006) — no se afirma una cifra única. |
| `SolarEclipse2017.csv` | 1,440 | Eclipse solar, 21/08/2017 | Periodo de calma geomagnética (control, no evento de tormenta) |
| `SolarStorm2017.csv` | 7,200 | Tormenta geomagnética, sept. 2017 | Dst mínimo ~-146 nT |
| `SolarEclipse2024.csv` | 1,440 | Eclipse solar, 08/04/2024 | Periodo de calma geomagnética (control, no evento de tormenta) |
| `may2024_G5_REAL.csv` | 5,760 | Tormenta G5 "Gannon", mayo 2024 | Dst mínimo ~-412 a -518 nT (según fuente/resolución); 12-22 satélites Starlink perdidos por estar en órbita de transferencia baja durante la tormenta, con pérdidas de altitud reportadas del orden de cientos de metros, no de kilómetros (Parker & Linares 2024, *Journal of Spacecraft and Rockets*; blog APNIC/IIT Kanpur) |

**Validación de proxies:** los eclipses (periodos de calma) muestran `gic_proxy_A` máximo de ~2.3 A, mientras que las tormentas muestran 7-30 A — la separación es consistente con lo esperado (más actividad geomagnética → proxy más alto), lo que respalda que el proxy responde a la física subyacente, aunque siga siendo una estimación y no una medición.

## Cómo usar
```python
import pandas as pd
df = pd.read_csv("DATASET_MAESTRO_V10_FINAL_5CAPAS.csv", parse_dates=['UTC'])
```

## Estado
v1.1 — corrige documentación de completitud y precisión de afirmaciones históricas respecto a v1. Los datos medidos (Bz, SYM_H) no cambiaron.

Licencia: CC-BY 4.0
Citar: https://doi.org/10.5281/zenodo.21541281
