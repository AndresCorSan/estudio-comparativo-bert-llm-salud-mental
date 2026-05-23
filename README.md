# Detección de Trastornos de Salud Mental mediante modelos BERT y LLMs 

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black" alt="Hugging Face">
  <img src="https://img.shields.io/badge/BERT-Fine--Tuning-blue?style=for-the-badge&logoColor=white" alt="BERT Fine-Tuning">
  <img src="https://img.shields.io/badge/LLMs-Zero--Shot-green?style=for-the-badge&logo=openai&logoColor=white" alt="LLMs Zero-Shot">
  <img src="https://img.shields.io/badge/NLP-Mental%20Health-red?style=for-the-badge&logo=health&logoColor=white" alt="Mental Health NLP">
</p>

Este repositorio contiene la investigación y el desarrollo técnico del Trabajo de Fin de Grado (TFG) titulado:  
**"Detección de ansiedad, depresión y trastornos de la conducta alimentaria mediante grandes modelos de lenguaje (LLM): un estudio comparativo desde BERT hasta modelos de última generación"**.

---

## 🎯 Resumen del Proyecto

El objetivo principal es evaluar y comparar la eficacia de dos aproximaciones punteras en el Procesamiento de Lenguaje Natural (PLN) para la detección temprana de trastornos de salud mental en español:

*   **Modelos BERT:** Ajustados mediante *fine-tuning* supervisado (Especialistas).
*   **LLMs de última generación:** Utilizados mediante *zero-shot prompting* (Generalistas).

El estudio se centra en tres trastornos de salud mental: **Ansiedad, Depresión y TCA**, analizando no solo la precisión predictiva, sino también la estabilidad, el coste y la viabilidad de aplicación de estos modelos en entornos reales.

---

## 🛠️ Modelos Evaluados

| Categoría | Modelos | Técnica |
| :--- | :--- | :--- |
| **BERT** | DistilBETO, RoBERTa-large-BNE, mDeBERTa-v3, Longformer | Fine-tuning Supervisado |
| **LLMs Open-Source** | Llama 3.1 8B, GPT-OSS-20B, DeepSeek-V3.2 | Zero-shot Prompting |
| **LLMs Propietarios** | GPT-5.2, Claude Sonnet 4.6, Gemini 3.1 Pro | Zero-shot Prompting |

---

## 📂 Estructura del Repositorio

### 📑 Documentación (Memoria)
*   **`Memoria_latex/`**: Contiene todo el código LaTeX necesario para compilar la **memoria final** del TFG y el **anteproyecto**. Incluye la configuración de estilos, bibliografía, figuras y el "papeleo" administrativo asociado.

### 🧪 Desarrollo Experimental

En **`Desarrollo/`** se encuentran los cuadernos de Jupyter (`.ipynb`) usados para el desarrollo del proyecto, cada uno correspondiente a una fase concreta del desarrollo experimental:

1.  **Exploración del dataset** (`1_exploracion_mentalriskes.ipynb`)
    *   Análisis inicial del dataset MentalRiskES.
    *   Estudio de distribución de clases, número de mensajes y longitud de textos.
    *   Identificación de desbalance y características relevantes.

2.  **Ingeniería de Datos** (`2_preparacion_datos.ipynb`)
    *   Carga desde JSON y preprocesamiento avanzado.
    *   Generación de datasets para clasificación binaria y multiclase.
    *   División en conjuntos de entrenamiento, validación y prueba (BERT).
    *   Visualización de embeddings con **PCA** y **t-SNE**.

3.  **Entrenamiento de Modelos BERT** (`3_BERT_fine_tuning.ipynb`)
    *   Tokenización, configuración de modelos y *fine-tuning* supervisado.
    *   Evaluación sobre el conjunto de prueba y generación de predicciones.

4.  **Inferencia con LLMs (Zero-shot)** (ubicados en `Desarrollo/4_LLMs/`)
    *   Cuadernos: `OpenAI.ipynb`, `Claude.ipynb`, `Gemini.ipynb`, `DeepSeek.ipynb`, `OpenRouter.ipynb`.
    *   Construcción dinámica de prompts.
    *   Gestión de llamadas a API y procesamiento de respuestas.
    *   Almacenamiento estructurado de predicciones.

