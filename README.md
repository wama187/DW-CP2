## Ejecutar con Docker

Para ejecutar la aplicación utilizando Docker, sigue estos pasos:

1.  **Construir la imagen de Docker:**
    ```bash
    docker build -t dw-cp2 .
    ```

2.  **Ejecutar el contenedor de Docker:**
    ```bash
    docker run -p 3000:3000 dw-cp2
    ```

    La aplicación estará disponible en `http://localhost:3000`.
