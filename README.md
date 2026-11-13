# Predicción Inteligente de la Demanda Eléctrica en Colombia 🇨🇴

Este repositorio contiene el desarrollo completo de un sistema de aprendizaje profundo (**Deep Learning**) para pronosticar el consumo de energía eléctrica en el Sistema Interconectado Nacional (SIN) de Colombia, empleando datos oficiales de XM y la plataforma SIMEM.



##  Descripción del Proyecto
El objetivo del proyecto es anticipar la demanda horaria de energía del país superando las limitaciones de los métodos tradicionales (como la persistencia o regresiones simples). Para lograrlo, se implementó, auditó y comparó una arquitectura basada en **Transformers** frente a diversas líneas base estadísticas y recurrentes.



##  Fases del Proyecto

### **Fase 1: Definición y Datos**
* **Dominio:** 16,080 horas continuas de demanda real depurada (2024–2025).
* **Fuentes:** Registros oficiales extraídos y validados desde **SIMEM** y **XM**.
* **Variables:** Consumo horario, estacionalidad, calendario local (marcas diferenciadas de fines de semana y festivos oficiales de Colombia).

### **Fase 2: Replicación y Traslado**
* **Replicación:** Validación inicial del flujo metodológico sobre el benchmark público **GEFCom2012**.
* **Transferencia:** Adaptación del modelo al dominio local colombiano, estructurando particiones estrictamente cronológicas para evitar la fuga de información futura.
* **Estrategia de Entrenamiento:** Se compararon estrategias de *extractor congelado* frente a *fine-tuning total (desde cero)*, demostrando que entrenar el modelo directamente con los datos colombianos reduce drásticamente el error (MAPE de 1.22% en validación).

### **Fase 3: Auditoría y Comunicación**
* **Evaluación contra Líneas Base:** Se contrastó el modelo final (*Transformer*) frente a persistencias diarias ($t-24h$), semanales ($t-168h$), regresión lineal clásica (*Ridge*) y redes recurrentes (*Seq2Seq-GRU*).
* **Explicabilidad y Pruebas de Estresse:** Análisis de matrices de atención, gradientes (*Saliency*) y pruebas de ablación lógica (por ejemplo, alterando festivos para evaluar la sensibilidad del modelo).
* **Resultados Estadísticos:** Validación mediante pruebas de Wilcoxon pareado sobre 56 días de prueba.



##  Resultados Principales (MAPE en Prueba)

| Modelo / Referencia | Error Porcentual Medio (MAPE %) |
| :--- | :---: |
| **Persistencia Diaria ($t-24h$)** | 4.60% |
| **Persistencia Semanal ($t-168h$)** | 3.02% |
| **Regresión Clásica (Ridge)** | 1.87% |
| **Transformer (Nuestro modelo final)** | **1.47%** |
| **Red Recurrente (Seq2Seq-GRU)** | 1.43% *(Empate técnico)* |

* **Significancia:** El modelo Transformer supera con significancia estadística ($p < 0.05$) a los métodos tradicionales y alcanza un empate técnico con la red GRU, logrando tiempos de inferencia de apenas **0.15 ms**.

---

##  Stack Tecnológico
* **Lenguaje:** Python 3.x
* **Librerías principales:** PyTorch / Keras (Deep Learning), Pandas & NumPy (Procesamiento de datos), Scikit-Learn (Métricas y líneas base), Matplotlib / Seaborn (Visualización).
* **Entorno de desarrollo:** VS Code / Google Colab.

---

##  Autor
* **Tania Liceth Barrera López**
* Ciencia de Datos — Universidad Externado de Colombia
