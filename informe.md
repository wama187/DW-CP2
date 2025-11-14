# Documentación del Trabajo

A continuación, se presenta la documentación del proyecto de maqueta web, desarrollado como interpretación del sistema propuesto en el artículo de referencia.

## 1. Datos del Artículo

*   **Autores:** Deepanshi Gupta; Preetvanti Singh
*   **Año:** 2024
*   **Título:** Development of a Recommendation System for Resume Tracking and Job Suggestions
*   **Fuente:** IEEE Xplore, 2024 11th International Conference on Delhi Section (DELCON)
*   **Enlace:** [https://doi.org/10.1109/DELCON64804.2024.10866841](https://doi.org/10.1109/DELCON64804.2024.10866841)

## 2. Tipo de Diseño Representado

El artículo describe un **sistema de recomendación** que utiliza inteligencia artificial generativa, procesamiento de lenguaje natural (NLP) y web scraping para analizar currículums y emparejarlos con ofertas de trabajo relevantes.

El diseño de la aplicación web desarrollada es una **maqueta funcional de la interfaz de usuario (UI)** que representa este sistema. Se centra en el **diseño centrado en el usuario (User-Centered Design)**, simulando el flujo de trabajo que un solicitante de empleo seguiría:

1.  **Carga de CV:** El usuario sube su currículum.
2.  **Análisis (Simulado):** El sistema simula el procesamiento y análisis del documento.
3.  **Visualización de Resultados:** El sistema presenta una lista de ofertas de trabajo personalizadas con un porcentaje de compatibilidad.

## 3. Capturas o Imágenes de la Maqueta

*AQUÍ VA LA CAPTURA DE LA PANTALLA PRINCIPAL DE LA APLICACIÓN*

*AQUÍ VA LA CAPTURA DE LA VISTA DE RESULTADOS CON LAS RECOMENDACIONES*

## 4. Explicación del Diseño

Nuestra maqueta, desarrollada con **Vue.js y TypeScript**, replica la experiencia de usuario del sistema de recomendación descrito en el artículo. Aunque el procesamiento de backend (IA, NLP) está simulado, la interfaz de usuario interpreta fielmente cómo un usuario interactuaría con el sistema final.

*   **Interpretación del Sistema:**
    *   **Carga de CV:** El componente `FileUpload.vue` permite al usuario subir su currículum en formato PDF, iniciando el proceso de recomendación.
    *   **Análisis Inteligente (Simulación):** Tras la carga, el componente `AnalyzingIndicator.vue` y un retardo programado simulan el tiempo que el motor de IA y NLP tardaría en procesar el documento, extrayendo habilidades y experiencia.
    *   **Recomendaciones Personalizadas:** El componente `Results.vue` muestra una lista de ofertas de trabajo (actualmente predefinidas) con un "porcentaje de compatibilidad", representando visualmente la eficacia del emparejamiento que el sistema del artículo busca lograr.
    *   **Detalles de la Oferta:** Un modal (`JobDetailModal.vue`) permite al usuario ver los detalles completos de cada oferta, mejorando la usabilidad.

En resumen, el proyecto es un **prototipo de baja fidelidad** que traduce los conceptos técnicos del artículo en una interfaz tangible, clara y moderna, enfocándose en la usabilidad y la experiencia del solicitante.

## 5. Repositorio del Código

El código fuente de la maqueta está disponible en el siguiente repositorio de GitHub:

*   **Enlace:** [https://github.com/wama187/DW-CP2](https://github.com/wama187/DW-CP2)
