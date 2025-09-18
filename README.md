# Predicción de Supervivencia en el Titanic

Este proyecto busca predecir la supervivencia de pasajeros del Titanic mediante técnicas de análisis de datos, modelado supervisado y no supervisado, así como estrategias híbridas. Está dirigido a analistas, científicos de datos y estudiantes interesados en aplicar machine learning en contextos históricos y narrativos.

##  Introducción

Se realizó un proceso completo de ETL para limpiar el dataset, imputar valores nulos, crear nuevas variables y codificar variables categóricas. El análisis exploratorio (EDA) reveló patrones en sexo, edad, clase y tarifas. Se aplicaron modelos supervisados como Regresión Logística, Random Forest, KNN y SVM, y un análisis no supervisado con K-means (K=4) para segmentar pasajeros e interpretar arquetipos. Finalmente, se evaluaron estrategias híbridas:  
- **Ruta A**: Mixture of Experts  
- **Ruta B**: Clúster como feature adicional

##  Análisis Exploratorio

- 38.3% de los pasajeros sobrevivió  
- Las mujeres y los niños tuvieron mayor probabilidad de supervivencia  
- Los pasajeros de 1ª clase presentaron ventajas claras frente a 2ª y 3ª clase

##  Modelado Supervisado (Baseline)

Se aplicaron cuatro modelos supervisados. El desempeño se resume a continuación:

| Modelo               | Accuracy | Precision | Recall  | AUC    |
|----------------------|----------|-----------|---------|--------|
| Regresión Logística  | 0.8338   | 0.7998    | 0.7571  | 0.8696 |
| Random Forest        | 0.8114   | 0.7642    | 0.7369  | 0.8623 |
| KNN                  | 0.8159   | 0.7925    | 0.7047  | 0.8622 |
| SVM                  | 0.8100   | 0.8100    | 0.6800  | 0.8370 |

##  Comparación de Modelos

- Regresión Logística destaca por su AUC (≈0.87)  
- SVM logra mayor precisión  
- Las matrices de confusión muestran fortalezas distintas: algunos modelos priorizan detección de no sobrevivientes, otros balance entre clases  
- Las curvas ROC confirman buen rendimiento general (AUC > 0.8)

##  Análisis No Supervisado (K-means)

Se aplicó K-means (K=4) para segmentar pasajeros en clústeres con perfiles diferenciados:

- **Clúster 3**: Mujeres de clase media con alta supervivencia (≈79%)  
- **Clúster 1**: Hombres mayores de 1ª clase con supervivencia intermedia (≈47%)  
- **Clúster 2**: Familias numerosas de 3ª clase con supervivencia baja-intermedia (≈44%)  
- **Clúster 0**: Hombres jóvenes de 3ª clase con baja supervivencia (≈26%)

##  Estrategias Híbridas

Se probaron dos enfoques:

| Modelo                          | Accuracy | Precision | Recall  | AUC    |
|----------------------------------|----------|-----------|---------|--------|
| Ruta A (Mixture of Experts)      | 0.7877   | 0.7460    | 0.6811  | 0.7678 |
| Ruta B (Cluster como feature)    | 0.8305   | 0.7961    | 0.7513  | 0.8695 |

- Ruta B mantiene métricas similares al baseline  
- Ruta A degrada el rendimiento por menor capacidad de generalización en subgrupos

##  Consideraciones Técnicas

- Se detectó fuga de datos por imputaciones y clustering global  
- Se recomienda encapsular todo el preprocesamiento en un pipeline y recalcular por fold en cada split/CV

##  Conclusiones

- Sexo, edad y clase social fueron factores clave en la supervivencia  
- Regresión Logística fue el mejor modelo por AUC  
- El clustering aportó interpretabilidad pero no mejoró métricas  
- Se confirma la regla histórica: “Mujeres y niños primero, especialmente de clases altas”

---
