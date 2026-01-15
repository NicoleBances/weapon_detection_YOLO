# Detección de armas con YOLO

## Colaboradores
- Francesca Nicole Bances Torres 
- Marcos Aaron Bedia Torres 
- Lizbeth Teresita Olivera Alvarez 

## Descripción del proyecto
El proyecto tiene como objetivo desarrollar un sistema de detección automática de armas (pistolas, rifles, cuchillos, granadas) en imágenes estáticas mediante técnicas de procesamiento de imágenes y aprendizaje automático.  
Esto busca contribuir a la seguridad ciudadana, facilitando una detección rápida y precisa de armas en contextos públicos y potencialmente integrable en sistemas de videovigilancia.

Este trabajo también constituye una oportunidad educativa para aplicar técnicas de visión por computadora, detección de objetos y evaluación de modelos en escenarios reales.

## Dataset
- Nombre: [Test Computer Vision Project](https://universe.roboflow.com/ashish-cuamw/test-y7rj3)
- Plataforma: Roboflow Universe  
- Total de imágenes: 4666  
- Distribución por clase:
  - Grenade: 1413  
  - Rifle: 1226  
  - Pistol: 1010  
  - Knife: 845  

## Propuesta de modelización
Se evaluaron modelos YOLO en versiones **Small (s)** y **Nano (n)**:  
- **Nano (n)**: Muy ligero y rápido, adecuado para hardware limitado, pero con menor precisión.  
- **Small (s)**: Equilibrio entre precisión y velocidad, recomendado para hardware moderado.  

| Modelo | Tipo | Velocidad CPU | Ventajas | Desventajas | Uso recomendado |
|--------|------|---------------|----------|-------------|----------------|
| YOLOv5n | Nano | ~3 ms | Muy rápido y eficiente | Menor precisión | Escenarios con hardware muy limitado |
| YOLOv5s | Small | ~5.5 ms | Buen balance velocidad-precisión | Requiere algo más de capacidad | Uso general moderado |
| YOLOv8n | Nano | ~1.2 ms | Muy rápido | Menor precisión | Solo para velocidad crítica |
| YOLOv8s | Small | ~1.2 ms | Preciso, rápido | Más recursos que Nano | Detectar armas en tiempo real (recomendado) |
| YOLOv12n | Nano | ~2.6 ms | Muy eficiente | Menor precisión | Hardware limitado |
| YOLOv12s | Small | ~9.3 ms | Mejor precisión que Nano | Consumo mayor | Hardware con capacidad moderada |

**Decisión del proyecto:** Se seleccionó **YOLOv8s** por su mejor equilibrio entre precisión (mAP@0.5: 0.780) y velocidad de inferencia (1.20 ms en CPU ONNX).

## Entrenamiento de modelos
- **YOLOv5s:** Script oficial `train.py`  
- **YOLOv8s y YOLOv12s:** Biblioteca `ultralytics`  
- **Hiperparámetros comunes:**
  - Tamaño de imagen: 800x800 px  
  - Batch size: 16  
  - Épocas: 100  

- Se comparó rendimiento entre versiones y se evaluaron métricas: **Precisión, Recall, mAP@0.5, mAP@0.5:0.95**.

## Resultados
| Modelo | Precisión | Recall | mAP@0.5 | mAP@0.5:0.95 |
|--------|-----------|--------|----------|--------------|
| YOLOv5s | 0.73969 | 0.66662 | 0.69362 | 0.42625 |
| YOLOv8s | 0.78656 | 0.72473 | 0.78009 | 0.54554 |
| YOLOv12s | 0.75515 | 0.70118 | 0.75901 | 0.53217 |

**Observación clave:** En detección de armas, el **Recall** es crítico para minimizar falsos negativos. Por ello, YOLOv8s se destaca como la mejor opción.

## Conclusiones
- La detección de armas mediante visión por computadora es viable y efectiva.  
- YOLOv8s proporciona el mejor balance entre precisión y velocidad, ideal para escenarios en tiempo real.  
- Los modelos Nano son útiles para velocidad extrema, pero menos confiables en situaciones críticas.  
- La calidad y cantidad del dataset impacta directamente en el desempeño del modelo.

