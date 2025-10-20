# Análisis de Clustering de Campaña de Marketing

## Introducción

El objetivo de este proyecto es realizar un análisis de clustering para segmentar a los clientes de una campaña de marketing en función de su comportamiento y características demográficas. La segmentación de clientes permite a la empresa dirigir sus esfuerzos de marketing de manera más eficaz, personalizando las ofertas y mensajes para cada segmento.

## Metodología

El análisis se llevó a cabo siguiendo los siguientes pasos:

### 1. Carga y Exploración de Datos

- Se cargó el conjunto de datos `marketing_campaign.csv`, que contiene información sobre 2240 clientes.
- Se realizó una exploración inicial para identificar los tipos de datos, la presencia de valores nulos y las características relevantes para el análisis.

### 2. Preprocesamiento de Datos

Se aplicaron varias técnicas de preprocesamiento para limpiar y preparar los datos para el modelo de clustering:

- **Manejo de valores nulos:** Se imputaron los valores nulos en la columna `Income` utilizando la media.
- **Ingeniería de características:**
    - Se convirtió la columna `Dt_Customer` a formato de fecha y se calculó la antiguedad del cliente (`Customer_Lifetime`).
    - Se calculó la edad de los clientes a partir de la columna `Year_Birth` y se eliminaron los valores atípicos (años de nacimiento anteriores a 1920).
- **Codificación de variables categóricas:** Las características categóricas `Education` y `Marital_Status` se convirtieron a formato numérico mediante codificación one-hot.
- **Escalado de características:** Todas las características numéricas se estandarizaron para tener una media de 0 y una desviación estándar de 1, lo cual es crucial para el correcto funcionamiento de los algoritmos de clustering basados en distancia.

### 3. Modelo de Clustering

- Se utilizó el algoritmo **K-Means** para agrupar a los clientes en diferentes segmentos.
- Para determinar el número óptimo de clusters (K), se empleó el **Método del Codo (Elbow Method)**. Este método consiste en ejecutar el algoritmo K-Means para un rango de valores de K y graficar la inercia (Within-Cluster Sum of Squares - WCSS) para cada valor. El "codo" en el gráfico representa el punto donde la disminución de la inercia se ralentiza, sugiriendo un número óptimo de clusters.

### 4. Evaluación del Modelo

La evaluación de un modelo de clustering es a menudo más cualitativa que cuantitativa, ya que el objetivo es obtener clusters que sean interpretables y útiles desde una perspectiva de negocio.

- **Evaluación cualitativa:** Se analizaron las características medias de cada cluster para crear perfiles de cliente y evaluar si los segmentos resultantes son distintos y tienen sentido en el contexto del negocio.
- **Métricas cuantitativas (no implementadas en este análisis):** Para una evaluación más rigurosa, se podría utilizar el **Coeficiente de Silueta (Silhouette Score)**. Esta métrica mide qué tan similar es un objeto a su propio cluster en comparación con otros clusters. Un valor cercano a 1 indica que el objeto está bien asignado a su cluster, mientras que un valor cercano a -1 indica que está mal asignado.

## Resultados

El análisis del método del codo sugirió que 3 o 4 clusters sería un número óptimo. Se eligieron 3 clusters para este análisis.

### Perfiles de los Clusters

- **Cluster 0 (Morado):** Clientes con ingresos y gastos moderados en todas las categorías. Tienen una cantidad moderada de niños y adolescentes en casa.
- **Cluster 1 (Verde):** Clientes con los ingresos más bajos y la mayor cantidad de niños en casa. Sus gastos en todas las categorías son los más bajos.
- **Cluster 2 (Amarillo):** Clientes con los ingresos más altos y la menor cantidad de niños. Son los que más gastan, especialmente en vinos y carnes.

### Visualización

Se utilizó el Análisis de Componentes Principales (PCA) para reducir la dimensionalidad de los datos a 2 componentes y visualizar los clusters en un gráfico de dispersión.

![Visualización de Clusters con PCA](reports/clusters_pca.png)

## Conclusiones

El análisis de clustering ha permitido identificar tres segmentos de clientes distintos y bien definidos. Esta segmentación puede ser muy valiosa para la empresa, ya que permite:

- **Personalizar las campañas de marketing:** Se pueden diseñar ofertas y mensajes específicos para cada segmento. Por ejemplo, al Cluster 2 se le podrían ofrecer vinos y productos gourmet de alta gama, mientras que al Cluster 1 se le podrían ofrecer descuentos y promociones en productos para niños.
- **Optimizar la asignación de recursos:** La empresa puede enfocar sus recursos de marketing en los segmentos más rentables (Cluster 2) o en aquellos con mayor potencial de crecimiento.
- **Mejorar la retención de clientes:** Al comprender mejor las necesidades y preferencias de cada segmento, la empresa puede desarrollar estrategias para aumentar la lealtad y satisfacción de sus clientes.

## Próximos Pasos

Para futuros análisis, se podrían explorar las siguientes áreas:

- **Probar otros algoritmos de clustering:** Algoritmos como DBSCAN o clustering jerárquico podrían revelar diferentes estructuras en los datos.
- **Analizar la relación con las campañas de marketing:** Investigar cómo cada cluster ha respondido a las campañas de marketing anteriores (`AcceptedCmp1`, `AcceptedCmp2`, etc.) para evaluar la efectividad de las mismas.
- **Construir un modelo de clasificación:** Desarrollar un modelo predictivo que pueda clasificar a los nuevos clientes en uno de los segmentos identificados, permitiendo una personalización automática desde el inicio de la relación con el cliente.

## Cómo Reproducir el Análisis

1.  **Clonar el repositorio:**
    ```bash
    git clone <URL_DEL_REPOSITORIO>
    cd <NOMBRE_DEL_REPOSITORIO>
    ```
2.  **Configurar el entorno de conda:**
    ```bash
    conda create -n ScikitLearnClustering python=3.10
    conda activate ScikitLearnClustering
    pip install -r requirements.txt
    ```
3.  **Ejecutar el notebook:**
    Abrir y ejecutar el notebook `notebooks/006_clustering_marketing_campaign.ipynb` en un entorno de Jupyter.
