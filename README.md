# Data Engineering Challenge

## Índice
Parte 1: Ingesta de Datos
1. [Introducción](#1-introducción)
   - [1.1. Contexto del problema](#11-contexto-del-problema)
   - [1.2. Objetivo de la solución](#12-objetivo-de-la-solución)

2. [Diseño del Pipeline](#2-diseño-del-pipeline)
   - [2.1. Esquema general](#21-esquema-general)
   - [2.2. Descripción de las etapas](#22-descripción-de-las-etapas)
     - [2.2.1. Extracción](#221-extracción)
     - [2.2.2. Transformación inicial](#222-transformación-inicial)
     - [2.2.3. Carga al Datalake](#223-carga-al-datalake)
     - [2.2.4. Carga en Base Relacional](#224-carga-en-base-relacional)

3. [Stack Tecnológico Propuesto](#3-stack-tecnológico-propuesto)
   - [3.1. Herramientas para cada etapa](#31-herramientas-para-cada-etapa)
   - [3.2. Ventajas de usar GCP y Data Fusion](#32-ventajas-de-usar-gcp-y-data-fusion)

4. [Planificación del Proyecto](#4-planificación-del-proyecto)
   - [4.1. Requerimientos previos](#41-requerimientos-previos)
   - [4.2. Etapas de implementación](#42-etapas-de-implementación)
   - [4.3. Plazos estimados](#43-plazos-estimados)

5. [Estrategia de Monitoreo](#5-estrategia-de-monitoreo)
   - [5.1. Alertas y métricas clave](#51-alertas-y-métricas-clave)
   - [5.2. Visualización de estados](#52-visualización-de-estados)

6. [Análisis de Riesgos y Puntos de Falla](#6-análisis-de-riesgos-y-puntos-de-falla)
   - [6.1. Identificación de posibles fallos](#61-identificación-de-posibles-fallos)
   - [6.2. Mitigación de riesgos](#62-mitigación-de-riesgos)

7. [Conclusión](#7-conclusión)
   - [7.1. Resumen de la solución](#71-resumen-de-la-solución)
   - [7.2. Beneficios esperados](#72-beneficios-esperados)

## 1. Introducción

### 1.1. Contexto del problema
La compañía ACME busca modernizar el manejo de sus datos mediante la implementación de un Datalake. Actualmente, sus tablas tienen características variadas: algunas son dimensionales y otras transaccionales, con diferencias en el manejo de timestamps. Este proyecto busca diseñar un pipeline escalable que permita la ingesta full/incremental de datos en un entorno que facilite el análisis.

### 1.2. Objetivo de la solución
Implementar un pipeline eficiente y escalable sobre Google Cloud Platform (GCP) utilizando Cloud Data Fusion para gestionar la ingesta, almacenamiento y transformación de datos. Además, proporcionar estrategias de monitoreo y mitigación de fallas para garantizar la operación continua.

## 2. Diseño del Pipeline

### 2.1. Esquema general
<img src="https://github.com/nahiriv/data-engineering-challenge/blob/main/pipeline-diagram.png" alt="Esquema del Pipeline" style="max-width:100%; height:auto;">
El pipeline se organiza en etapas principales:
- Extracción
- Transformación inicial (Staging)
- Carga al Datalake
- Consolidación en una base analítica (BigQuery)

### 2.2. Descripción de las etapas

#### 2.2.1. Extracción
Los datos se extraen desde bases relacionales utilizando conectores de Cloud Data Fusion, configurando tareas específicas para ingestas full o incrementales.

#### 2.2.2. Transformación inicial
Los datos son procesados para limpieza básica, enriquecimiento con metadatos y validación inicial. Esta etapa ocurre en Cloud Data Fusion.

#### 2.2.3. Carga al Datalake
Los datos procesados se almacenan en Cloud Storage en formato Parquet o Avro, organizados en particiones para optimizar el análisis posterior.

#### 2.2.4. Carga en Base Relacional
Los datos se consolidan en BigQuery mediante operaciones MERGE, reemplazando o actualizando registros según el tipo de tabla.

## 3. Stack Tecnológico Propuesto

### 3.1. Herramientas para cada etapa
- **Cloud Data Fusion**: Orquestación de pipelines y transformaciones.
- **Cloud Storage**: Datalake para almacenamiento escalable y particionado.
- **BigQuery**: Base analítica para consultas rápidas y análisis de datos.

### 3.2. Ventajas de usar GCP y Data Fusion
- **Interfaz visual**: Pipelines fáciles de construir y gestionar.
- **Escalabilidad**: Procesamiento distribuido sobre Apache Beam.
- **Conectividad**: Soporte nativo para diversas fuentes y destinos.
- **Costo-eficiencia**: Facturación por uso.

## 4. Planificación del Proyecto

### 4.1. Requerimientos previos
- Identificación de tablas clave para ingesta.
- Configuración de permisos en GCP para acceso a fuentes y almacenamiento.
- Creación de buckets en Cloud Storage y esquemas en BigQuery.

### 4.2. Etapas de implementación
- Configuración de servicios (1-2 semanas).
- Creación y prueba de pipelines full (2 semanas).
- Implementación de ingestas incrementales (2 semanas).
- Integración con BigQuery y optimización (2 semanas).

### 4.3. Plazos estimados
Total de 8 semanas.

## 5. Estrategia de Monitoreo

### 5.1. Alertas y métricas clave
- Configuración de alertas en Cloud Monitoring para detectar fallas o retrasos.
- Monitoreo de volumen y calidad de datos procesados en cada etapa.

### 5.2. Visualización de estados
- Uso de Cloud Logging para centralizar logs.
- Dashboards en Cloud Monitoring con métricas de pipelines y tareas.

## 6. Análisis de Riesgos y Puntos de Falla

### 6.1. Identificación de posibles fallos
- Fallos en la conexión con bases fuente.
- Errores en transformación de datos (esquemas inconsistentes).
- Problemas de permisos en Cloud Storage o BigQuery.

### 6.2. Mitigación de riesgos
- Implementar reintentos automáticos en Data Fusion.
- Validar esquemas en etapas iniciales.
- Documentar flujos y procedimientos para soporte.

## 7. Conclusión

### 7.1. Resumen de la solución
El pipeline diseñado es escalable, eficiente y está alineado con los objetivos del proyecto ACME, garantizando un proceso analítico simplificado en un entorno robusto como GCP.

### 7.2. Beneficios esperados
- Reducción de tiempos de procesamiento.
- Escalabilidad para soportar crecimiento futuro.
- Mayor confiabilidad en la operación del pipeline.


