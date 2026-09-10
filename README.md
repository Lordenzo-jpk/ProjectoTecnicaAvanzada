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
[Por desarrollar]

## Preparación y Análisis Exploratorio de Datos (EDA) (Descripcion de lo que se hara)
[Por desarrollar]

## Metodología (CRISP-DM)
[por desarrollar]
