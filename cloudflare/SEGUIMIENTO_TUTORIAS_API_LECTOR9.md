# Seguimiento de tutorías API Lector 9 en Cloudflare D1

## Propósito
El panel administrativo mostrará, por separado, las calificaciones oficiales del OVA y las **4 tutorías de la Misión 2**. Cada caso tiene 5 estados (0, 25, 50, 75 y 100 %) y se considera terminado cuando llega a 100 %. Este indicador **no es una calificación** ni acredita corrección semántica.

## Componentes
- **Frontend**: `modulos/agente/api-lector9.html` e instancia incrustada dentro de `index.html`, en `main` después de integrar estos cambios.
- **Backend Cloudflare**: requiere actualizar el código del Worker actualmente publicado. Una actualización de GitHub por sí sola no añade rutas a Cloudflare.
- **D1**: tabla separada `tutor_case_progress(user_id,case_id,stage,updated_at)`, creada por el Worker cuando se utiliza por primera vez. No se modifica `progress` ni `student_state`.
- **Rutas**: `GET /api/tutor-progress` (identidad y etapas del estudiante), `POST /api/tutor-progress` (registra una etapa), `GET /students/tutorias?id=N` (detalle exclusivo del administrador).
- **Panel**: columna «Tutorías API Lector 9» con cantidad completada, porcentaje global y «Ver casos».

## Protección de cuentas
La ruta comprueba sesión y rol; el estudiante nunca decide su propio ID. Solo se envían número de caso y etapa, sin texto de respuestas, preguntas a IA, PIN ni datos personales. Las tutorías se guardan bajo una clave local diferente por estudiante cuando hay sesión. Los registros locales previos a esta mejora eran compartidos en el navegador: se pueden importar a la cuenta actual **únicamente pulsando «Importar mis tutorías anteriores» y confirmando**. No importarlos si pertenecen a otra persona.

## Activación
1. Abrir Cloudflare → Workers & Pages → Worker del OVA → Edit code.
2. Hacer copia de seguridad del Worker que está publicado. Contrastar con el archivo completo actualizado proporcionado en el chat: `OVA_Worker_con_IA_y_SEGUIMIENTO_TUTORIAS.txt`, construido a partir del último código del Worker aportado por el usuario con las funciones de PIN, registro y Workers AI.
3. Sustituir el Worker **únicamente si el código actual coincide con esa base**; si hubo otros cambios, integrar los bloques relacionados con `tutor_case_progress` conservando dichos cambios.
4. Desplegar y, como estudiante, abrir el OVA → Inferencias → API Lector 9; se realizará la sincronización de nuevas etapas cuando haya internet.
5. Para datos anteriores a la integración: pulsar «Importar mis tutorías anteriores» solo desde la cuenta de quien hizo los ejercicios.
6. Regresar al administrador → estudiantes → «Tutorías API Lector 9» → «Ver casos». Si un estudiante usa el HTML descargado sin iniciar sesión, su progreso seguirá local hasta que se identifique y lo importe o vuelva a usar el OVA en línea.

## Verificación y reversión
- Completar caso 1 y caso 2 como estudiante: panel muestra `2/4 casos`; promedio y actividades oficiales permanecen intactos.
- Sin conexión: el tutor funciona, pero no aparece el avance en el panel hasta que se recupere la conexión y sincronice.
- Probar cambio de PIN, creación y eliminación de usuarios, y acceso al panel después de publicar.
- Si el Worker genera errores: restaurar la versión anterior de Cloudflare; no borrar las tablas D1.

**No se ha desplegado ni probado el Worker en Cloudflare desde la integración GitHub.**