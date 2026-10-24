# Corrección de recarga de API Lector 9 en Cloudflare

## Problema corregido
La versión anterior abre el tutor en una pestaña `about:blank` y escribe dentro su HTML. Esa pestaña no tiene una ruta persistente y queda blanca si se actualiza.

## Ruta propuesta
`GET /agente` en el mismo Worker que sirve `/ova`.

El Worker verifica la sesión y el rol estudiantil antes de entregar `modulos/agente/api-lector9.html` desde la rama principal de GitHub. Conserva cookies, `/api/agent`, `/api/tutor-progress` y Cloudflare D1. Se envía con la política de seguridad habitual y `Cache-Control: private, no-store`. No se introduce ninguna tabla nueva.

El botón de la misión de Inferencias abrirá directamente `/agente` en la versión web. La pestaña puede actualizarse sin volver a `about:blank`.

Cuando se utiliza una copia descargada de `index.html`, o si se pierde internet antes de abrir el tutor, la aplicación conserva el modo HTML autocontenido. Es una contingencia offline; esa pestaña temporal no es recargable.

## Secuencia segura de publicación
1. Guardar una copia del Worker actual en Cloudflare.
2. Incorporar la ruta `GET /agente` al Worker, preservando el código de usuarios, contraseñas, consultas de IA y tutorías. Se proporciona en el archivo completo `OVA_Worker_IA_Seguimiento_Ruta_Agente.txt` elaborado a partir de la última versión compartida.
3. Publicar primero el Worker y comprobar que `/agente` abre el tutor como estudiante, y que tras pulsar Actualizar sigue abierto.
4. Fusionar la rama `fix/agente-ruta-permanente-cloudflare` en `main`. Hasta entonces el OVA en producción sigue abriendo el tutor anterior con `about:blank`.
5. Verificar que el botón «Abrir tutor de inferencias» abre `/agente`, que la IA responde, que `/api/tutor-progress` sincroniza y que las notas oficiales permanecen intactas.

## Comprobaciones realizadas
- El Worker modificado pasó análisis sintáctico y pruebas simuladas de `GET /agente`: usuario estudiante válido (200), administrador (redirigido al panel) y visitante sin sesión (redirigido al acceso).
- El botón pasa pruebas simuladas de apertura web permanente y de los dos modos de respaldo HTML.
- No se modifican las cuentas, la puntuación, las estructuras de D1 ni el código original del agente.

**El Worker de Cloudflare no se modifica por actualizar GitHub.** La ruta seguirá sin existir hasta que se publique el código de Cloudflare.