# 🧠 Asistente Orientador Universitario – n8n Workflow

Este repositorio contiene los archivos JSON del proyecto de automatización desarrollado en la plataforma **n8n**, cuyo objetivo es permitir que un **estudiante pueda conversar vía Telegram con un asistente inteligente orientativo**, que recopila y procesa sus datos para ayudarle en su proceso de orientación universitaria.

---

## 📌 Objetivo del Proyecto

El objetivo principal fue diseñar una experiencia conversacional guiada, capaz de recopilar la siguiente información del estudiante:

- Nombre  
- Edad  
- Ciudad de residencia  
- Vía de acceso a la universidad  
- Intereses  
- Asignaturas favoritas  
- Correo electrónico

---

## 🛠 Tecnologías Utilizadas

- **n8n** – Plataforma central de automatización basada en flujos.
- **Telegram Bot API** – Canal de entrada para el usuario.
- **Supabase** – Base de datos relacional para persistencia de datos.
- **Google Sheets** – Fuente auxiliar de datos estructurados (plazos, carreras, grupos).
- **LLM / Agentes de IA (OpenAI)** – Para extracción de contexto, clasificación semántica y generación de texto.
- **MongoDB (ChatMemory)** – Experimentación con memoria conversacional (fase de laboratorio).

---

## ⚙️ Estructura del Workflow

El flujo principal se basa en una **lógica de estados**, en la que cada mensaje recibido se clasifica como parte de una etapa secuencial:

1. Nombre  
2. Edad  
3. Ciudad  
4. Vía de acceso  
5. Intereses  
6. Asignaturas favoritas  
7. Email  

En cada paso, un **agente de IA** recibe el mensaje del estudiante junto con el estado actual, y se encarga de extraer el dato correspondiente. Una vez obtenido, se actualiza en Supabase. Si la información no puede ser identificada, se solicita al usuario que repita su respuesta.

---

## ✉️ Subworkflow de Generación de Correo (No implementado aun, es un evolutivo)

Una vez finalizada la conversación, se lanza un subworkflow que:

1. Recupera todos los datos del estudiante desde Supabase.
2. Utiliza **tres agentes de IA** para generar las siguientes secciones del correo:
   - Descripción de su grupo de acceso, basado en edad y vía.
   - Fechas clave de inscripción, según ciudad.
   - Sugerencias de carreras universitarias, basadas en intereses y asignaturas favoritas.
3. Une y formatea las secciones para crear un mensaje personalizado.
4. Envía el correo al estudiante.

---

## 🧪 Evolución del Proyecto

Este proyecto ha evolucionado a través de múltiples fases experimentales, en las que se exploraron y validaron diferentes estrategias:

- Uso inicial de sub-workflows para simular funciones (fallido por bucles).
- Exploración de formularios vs. chat libre.
- Experimentación con clasificación automática mediante LLM sin control de estado (fallaba en estabilidad).
- Implementación de memoria conversacional con MongoDB (útil, pero no viable a gran escala).
- Consolidación de lógica de estados + Supabase como estructura robusta.
- Creación de subworkflow modular con generación de contenido vía IA y clasificacion de mensajes en categorias

---

## 🧠 Aprendizajes y Valor Personal

Este proyecto ha representado una oportunidad para aprender de forma acelerada sobre:

- Modelado de flujos conversacionales complejos.
- Integración práctica de bases de datos en tiempo real.
- Diseño de sistemas de IA multi-agente aplicados a casos reales.
- Gestión de errores, optimización de recursos y validación semántica.

Gracias a esta experiencia, he pasado de tener una visión estructurada basada en programación clásica a desarrollar un enfoque más **fluido, reactivo y centrado en el usuario**, aprovechando al máximo las capacidades de n8n como entorno modular y visual.

---

## 📂 Contenido del Repositorio

- Memoria del Bot (Recomendado como primera lectura)
- `/jsons/` – Archivos exportados desde n8n, incluyendo el flujo principal y subworkflow del evolutivo. Se incluyen tambien archivos laboratorio_*.json mencionados en la memoria.
- `README.md` – Este documento.


---

## 🚀 Próximos Pasos

- Añadir autenticación para evitar duplicados o respuestas anónimas.
- Optimizar el uso de tokens para los agentes LLM.
- Diseñar un panel de administración para revisar los perfiles generados.
- Explorar una versión multilingüe del asistente.
- Generar un **correo electrónico personalizado** con información útil adaptada al perfil del usuario.


---

Gracias por tu interés y bienvenido/a a este asistente educativo automatizado creado con n8n.

