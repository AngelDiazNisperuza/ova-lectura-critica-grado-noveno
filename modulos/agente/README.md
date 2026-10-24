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

## Integración controlada en el OVA y Cloudflare

El OVA incluye dentro de la misión **Inferencias** un botón **«Abrir tutor de inferencias»**. En esta versión el HTML completo del tutor está incorporado en `index.html`, de modo que al abrirlo en otra pestaña no solicita a Cloudflare un archivo adicional inexistente. Es un diseño reversible que evita cambiar la autenticación o las tablas D1.

- En **Cloudflare**, el estudiante debe iniciar sesión de manera habitual y abrir la ruta autenticada `/ova`; se aplica la política de seguridad de esa página.
- En una copia local, el tutor funciona sin conexión tras abrir `index.html`.
- La calificación oficial del OVA continúa independiente del historial local del tutor.
- El programa `modulos/agente/api-lector9.html` se conserva como copia independiente para pruebas y auditoría.
- Si un navegador bloquea nuevas pestañas, es necesario habilitar ventanas emergentes para el sitio educativo.
- No se ha integrado un servicio generativo, ni se han verificado todavía las credenciales o la publicación real del Worker.

## Pruebas

Se probaron el recorrido de hipótesis → evidencia → justificación → revisión, cambio de casos, pistas y vista móvil mediante navegador automatizado. La persistencia efectiva en un dispositivo escolar, el flujo de impresión a PDF y el inicio de sesión real en Cloudflare requieren comprobación adicional en el entorno de despliegue. Estas pruebas técnicas no son evaluación con estudiantes.

## Reversión

No se modifica `main`. Para deshacer el experimento, cerrar la solicitud de cambios sin fusionarla o eliminar la rama de desarrollo. El archivo `index.html` en `main` permanece sin cambios.
