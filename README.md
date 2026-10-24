# Rutas de Lectura Crítica · Grado 9.º

OVA interactivo de Lengua Castellana para la **Institución Educativa San José del Pantano**, Puerto Escondido, Córdoba. Producto de la **Evidencia 3** de la Unidad 2 de la Maestría en Innovación Educativa con Tecnología e Inteligencia Artificial (MIETIA).

## Abrir y entregar
- **Archivo principal:** [index.html](./index.html). Descarga el archivo y ábrelo en un navegador moderno; funciona sin internet, pues incorpora la ilustración, las hojas de estilo, los datos y el JavaScript en el mismo HTML.
- **GitHub Pages:** si está habilitado, la página principal muestra el OVA. La publicación web requiere conectividad para abrirse normalmente; esto es distinto de la ejecución offline de la copia local.
- **Entrega en plataforma:** adjuntar `index.html`, no solamente un enlace, y añadir el resumen del prompt maestro ROCAS del archivo de documentación.

## Secuencia
1. Ideas principales: 3 lecturas originales y 9 preguntas.
2. Inferencias: 4 casos prácticos basados en dos lecturas y 4 preguntas.
3. Argumentación: 10 desafíos con 50 clasificaciones de tesis, razones y evidencias.
4. Reto integrador: 6 preguntas transversales.

**Evaluación:** 100 puntos posibles, distribuidos 30/30/30/10. El error no bloquea el recorrido, y cada decisión recibe una explicación. El avance puede guardarse localmente en el navegador. En la sección de resultados se ofrece un informe imprimible que puede guardarse como PDF.

## Acceso local y conexión con Cloudflare

- **OVA local o GitHub Pages:** funciona como recurso descargable, con respuestas y puntuaciones guardadas en el navegador.
- **OVA bajo el Worker de Cloudflare (ruta `/ova`):** requiere acceso de estudiante; lee y sincroniza el avance evaluable mediante `/api/state` y la base de datos D1 del Worker, si el servicio está desplegado y disponible. Esto no hace que la versión autenticada funcione sin conexión.
- **API Lector 9:** tutor socrático opcional en la misión Inferencias. Abre una pestaña generada desde el mismo `index.html`, con dos lecturas y cuatro casos; registra su propio avance localmente, sin modificar la puntuación del OVA ni enviar ese diálogo a D1. Es una interacción guiada por reglas, **no IA generativa**.

## Estructura
- `index.html` · OVA integrado y final
- `prototipos-originales/` · Los tres prototipos completos utilizados como antecedentes, mantenidos por separado.
- `documentacion/` · Trazabilidad pedagógica, prompt ROCAS y auditoría.
- `modulos/agente/api-lector9.html` · Copia autocontenida del tutor para pruebas y conservación.
- `modulos/agente/README.md` · Instrucciones y límites de API Lector 9.

## Tutor con IA socrática opcional

El tutor de la Misión 2 incorpora un cuadro de consulta libre a **Cloudflare Workers AI**. En el OVA descargado y si falla la red o el servicio, las actividades y la mediación socrática local permanecen disponibles. La IA se utiliza únicamente al conectarse al Worker con el binding de Workers AI habilitado; este cambio no está incluido automáticamente en GitHub. Véanse [instrucciones de activación](./cloudflare/ACTIVAR_IA_LECTOR9.md). Las respuestas generativas son preguntas orientadoras, sin puntuación ni acceso a las respuestas oficiales.

## Seguimiento independiente de API Lector 9

Las cuatro tutorías socráticas pueden registrarse por estudiante en Cloudflare D1, sin modificar los puntos ni las actividades oficiales. El panel mostrará los casos realizados y su avance en otra columna **después de desplegar el Worker actualizado**. Las tutorías antiguas de este navegador requieren importación voluntaria. Véase [guía de seguimiento](./cloudflare/SEGUIMIENTO_TUTORIAS_API_LECTOR9.md).

## Transparencia
Los textos argumentativos contienen ejemplos ficticios con fines didácticos. Los intentos de prueba no equivalen a resultados académicos obtenidos con estudiantes. El OVA contiene un tutor local por reglas y una integración opcional con un modelo de IA generativa en Cloudflare y no debe confundirse con el bot desconectado previsto en la tesis. En la versión local no se necesita servidor. En la ruta autenticada de Cloudflare, el sistema **sí transmite y almacena el progreso evaluable** asociado a la cuenta de estudiante; el diálogo del tutor se mantiene separado en el almacenamiento local del navegador. La operación real del Worker y sus políticas de conservación deben confirmarse en Cloudflare.
