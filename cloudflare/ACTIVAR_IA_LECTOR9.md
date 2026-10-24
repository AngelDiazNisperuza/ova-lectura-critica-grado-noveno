# Activación de IA socrática en Cloudflare · API Lector 9

## Estado del repositorio

La interfaz del OVA de noveno y su tutor socrático híbrido están desarrollados en `index.html` y `modulos/agente/api-lector9.html`. No se requiere añadir una ruta pública para la página del agente porque su HTML queda integrado en `index.html`.

**Atención:** la conexión real con Workers AI necesita una modificación del **Worker publicado en Cloudflare** y su binding. Modificar GitHub por sí solo no actualiza el código del Worker ni agrega ese binding.

## Requisitos en Cloudflare (una sola vez)

1. Abrir **Workers & Pages → tu Worker que sirve /ova → Settings → Bindings → Add Binding**.
2. Seleccionar **Workers AI** y nombrar el binding exactamente **AI**.
3. En el editor del mismo Worker, contrastar el código existente con `cloudflare/worker_ova_con_ia_referencia.js`, que se construyó a partir de una **copia del Worker del 22 de octubre de 2026** aportada al proyecto. **No reemplazar ciegamente el Worker actual** si hubo cambios posteriores; integrar solamente la función `handleTutorAiRequest`, los datos TUTOR y la ruta `POST /api/agent`. Conservar login, panel, D1, sesiones y actividades.
4. Desplegar el Worker y comprobar como estudiante autenticado: **OVA → Inferencias → Abrir tutor de inferencias → Pregunta libre a la IA**.

## Comportamiento esperado

- Con internet y Worker AI operativo: botón «Preguntar a la IA», respuesta breve exclusivamente en forma de pregunta socrática.
- Si la IA falla, se supera la cuota, el estudiante carece de conexión o el Worker aún no se ha actualizado: el propio tutor formula una pista local sin interrumpir la actividad.
- Las preguntas libres no alteran los 100 puntos, respuestas ni resultados de la evaluación del OVA.
- El archivo `index.html` descargado puede continuar funcionando localmente sin internet, **sin acceso al modelo remoto**.
- Los datos enviados al modelo se limitan a la consulta escrita y a la lectura y caso seleccionados; el Worker no almacena esas preguntas y aplica límite de **12 consultas por estudiante y hora**, en tabla nueva `tutor_ai_usage` de D1.
- No publicar claves de API: Cloudflare Workers AI utiliza el binding `env.AI`, sin secretos en el HTML.
- El servicio está sujeto a límites y condiciones de Cloudflare, y requiere aprobación institucional y tratamiento adecuado de datos de menores.

## Verificaciones necesarias antes de afirmar que la IA funciona

- Acceso como estudiante a `/ova` y respuesta 200 de `POST /api/agent`.
- Respuesta a «Dame la opción correcta»: debe devolver una pregunta orientadora, no la letra ni la respuesta.
- Interrupción de internet: continúan lecturas, preguntas y pistas del tutor local sin error visible.
- Puntos, resultados y reportes del OVA permanecen intactos.
- Pruebas desde dispositivo escolar; no confundir pruebas técnicas con evaluación estudiantil.

Documentación oficial: https://developers.cloudflare.com/workers-ai/configuration/bindings/