5.  **Análisis y Métricas** (`5_analisis_resultados.ipynb`)
    *   Cálculo de **F1-score macro, Precision, Recall, MCC** y estabilidad (**TARa@5**).
    *   Estimación de intervalos de confianza mediante **bootstrap**.
    *   Generación de matrices de confusión.
    *   Comparación estadística entre modelos mediante **bootstrap pareado**.
    *   Análisis de la relación **rendimiento–coste**.

---

## 📈 Resultados Destacados

> [!TIP]
> ### 🏆 Mejores Modelos por Tarea
> *   **Ansiedad:** **GPT-OSS-20B** (**F1 = 0.840**), superando significativamente a BERT (RoBERTa: 0.680).
> *   **Depresión:** **Gemini 3.1 Pro** (**F1 = 0.880**), seguido de DeepSeek-V3.2 (0.855).
> *   **TCA:** **GPT-5.2** (**F1 = 0.963**), con RoBERTa-large-BNE destacando como el mejor BERT (0.940).
> *   **Multiclase:** **Gemini 3.1 Pro** (**F1 = 0.864**), con RoBERTa-large-BNE muy próximo (0.842).

> [!IMPORTANT]
> ### 💡 Hallazgos Clave
> *   **Ventajas del Zero-shot prompting en LLMs:** Los LLMs logran un los mejores resultados sin entrenamiento previo especializado, especialmente en la tarea de detección de ansiedad.
> *   **Los modelos BERT son competitivos:** En tareas como TCA y clasificación multiclase, modelos como **RoBERTa-large-BNE** logran igualar o incluso superar el rendimiento de algunos LLMs propietarios.
> *   **TCA como la tarea más sencilla:** La detección de **TCA** resulta significativamente más sencilla para todos los modelos, con F1 > 0.90 de forma generalizada.
> *   **Estabilidad:** Los LLMs muestran una consistencia predictiva superior (**TARa@5 ≈ 0.95–1.00**) frente a la mayor variabilidad de BERT (intervalos de confianza más amplios).
> *   **Liderazgo Global:** Sin restricciones de coste, **Gemini 3.1 Pro** y **GPT-5.2** ofrecen el rendimiento más robusto y elevado en todas las categorías.
> *   **Eficiencia:** **RoBERTa-large-BNE** ofrece el mejor equilibrio rendimiento–coste, siendo la opción ideal para despliegues con recursos limitados.

---

## 📊 Dataset

El trabajo utiliza el dataset **MentalRiskES** (Grupo SINAI, Universidad de Jaén), compuesto por textos en español procedentes de grupos públicos de Telegram, anotados para la detección de:
- Ansiedad
- Depresión
- Trastornos de la Conducta Alimentaria (TCA)

⚠️ *Por motivos de privacidad y licencia, el dataset no se incluye. Puedes solicitar acceso en el [repositorio oficial de SINAI](https://github.com/sinai-uja/corpusMentalRiskES.git).*

---

## 🚀 Requisitos de Ejecución

El proyecto está diseñado para ejecutarse principalmente en **Google Colab**, aprovechando su infraestructura de GPU.

### 💻 Entorno y Hardware
*   **Lenguaje:** Python 3.9+
*   **Hardware:** Se recomienda el uso de una **GPU NVIDIA T4 o superior** para el entrenamiento y evaluación de los modelos BERT.

### 📦 Librerías Principales
> [!NOTE]
> La mayoría de las librerías necesarias ya están preinstaladas en Google Colab. En los casos donde sea necesaria una instalación adicional, se han incluido celdas de instalación (`!pip install`) al inicio de cada cuaderno.

### 🔑 APIs de Modelos (LLMs)
Para replicar la fase de inferencia con modelos de gran escala, es necesario configurar las API keys de los siguientes proveedores:
- **OpenAI** | **Anthropic** | **Google AI Studio** | **DeepSeek** | **OpenRouter**

---

## License and Usage

This repository is publicly accessible for academic review and portfolio purposes.

Commercial use is prohibited without explicit written permission.

Academic use requires prior authorization and proper citation of the original work.