# Experimentos con StyleGAN para Generación de Pixel Art

Este repositorio contiene un notebook de Jupyter diseñado para experimentar con diferentes configuraciones de una red StyleGAN para generar imágenes de pixel art. El objetivo es comparar tres enfoques distintos y evaluar su impacto en la calidad de las imágenes generadas.

## Ruta Elegida y Dataset

-   **Dataset:** [Pixel Art Sprites](https://www.kaggle.com/datasets/ebrahimelgazar/pixel-art)
-   **Fuente:** Kaggle
-   **Licencia:** CC0: Public Domain. El dataset es de dominio público, lo que permite su uso libre para cualquier propósito.

El dataset consiste en miles de sprites de pixel art de 16x16, lo que lo hace ideal para entrenar modelos de GANs en un entorno con recursos limitados y obtener resultados en un tiempo razonable.

## Cómo Ejecutar

El notebook está diseñado para ser ejecutado en un entorno que proporcione una GPU, como **Google Colab** o **Kaggle Notebooks**.

1.  **Abrir el Notebook:**
    -   En Kaggle: Sube el archivo `GAN.ipynb` a un nuevo notebook.
    -   En Google Colab: Sube el archivo `GAN.ipynb` a tu Drive y ábrelo con Colab.
2.  **Seleccionar Acelerador de GPU:**
    -   En Kaggle: En la configuración del notebook (panel derecho), asegúrate de que el acelerador esté configurado en `GPU`.
    -   En Google Colab: Ve a `Entorno de ejecución` -> `Cambiar tipo de entorno de ejecución` y selecciona `GPU` como acelerador de hardware.
3.  **Ejecutar las Celdas:** Ejecuta las celdas del notebook en orden, desde el principio hasta el final. La primera celda se encargará de instalar todas las dependencias necesarias.

## Cómo Entrenar y Evaluar

El notebook está estructurado para entrenar y evaluar las tres configuraciones de forma automática.

1.  **Setup, Datos y Preprocesamiento (Secciones 1-3):** Las primeras celdas se encargan de la configuración inicial, la descarga del dataset desde Kaggle y el preprocesamiento de las imágenes.
2.  **Entrenamiento A/B/C (Sección 4):** Esta sección contiene el código para entrenar las tres configuraciones de forma secuencial:
    -   **Configuración 1: Baseline:** Un modelo base simple.
    -   **Configuración 2: Regularización y Augmentations:** Utiliza Adaptive Discriminator Augmentation (ADA) y dropout para mejorar la robustez.
    -   **Configuración 3: Variación Arquitectónica / Pérdida:** Emplea una arquitectura de discriminador ResNet, pérdida Hinge y regularización R1.
    Al ejecutar la celda "Ejecución del Entrenamiento", se iniciará todo el proceso, que puede tardar un tiempo considerable dependiendo de la GPU.
3.  **Evaluación (Sección 5):** Una vez finalizado el entrenamiento, esta sección calcula automáticamente las métricas de evaluación (FID e Inception Score) para cada modelo.

## Cómo Generar la Tabla y el Gráfico de Métricas

La generación de los resultados finales es automática y forma parte de la **Sección 5 (Evaluación)**.

1.  **Tabla Resumen:** La primera celda de la sección de evaluación crea y muestra una tabla de `pandas` que resume las pérdidas finales y las métricas (FID, IS) para cada una de las tres configuraciones. Esta tabla también se guarda como `results/metrics_summary.csv`.
2.  **Gráficos Comparativos:** Las celdas siguientes generan y muestran tres gráficos:
    -   Un gráfico de barras que compara los scores **FID** e **IS** entre las configuraciones.
    -   Un gráfico de líneas que compara las **curvas de pérdida** del generador y el discriminador para cada modelo.
    -   Un gráfico de líneas que muestra la evolución de la **probabilidad de aumento (p)** para la configuración con ADA.

Todos los gráficos y resultados generados se guardan en el directorio `/results`.
