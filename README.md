# Análisis de Complicaciones Respiratorias en UCI con Modelos Lineales Generalizados

## Ver Análisis Completo
**[Informe Interactivo en RPubs](https://rpubs.com/ASG213/1374219)**

## Resumen
Modelado estadístico de complicaciones respiratorias en pacientes de cuidados intensivos utilizando la base de datos eICU Collaborative Research Database. Aplicación de Modelos Lineales Generalizados (GLM) para predecir duración de ventilación mecánica y riesgo de fallo respiratorio.

## Hallazgos Principales

**Mortalidad y Estancia Hospitalaria:**
- Tasa de mortalidad observada: 4.95% (IC 95%: 4.25%-5.65%), significativamente inferior al estándar nacional del 12% (Z = -13.15, p < 0.001)
- Distribución de estancia altamente asimétrica: mediana 1.70 días vs media 2.67 días
- 58% de pacientes con estancia menor a 48 horas, pero el 1% superior supera los 17 días

**Neumonía Asociada a Ventilación (NAV):**
- Ventilación corta: tasa del 5.36%
- Ventilación prolongada (>7 días): tasa del 20% (p < 0.001)
- El riesgo se cuadruplica con ventilación prolongada

**Inestabilidad Hemodinámica:**
- Presión arterial media poblacional: 84.65 mmHg (por encima del umbral de seguridad)
- Proporción con hipotensión severa (PAM < 65 mmHg): 47.98%-52.15% (IC 95%)
- Aproximadamente la mitad de los pacientes en riesgo de shock

**Modelos Predictivos:**
- **GLM Ventilación Mecánica** (Poisson): R² = 62.65%, MAE = 1.51 días
  - Cirugía electiva reduce duración esperada en 28.5%
  - Cada punto adicional en severidad fisiológica incrementa duración en 1.5%
- **Regresión Logística Fallo Respiratorio**: AUC = 0.975, Sensibilidad = 91.1%, Especificidad = 94.9%
  - Glasgow Coma Scale: predictor más potente (cada punto reduce probabilidad de fallo en 24%)

## Metodología
- **Fuente de Datos**: eICU Collaborative Research Database (2,500+ estancias en UCI)
- **Técnicas Estadísticas**:
  - Análisis Exploratorio de Datos
  - Contrastes de Hipótesis (t-test, test Z, razón de verosimilitudes)
  - Intervalos de Confianza (proporciones, medias, comparaciones por grupos)
  - Modelos Lineales Generalizados (distribuciones Poisson y Gamma)
- **Enfoque Clínico**: Complicaciones neumológicas en cuidados críticos

## Tecnologías
- R 4.x
- Paquetes principales: `tidyverse`, `ggplot2`, `MASS`, `car`

## Estructura del Proyecto
- `analysis.Rmd` - Análisis estadístico completo y modelado
- `data/` - Instrucciones para acceder a la base de datos eICU

## Reproducir el Análisis
```r
# 1. Instalar paquetes necesarios
install.packages(c("tidyverse", "ggplot2", "MASS", "car"))

# 2. Acceder a la base de datos eICU demo (ver data/README.md)

# 3. Renderizar el análisis
rmarkdown::render("analysis.Rmd")
```

## Datos
Este proyecto utiliza la versión demo (v2.0.1) de la [eICU Collaborative Research Database](https://eicu-crd.mit.edu/). Consulta `data/README.md` para instrucciones de acceso.

## Contenido del Análisis
- **Distribuciones de variables clínicas**: Glucosa, presión arterial, saturación O2, leucocitos
- **Estimación puntual**: Métodos de máxima verosimilitud
- **Contrastes de hipótesis**: Mortalidad, estancia, sepsis, neumonía asociada a ventilación
- **Intervalos de confianza**: Proporciones, medias, comparaciones por grupos
- **Modelos GLM**: Predicción de días de ventilación mecánica y fallo respiratorio

## Limitaciones
- **Sesgo de selección**: La base de datos demo no es representativa de todas las UCI estadounidenses
- **Causalidad**: Los modelos identifican asociaciones, no necesariamente relaciones causales
- **Generalización**: Los resultados deben interpretarse en el contexto de los 20 hospitales incluidos
