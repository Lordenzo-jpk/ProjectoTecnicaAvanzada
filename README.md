# Evaluación Parcial N°1 - Clasificación de Imágenes con MLP

## Descripción del problema de negocio
La detección temprana de enfermedades en cultivos frutales es crucial para evitar pérdidas económicas en el sector agrícola. Actualmente, los agricultores dependen de la inspección visual, un proceso lento y que requiere experiencia especializada, lo que retrasa el diagnóstico y provoca daños irreversibles en los cultivos en sus falsos positivos.

Este proyecto propone desarrollar un modelo MLP que clasifique automáticamente las enfermedades de un único tipo de árbol frutal a partir de fotografías. La especialización en una sola especie permite un modelo más preciso, ya que las enfermedades de un mismo árbol presentan síntomas visuales similares y difíciles de distinguir.

## Objetivos del proyecto
1.- **Desarrollar un modelo MLP** capaz de clasificar imágenes de los tipos de tomates, y así poder tener una predicción mas acertada sobre que frutas están en mal estado y cuales no

2. **Alcanzar un desempeño mínimo** de 80% de Accuracy y 0.75 de F1-Score en el conjunto de prueba, seria lo ideal para que el sistema funcione bien

3. Analizar los errores del modelo e identificar las principales limitaciones del MLP en la clasificación de imágenes.

## Definicion de KPIs
| KPI | Métrica | Meta | Justificación |
|-----|---------|------|---------------|
| Precisión general | Accuracy | > 80% | El modelo debe ser confiable para uso práctico |
| Detección de enfermedades | Recall | > 75% | Es crítico no pasar por alto plantas enfermas |
| Balance general | F1-Score | > 0.75 | Equilibrio entre precisión y recall |
| Confiabilidad por clase | Precision | > 75% | Cada diagnóstico debe ser confiable |
| Velocidad de respuesta | Tiempo de inferencia | < 1 seg | Debe funcionar en tiempo real |

## Fuentes de datos
El conjunto de datos utilizados para este proyecto se extrajo de la plataforma **Kaggle**, específicamente del dataset público **"PlantVillage"**. El cual originalmente el repositorio contiene miles de imágenes de hojas de diversos cultivos.

Para cumplir con la variante propuesta en este proyecto y adaptarlo a la realidad agrícola de la región, se filtró el dataset original para extraer exclusivamente hojas de la especie Tomate (Solanum lycopersicum). Se seleccionaron 4 categorías específicas, conformando un total de miles de imágenes en formato RGB:

1. Tomate Sano (Tomato_healthy)
2. Mancha Bacteriana (Tomato_Bacterial_spot)
3. Tizón Temprano (Tomato_Early_blight)
4. Tizón Tardío (Tomato_Late_blight)
 
## Preparación y Análisis Exploratorio de Datos (EDA) (Descripcion de lo que se hara)
### Descripción del dataset
Se utilizó el dataset **PlantVillage**, que contiene imágenes de hojas de plantas clasificadas por tipo de cultivo y enfermedad. Para este proyecto se definió una **variante enfocada exclusivamente en el cultivo de tomate**, seleccionando 4 clases críticas:

| Clase | Descripción | N° de imágenes |
|-------|-------------|----------------|
| Tomato_healthy | Hojas sanas | 1.591 |
| Tomato_Bacterial_spot | Mancha bacteriana | 2.127 |
| Tomato_Early_blight | Tizón temprano | 1.000 |
| Tomato_Late_blight | Tizón tardío | 1.909 |
| **Total** | | **6.627** |

### Distribución de clases
Se realizó un gráfico de barras para visualizar la distribución de imágenes por clase. Se observa que el dataset está **moderadamente balanceado**, aunque la clase *Early_blight* tiene aproximadamente la mitad de imágenes que *Bacterial_spot*. Esta diferencia no es lo suficientemente crítica como para requerir técnicas de balanceo, pero se tuvo en cuenta al interpretar las métricas por clase.

### Calidad de los datos 
- **Resolucion de la imagen:** Las imágenes del dataset original tienen diferentes tamaños, por lo que fue necesario redimensionarlas a 64x64 píxeles, para que todos esten en el mismo margen
- **Formato:** Todas las imágenes están en formato RGB.

### Preparación de los datos
1. **Filtrado:** Se seleccionaron únicamente las 4 carpetas correspondientes al cultivo de tomate.
2. **Redimensionamiento:** Todas las imágenes se ajustaron a 64x64 píxeles para reducir la carga computacional del MLP.
3. **Normalización:** Los valores de píxeles se escalaron al rango [0, 1] dividiendo por 255, lo que facilita la convergencia del modelo.
4. **División de datos:** Se utilizó una partición de 80% para entrenamiento y 20% para validación, con una semilla fija (seed=42) para garantizar reproducibilidad.
5. **Codificación de etiquetas:** Se utilizó codificación one-hot (categorical) para las 4 clases.


## Metodología (CRISP-DM)
El desarrollo del proyecto siguió las 6 fases de la metodología CRISP-DM:

### 1. Comprensión del negocio
Se identificó la problemática de los pequeños y medianos agricultores de la Región de Valparaíso, quienes enfrentan pérdidas económicas por la detección tardía de enfermedades en cultivos de tomate. Se definió como objetivo desarrollar un modelo MLP capaz de clasificar automáticamente 4 clases críticas (hoja sana, mancha bacteriana, tizón temprano y tizón tardío) a partir de fotografías de hojas.

### 2. Comprensión de los datos
Se utilizó el dataset PlantVillage, filtrando únicamente las 4 clases de tomate seleccionadas. Se realizó un EDA que incluyó:
- Conteo de imágenes por clase (6.627 imágenes en total).
- Visualización de la distribución de clases mediante gráfico de barras.
- Identificación de desafíos: similitud visual entre enfermedades, fondos variables y desbalance leve.

### 3. Preparación de los datos
Se aplicaron las siguientes transformaciones:
- **Filtrado:** Selección de las 4 carpetas de tomate.
- **Redimensionamiento:** Imágenes ajustadas a 64x64 píxeles.
- **Normalización:** Píxeles escalados al rango [0, 1] dividiendo por 255.
- **Codificación:** Etiquetas en formato one-hot (categorical).
- **División:** 80% entrenamiento y 20% validación, con semilla fija de seed= 12.

### 4. Modelamiento 
Se implementó un Perceptrón Multicapa (MLP) con la siguiente arquitectura:
- **Capa de entrada:** Flatten de 64x64x3 = 12.288 neuronas.
- **Capa oculta 1:** 256 neuronas con activación ReLU.
- **Capa oculta 2:** 128 neuronas con activación ReLU.
- **Capa de salida:** 4 neuronas con activación Softmax.
- **Función de pérdida:** Categorical Crossentropy.
- **Épocas:** 15.
- **Batch size:** 32.


### 5. Evaluación
Se evaluó el modelo con las siguientes métricas:
- **Accuracy:** 86.51% (entrenamiento) / 78.42% (validación/entrenamiento).
- **Loss:** 0.34 (entrenamiento) / 0.54 (validación).
- Análisis de curvas de aprendizaje para detectar overfitting.
- Matriz de confusión para identificar clases con mayor confusión.


  ### 6. Despliegue
El modelo entrenado se guardó en formato `.h5`, listo para ser desplegado.
