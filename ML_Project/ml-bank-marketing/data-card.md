# Data Card - Bank Marketing Dataset

## Fuente
UCI Machine Learning Repository

## Tamaño
45,211 registros y 17 variables

## Tipo de problema
Clasificación binaria

## Variable objetivo
y: indica si el cliente aceptó (yes) o no (no) el depósito

## Variables
- Numéricas: age, balance, duration, campaign, pdays, previous
- Categóricas: job, marital, education, contact, etc.

## Calidad de datos
- No hay valores nulos explícitos
- Existen valores "unknown" en variables categóricas

## Limitaciones
- Dataset desbalanceado (~88% vs 12%)
- Posible data leakage en la variable "duration"
- Algunas variables pueden no estar disponibles en un escenario real

## Riesgos
- Sesgo por desbalance
- Sobreestimación del desempeño si no se maneja correctamente el leakage