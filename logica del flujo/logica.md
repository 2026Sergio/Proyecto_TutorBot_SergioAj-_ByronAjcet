# TutorBot – Sistema de Asesorías Académicas

## Descripción
TutorBot es una solución automatizada desarrollada en n8n para la gestión inteligente de tutorías académicas. El sistema permite que los estudiantes soliciten asesorías de forma autónoma a través de Telegram, validando la disponibilidad de tutores y materias en tiempo real mediante una base de datos centralizada en Google Sheets.

El flujo integra agentes de IA para procesar lenguaje natural, gestionar la lógica de asignación, verificar fechas y actualizar el estado de las tutorías automáticamente.

## Tecnologías Utilizadas
* **n8n:** Orquestador principal del flujo de trabajo y lógica de negocio.
* **Telegram Bot API:** Interfaz conversacional para el usuario.
* **Google Sheets:** Base de datos relacional para el almacenamiento y gestión de registros.
* **Google Gemini (AI Agent):** Motor de procesamiento para la toma de decisiones, consulta de datos y actualización de registros.

## Flujo de Trabajo (Workflow)
El sistema opera bajo un proceso estructurado en pasos:

1. **Inicio (Trigger):** El usuario inicia el bot en Telegram enviando un "Hola".
2. **Identificación (Switch):** Un nodo de `Switch` clasifica al usuario como Estudiante o Profesor basándose en su perfil.
3. **Menú Interactivo:** Dependiendo del perfil, el sistema despliega opciones dinámicas extraídas de las hojas de Google Sheets (`Estudiantes`, `Tutores`, `Materias`).
4. **Procesamiento Inteligente:**
   - El usuario ingresa la materia y la fecha deseada.
   - El **Agente de IA** interviene analizando la fecha proporcionada contra la hoja de `DISPONIBILIDAD`.
   - La IA realiza la búsqueda de tutores libres y, tras la selección, puede **modificar el estado** de la reserva directamente en la hoja de `TUTORIAS` (marcando como asignada/ocupada).
5. **Comunicación:** El sistema envía un mensaje de confirmación o actualización al usuario a través de Telegram.

## Estructura de la Base de Datos (Google Sheets)
El sistema utiliza las siguientes hojas para mantener la integridad de los datos:

* **TUTORES:** Catálogo de docentes y sus especialidades.
* **DISPONIBILIDAD:** Agenda de horarios libres y ocupados.
* **TUTORIAS:** Historial y estado de las sesiones (Solicitada, Asignada, Finalizada).
* **ESTUDIANTES:** Registro de usuarios autorizados.

## Instrucciones de Instalación
1. Clona este repositorio.
2. Importa el archivo `proyecto.json` en tu instancia de n8n.
3. Configura las credenciales de los nodos:
   - **Telegram Trigger:** Inserta tu Token de bot proporcionado por @BotFather.
   - **Google Sheets:** Conecta tu cuenta de Google y vincula los IDs de tus hojas de cálculo.
   - **Google Gemini:** Asegúrate de tener una API Key válida para que los agentes de IA funcionen correctamente.
4. Activa el workflow en n8n y comienza a interactuar con tu bot en Telegram.

---