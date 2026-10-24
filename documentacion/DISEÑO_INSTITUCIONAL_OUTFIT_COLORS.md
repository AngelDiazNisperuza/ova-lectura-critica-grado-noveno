# Interfaz institucional — Outfit y Space Grotesk

La interfaz **original** del OVA y del tutor se conserva: tarjetas, navegación, cuestionarios, efectos, botones y estructura. Únicamente se actualiza la paleta institucional (azul, verde, amarillo) y la tipografía: **Outfit** para títulos y texto; **Space Grotesk** para etiquetas, indicadores y metadatos.

## Aplicación

- `index.html` incorpora la hoja oficial de Google Fonts y estilos CSS de identidad; el agente integrado y la misión de Inferencias mantienen sus funciones.
- `modulos/agente/api-lector9.html` incorpora la misma hoja de fuentes y conserva su respaldo socrático sin conexión.
- Las vistas de **login** y **administración** se generan desde el Worker de Cloudflare, que no se despliega automáticamente al actualizar GitHub. El nuevo Worker está preparado por separado para instalarse en Cloudflare tras respaldar y revisar la versión actual.

## Seguridad y disponibilidad

El Worker conserva sesiones, PIN, sincronización D1, la ruta `/agente` y la IA. Su política CSP necesita `style-src https://fonts.googleapis.com` y `font-src https://fonts.gstatic.com`, sin autorizar scripts adicionales. Las fuentes de Google se cargan **cuando existe internet**; sin conexión se usa `Segoe UI` o la fuente del sistema como alternativa. La funcionalidad pedagógica no depende de las fuentes.

## Validación de la publicación

1. Abrir el OVA y comprobar la tipografía y los colores de inicio, Inferencias, Argumentación, reto final y reporte.
2. Abrir `/agente`, utilizar Intro para enviar e intentar actualizar la pestaña.
3. Comprobar acceso y registro de estudiantes y el panel administrativo.
4. Revisar la consola de Chrome para confirmar que la CSS de Google Fonts y los archivos de fuentes se descargan sin bloqueos CSP.
5. Probar un ejercicio, el historial de tutorías, la IA en línea y el respaldo local sin internet.
6. Conservar el Worker anterior para una restauración inmediata si surgiera un problema.
