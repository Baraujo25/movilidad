# Datos de movilidad — Intendencia de Montevideo

Datasets públicos del **Centro de Gestión de Movilidad (CGM)** de la Intendencia de Montevideo, preparados para ingesta en un datalake (NiFi → HDFS).

**Fuente original:** Portal de Datos Abiertos — Intendencia de Montevideo (no Kaggle).

---

## Estructura

| Carpeta | Contenido | Período |
|---------|-----------|---------|
| `parque-automotor/` | Parque vehicular y catálogo de tipos | 2019, 2024 |
| `conteo/` | Volumen vehicular cada 5 min en avenidas | Ene 2019, Ene 2024 |
| `velocidad/` | Velocidad promedio por carril | Ene 2021 (≈2019), Ene 2024 |
| `sensores/` | Ubicación de sensores de medición | 2021 (≈2019), 2024 |

Cada carpeta incluye `descripcion-datos.md` con el dominio de las columnas.

---

## Archivos

| Archivo | Tamaño aprox. | Git LFS |
|---------|---------------|---------|
| `parque-automotor/parque_dag_2019.csv` | 3.2 MB | No |
| `parque-automotor/parque_dag_2024.csv` | 3.2 MB | No |
| `parque-automotor/tipos_vehiculos_dag.csv` | 7 KB | No |
| `conteo/autoscope_ene_2019.csv` | 227 MB | **Sí** |
| `conteo/autoscope_01_2024_volumen.csv` | 296 MB | **Sí** |
| `velocidad/autoscope_01_2021_velocidad.csv` | 367 MB | **Sí** |
| `velocidad/autoscope_01_2024_velocidad.csv` | 286 MB | **Sí** |
| `sensores/infosensoresmedicionconteo012021.csv` | 13 KB | No |
| `sensores/infosensoresmedicionconteo012024.csv` | 11 KB | No |

---

## Consumo HTTP (NiFi / InvokeHTTP)

Archivos **sin** LFS:

```
https://raw.githubusercontent.com/Baraujo25/movilidad/main/{ruta}
```

Archivos **con** LFS (`conteo/`, `velocidad/`):

```
https://media.githubusercontent.com/media/Baraujo25/movilidad/main/{ruta}
```

> No usar `raw.githubusercontent.com` para archivos LFS: devuelve un puntero de ~130 bytes, no el CSV.

---

## Notas metodológicas

- **Parque automotor:** solo existen snapshots 2019 y 2024.
- **Velocidad 2019:** no hay registro; se usa enero 2021 como proxy.
- **Sensores 2019:** metadata de 2021 como proxy de ubicaciones.
- **Comparación temporal:** enero 2019 vs enero 2024 para conteo y velocidad.

---

## Obligatorio Big Data — ORT 2026

Este repo es el **staging HTTP** para la ingesta NiFi del obligatorio de Herramientas de Software para Big Data. El análisis (Spark, Hive, SuperSet) se realiza sobre copias en HDFS.
