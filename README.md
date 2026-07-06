
# Prompts para VS Code (Workflows Agénticos)

Este repositorio es una guía práctica para configurar y desplegar **entornos de trabajo agénticos** optimizados en VS Code, maximizando el uso de asistentes de IA y flujos de trabajo autónomos.

---

## 🛠️ Flujo de Implementación de un Proyecto

Para estructurar un nuevo proyecto utilizando este entorno agéntico, sigue este proceso paso a paso:

### 1. Definición de la Base Documental

Antes de interactuar con el agente, es fundamental establecer el contexto. Crea y define los siguientes archivos en la raíz de tu espacio de trabajo:

* 📂 `objetivos-proyecto.md`: Define el alcance, metas y entregables del desarrollo.
* 📂 `instrucciones-proyecto.md`: Detalla las reglas de negocio, dependencias y restricciones técnicas.

> 💡 **Guía de referencia:** Para redactar correctamente estos archivos, consulta la documentación detallada en [archivos-objetivos-especificaciones.md](archivos-objetivos-especificaciones.md).

---

### 2. Inicialización del Proyecto con el Agente

Una vez definidos los archivos de contexto, utiliza los comandos de barra diagonal (`/`) en la terminal o chat del asistente para estructurar el entorno:

1. **`/new`**: Utiliza este comando para indicarle al agente la creación del nuevo espacio.
2. **`/init`**: Inicializa la estructura de directorios y los archivos base del proyecto de forma automatizada.

> 📘 **Nota:** El comportamiento y la configuración de estos comandos se encuentran detallados en la guía de [archivos-objetivos-especificaciones.md](archivos-objetivos-especificaciones.md).

---

### 3. Generación de Instrucciones Específicas

Para tareas complejas o flujos de trabajo muy concretos dentro del desarrollo, puedes automatizar la creación de directivas adicionales:

* Utiliza el comando **`/create-instructions`** para generar pautas específicas que guíen al agente en tareas subsecuentes.

---

## 🚀 Buenas Prácticas

* Mantén los archivos de objetivos e instrucciones actualizados a medida que el proyecto evolucione.
* Asegúrate de que el agente tenga visibilidad completa del contexto de los archivos `.md` antes de ejecutar comandos de generación de código.
