# API Lector 9 · Evidencia 3 (prototipo)

Este módulo pertenece a la Unidad 3 y acompaña exclusivamente la misión **Inferencias** del OVA de lectura crítica de noveno de la Institución Educativa San José del Pantano.

## Ejecutar sin conexión

Descarga `modulos/agente/api-lector9.html` y ábrelo en un navegador compatible. Los estilos, dos lecturas, cuatro casos y el código de interacción están incorporados en un único archivo; no necesita paquetes, cuentas ni servicios externos para esta demostración.

## Funciones implementadas

- Cuatro casos de inferencia basados en **El cuaderno de Lucía** y **Dos cajas de tierra y una pregunta**, procedentes del `index.html` del OVA original.
- Ciclo de hipótesis, evidencia textual numerada, justificación y revisión, con preguntas, pistas graduadas y opción de consulta al docente.
- Progreso de la tutoría almacenado exclusivamente en el navegador, opción de borrar registros y de imprimir a PDF.
- Interfaz adaptable para móvil y computador. No se utilizan nombres, correos ni datos de estudiantes.

## Límite de implementación

**Este prototipo es un tutor guiado por reglas locales, no una IA generativa ni un modelo de lenguaje ejecutado sin conexión**. La validación del contenido escrito es orientativa, mediante reglas simples, y necesita supervisión del docente. No emite nota, no modifica los 100 puntos del OVA, no envía datos a D1 y no administra cuentas.

## Integración controlada

La rama `feature/api-lector9-unidad3` añade un enlace reversible en el `index.html` que abre el módulo en otra pestaña. Se conserva intacta la ruta de evaluación original. **La rama no está desplegada automáticamente en Cloudflare**; no fusionar sin verificar primero que la ruta del módulo está publicada y funciona tanto en Pages como en el dominio usado por Cloudflare, de lo contrario el enlace podría llevar a una página inexistente. El backend de Cloudflare sigue fuera de esta rama.

## Pruebas

Se probaron el recorrido de hipótesis → evidencia → justificación → revisión, cambio de casos, pistas y vista móvil mediante navegador automatizado. La persistencia efectiva en un dispositivo escolar, el flujo de impresión a PDF y el inicio de sesión real en Cloudflare requieren comprobación adicional en el entorno de despliegue. Estas pruebas técnicas no son evaluación con estudiantes.

## Reversión

No se modifica `main`. Para deshacer el experimento, cerrar la solicitud de cambios sin fusionarla o eliminar la rama de desarrollo. El archivo `index.html` en `main` permanece sin cambios.
