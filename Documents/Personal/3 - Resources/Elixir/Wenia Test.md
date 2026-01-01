# Prueba Técnica Senior Backend Developer

### **Descripción General:**

**"CryptoStream"** es una empresa emergente en el mercado de criptomonedas que busca expandir sus servicios a través de colaboraciones B2B. La empresa necesita un portal de APIs que permita a terceros integrar sus sistemas con la plataforma de CryptoStream para acceder a datos de mercado y realizar operaciones simuladas.

### **Objetivo de la Prueba Técnica:**

Desarrollar un sistema B2B que exponga un portal de APIs para "CryptoStream", permitiendo a empresas terceras:

- Acceder a datos de mercado en tiempo real y a información histórica de criptomonedas específicas.
- Realizar operaciones simuladas de trading para pruebas y desarrollo.
- Implementar autenticación y autorización segura para proteger el acceso a los servicios.

El sistema debe integrar datos de fuentes externas como **Coingecko** y debe incluir capacidades de autenticación, autorización y manejo de transacciones.

### **Descripción Detallada del Proyecto:**

### **1. Autenticación y Autorización:**

- **Sistema de Autenticación:**
    - Implementar autenticación mediante **JWT (JSON Web Tokens)**.

### **2. Integración con Coingecko:**

- **Consumo de APIs Externas:**
    - Obtener datos actualizados de precios y detalles de las siguientes criptomonedas:
        - **Bitcoin (BTC)**
        - **Solana (SOL)**

### **3. Endpoints Funcionales:**

- **Datos de Mercado:**
    - **Endpoint para Obtener Precios en Tiempo Real:**
        - Proporcionar el precio actual en USD de las criptomonedas especificadas.
    - **Endpoint para Obtener Datos Históricos:**
        - Permitir al usuario obtener precios históricos de una criptomoneda específica en un rango de fechas dado.
- **Operaciones de Trading Simulado:**
    - **Endpoint para Compra Simulada:**
        - Permitir al usuario comprar una cantidad específica de una criptomoneda utilizando un saldo virtual en USD.
    - **Validaciones Necesarias:**
        - Verificar que el usuario tenga saldo suficiente antes de realizar la compra.
        - Registrar cada transacción en el historial del usuario.
- **Historial y Estado de Cuenta:**
    - **Endpoint para Consultar Historial de Transacciones:**
        - Listar todas las operaciones de compra y venta realizadas por el usuario.
    - **Endpoint para Obtener Balance Actual:**
        - Proporcionar el saldo actual en USD y las cantidades de cada criptomoneda en posesión del usuario.

### **4. Portal de Documentación del API:**

- **Documentación Interactiva:**
    - Utilizar **Swagger/OpenAPI** para generar documentación detallada y exploración interactiva de los endpoints.
    - Incluir ejemplos de solicitudes y respuestas.

### **Requerimientos Técnicos:**
- **Base de Datos:**
    - Utilizar una base de datos para almacenar información de usuarios, balances y transacciones.
    - Se sugiere el uso de **SQLite**
- **Control de Versiones:**
    - Alojar el repositorio en **GitHub**, asegurando que refleje el historial de commits y el proceso de desarrollo.
- **Pruebas Unitarias:**
    - Incluir pruebas unitarias que cubran las funcionalidades clave.
    - Enfocarse en las operaciones de trading y validaciones.
- **Buenas Prácticas de Desarrollo:**
    - Seguir principios **SOLID** y **Clean Code**.
    - Arquitectura orientada a eventos
    - DDD
    - Manejo adecuado de errores y excepciones.

### **Requerimientos de Entrega:**

### **1. Código Fuente:**

- **Repositorio en GitHub:**
    - El repositorio debe ser público o se deben proporcionar los accesos necesarios.
    - Incluir un archivo **[README.md](http://README.md)** detallado con:
        - Instrucciones para configurar y ejecutar el proyecto localmente.
        - Instrucciones para ejecutar las pruebas unitarias.
        - Detalles sobre la estructura del proyecto y decisiones técnicas.

### **2. Documentación del API:**

- **Swagger/OpenAPI:**
    - Asegurar que la documentación esté accesible y actualizada.
    - Incluir detalles sobre autenticación, ejemplos de llamadas y manejo de errores.
    - Se recomienda orientar el desarrollo a Contract First y usar alguna herramienta que autogenere el Swagger.

### **Plazo de Entrega:**

- La prueba debe ser completada y entregada en un máximo de **5 días** a partir de la recepción de esta asignación.

### **Criterios de Evaluación:**

### **1. Funcionalidad Completa:**

- **Cumplimiento de Requerimientos:**
    - El sistema debe cubrir todos los puntos especificados en la descripción del proyecto.

### **2. Calidad y Mantenibilidad del Código:**

- **Estructura y Organización:**
    - Código bien estructurado y modular.
    - Uso apropiado de patrones de diseño y principios de programación.
    - Diseño de arquitectura usado para la solución

### **3. Pruebas y Calidad:**

- **Cobertura de Pruebas:**
    - Pruebas unitarias que cubran casos críticos y manejo de errores.
- **Automatización:**
    - Instrucciones claras para ejecutar las pruebas.

### **4. Documentación y Entregables:**

- **[README.md](http://README.md):**
    - Claridad y exhaustividad en las instrucciones.
    - Explicación de decisiones técnicas y arquitectónicas.
- **Documentación del API:**
    - Completitud y facilidad de uso.
    - Incluye información sobre autenticación, ejemplos y manejo de errores.

### **5. Seguridad y Buenas Prácticas:**

- **Protección de Datos:**
    - Implementación de medidas de seguridad efectivas.
    - Gestión adecuada de sesiones y tokens.
- **Manejo de Errores:**
    - Respuestas coherentes y útiles al cliente.
    - Registro interno de errores para depuración sin exponer detalles sensibles.

### **Extras Valorados (Opcionales):**

- **Implementación Básica de Arquitectura Orientada a Eventos:**
    - Si el tiempo lo permite, implementar un componente simple que notifique a los usuarios cuando el precio de una criptomoneda cambia significativamente (por ejemplo, más del 5% en 24 horas).
    - Puede ser mediante un sistema interno de mensajes o notificaciones dentro del sistema.
- **Dockerización:**
    - Proporcionar un **Dockerfile** para facilitar la configuración y ejecución del proyecto.

### **Instrucciones Finales:**

- **Entrega:**
    - Al completar la prueba, enviar un correo electrónico con el enlace al repositorio de GitHub.
    - Asegurarse de que todas las instrucciones y documentación estén claras y completas.
- **Comunicación:**
    - Si surgen dudas o necesitas aclaraciones durante el desarrollo, no dudes en comunicarte.
- **Notas Adicionales:**
    - Puedes incluir en el **[README.md](http://README.md)** cualquier consideración adicional, como desafíos encontrados, supuestos realizados o áreas que considerarías mejorar con más tiempo.
