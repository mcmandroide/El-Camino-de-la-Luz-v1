# El Camino de la Luz v1 - Dataset Maestro 5 Capas

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21541281.svg)](https://doi.org/10.5281/zenodo.21541281)
**DOI:** https://doi.org/10.5281/zenodo.21541281

Dataset unificado 28800 filas x 17 columnas de clima espacial 2003-2024 con 5 capas fisicas: eventos solares, medio planetario, GNSS, arrastre satelital y GICs.

## Archivo principal
`DATASET_MAESTRO_V10_FINAL_5CAPAS.csv` - Un solo CSV listo para Python / Excel / ML

## Columnas (17)
- UTC: Fecha hora universal
- Bz_GSM, SYM_H, AE, AL, AU, B_MAG, FlowSpeed, ProtonDensity: Datos OMNI NASA
- source_file: Trazabilidad de donde viene cada fila
- phase_slip_proxy_per_hour, jitter_proxy_ns, timing_error_proxy_ns: Capa 3 GNSS
- drag_proxy_m_day, anomaly_proxy_count: Capa 4 satelites
- dSYM_H_dt, gic_proxy_A: Capa 5A redes electricas

## Trazabilidad source_file
- Halloween2003.csv: 12960 filas - Tormenta G5 2003, 47 sats afectados, blackout Malmo
- SolarEclipse2017.csv: 1440 filas - Eclipse 21/08/2017, calma 0.2 slips/h
- SolarStorm2017.csv: 7200 filas - Tormenta Sep 2017
- SolarEclipse2024.csv: 1440 filas - Eclipse 08/04/2024, calma drag 1.2
- may2024_G5_REAL.csv: 5760 filas - G5 Mayo 2024, 43 slips/h, Starlink -10km

Validacion: Eclipses 2.3A GIC vs Tormentas 27-30A = proxy especifico, no falso.

## Como usar
import pandas as pd
df = pd.read_csv("DATASET_MAESTRO_V10_FINAL_5CAPAS.csv", parse_dates=['UTC'])

## Estado
100% v1 final - Listo para paper
Licencia: CC-BY 4.0
Citar: https://doi.org/10.5281/zenodo.21541281