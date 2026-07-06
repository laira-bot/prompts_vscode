# Guía de Creación y Desarrollo de Proyectos en VS Code con GitHub Copilot

Esta guía proporciona un flujo de trabajo estructurado para iniciar, configurar y desarrollar proyectos de software y ciencia de datos en Visual Studio Code utilizando GitHub Copilot (a través de Copilot Chat y sus comandos de barra diagonal /).

## 1. Flujo de Trabajo Sugerido (Paso a Paso)

Para garantizar que tu proyecto se construya sobre bases sólidas, sigue esta secuencia de pasos al iniciar con GitHub Copilot:
```
[Paso 1: Planificación] ──> [Paso 2: Inicialización (/new)] ──> [Paso 3: Configuración (/init)] ──> [Paso 4: Reglas (/create-instructions)] ──> [Paso 5: Desarrollo Iterativo]
```

### Paso 1: Definición del Alcance y Requisitos

Antes de escribir código o interactuar con la IA, define el objetivo del proyecto, el lenguaje de programación principal (ej. Python), las librerías clave y la arquitectura general.

### Paso 2: Inicialización de la Estructura (`/new`)

Utiliza Copilot Chat en la vista de chat o mediante el comando rápido para generar el andamiaje (scaffolding) de directorios y archivos iniciales del proyecto.

### Paso 3: Configuración del Entorno y Dependencias (`/init`)

Genera los archivos de configuración necesarios para el entorno virtual, dependencias (`requirements.txt`, `pyproject.toml`) o herramientas de contenedor (Docker).

### Paso 4: Establecimiento de Reglas del Proyecto (`/create-instructions`)

Crea un archivo de instrucciones personalizadas para que Copilot se ciña a tus estándares de codificación (como PEP 8, patrones de diseño específicos o manejo de excepciones).

### Paso 5: Desarrollo, Pruebas e Iteración

Usa el chat de Copilot en combinación con agentes de terminal (`@terminal`) y herramientas de espacio de trabajo (`@workspace`) para implementar las funciones paso a paso, escribir pruebas unitarias y documentar el código.

## 2. Instrucciones Clave de Copilot Chat

GitHub Copilot cuenta con comandos específicos diseñados para acelerar las fases tempranas del ciclo de desarrollo. A continuación se detallan los más importantes:

### 2.1 `/new` (o `/newNotebook`)

- **Objetivo:** Crear un nuevo espacio de trabajo, aplicación o archivo desde cero.
- **Cómo funciona:** Le indicas a Copilot qué tipo de aplicación deseas y este te sugerirá una estructura completa de carpetas y archivos. Puedes previsualizarlos y, con un solo botón (`Create Workspace`), Copilot los creará físicamente en tu disco y abrirá la nueva ventana de VS Code.
- **Ejemplo de uso:** `@workspace /new Un pipeline de procesamiento de datos en Python estructurado de forma modular.

### 2.2 `/init`

- **Objetivo:** Inicializar configuraciones específicas de herramientas, entornos de desarrollo o plantillas de frameworks.
- **Cómo funciona:** Ayuda a preparar el entorno de ejecución del proyecto. Puede generar configuraciones para Git (.gitignore), Docker (Dockerfile), linters, configuraciones de VS Code (.vscode/settings.json), entre otros.
- **Ejemplo de uso:** `@workspace /init Genera un archivo .gitignore para Python y un Dockerfile optimizado para desarrollo local.`

### 2.3 `/create-instructions` (o uso de archivos `.githubcopilot-instructions`)

- **Objetivo:** Definir directrices persistentes de estilo, diseño y arquitectura para que Copilot las respete en todas las respuestas dentro del repositorio.
- **Cómo funciona:** Genera o te ayuda a redactar un archivo (habitualmente `.githubcopilot-instructions` o guardado en `.github/copilot-instructions.md`) que actúa como contexto de sistema personalizado para tu espacio de trabajo.
- **Ejemplo de uso:** `/create-instructions Genera reglas que fuercen a que todo el código de Python siga estrictamente PEP 8, incluya docstrings descriptivos y use tipado estático (type hinting).`

## 3. PROMPT Maestro (Diseñador de Prompts)

Copia y pega este prompt en Copilot Chat (o en tu LLM preferido) para generar el prompt perfecto para `/new` o `/init` adaptado a tus necesidades específicas.

```
Actúa como un Ingeniero de Prompts experto en desarrollo de software y GitHub Copilot.

Tu objetivo es ayudarme a diseñar el prompt ideal de inicialización de proyecto para usar con los comandos '/new' o '/init' de Copilot en VS Code.

Para lograrlo, debes seguir estas reglas estrictas:
1. NO asumas ninguna información sobre mi proyecto (como el lenguaje, la arquitectura, la base de datos o las librerías a usar).
2. Hazme preguntas detalladas una por una o en un bloque organizado para recopilar todo el contexto necesario.
3. Las preguntas deben cubrir:
   - Objetivo principal del proyecto.
   - Lenguaje de programación, framework y versión preferida.
   - Patrón de arquitectura de software deseado (ej. modular, MVC, DDD, microservicios).
   - Estilo de código o estándares requeridos (ej. PEP 8 para Python).
   - Librerías clave o dependencias críticas.
   - Requisitos de entorno de desarrollo (ej. Docker, entorno virtual, soporte para Notebooks).
4. Una vez recopilada la información, entrégame dos outputs claros:
   - Opción A: Un prompt optimizado listo para usar con '/new' para crear el espacio de trabajo.
   - Opción B: Un prompt optimizado listo para usar con '/init' (o instrucciones complementarias) para configurar el entorno y dependencias.

Por favor, comienza haciéndome las preguntas necesarias de manera clara y directa.
```
## 4. Ejemplo Práctico con Información Mínima

A continuación, se simula cómo interactuar con el **Prompt Maestro** utilizando los requisitos mínimos para un proyecto de ciencia de datos.

### 4.1 Información Mínima Proporcionada por el Usuario

- **Objetivo:** Crear un pipeline básico de Machine Learning para entrenar un modelo de clasificación con el dataset Iris.
- **Lenguaje:** Python.
- **Restricciones de estilo:** Seguir estrictamente PEP 8.

### 4.2 Resultado generado por el Prompt Maestro (Prompts Optimizados para Copilot)

Basándose en la información mínima provista, el Prompt Maestro generaría las siguientes instrucciones para utilizar directamente en Copilot Chat:

#### A. Prompt optimizado para `@workspace /new` (Estructura del Proyecto)

**Instrucción para pegar en Copilot Chat:**
```
@workspace /new Crea un proyecto modular de Python para un pipeline de Machine Learning (clasificación con el dataset Iris). Estructura el proyecto con la siguiente arquitectura:
- Una carpeta 'src' que contenga módulos para:
  - 'data_ingestion.py' (para cargar los datos).
  - 'features.py' (para preprocesamiento y escalado).
  - 'model.py' (para entrenar y evaluar un modelo RandomForestClassifier).
- Una carpeta 'tests' para pruebas unitarias básicas.
- Un script principal 'main.py' en la raíz que orqueste todo el flujo.
Todo el código de Python debe seguir estrictamente la guía de estilo PEP 8, usar anotaciones de tipo (type hinting) y funciones documentadas.
```
#### B. Prompt optimizado para configuración con `/init` (Configuración de Entorno)
**Instrucción para pegar en Copilot Chat:**
```
@workspace /init Genera los archivos de configuración iniciales para este proyecto de Python:
1. Un archivo 'requirements.txt' que incluya las versiones estables más recientes de scikit-learn, pandas, numpy y pytest.
2. Un archivo '.gitignore' estándar optimizado para Python (que ignore .venv, __pycache__, .pytest_cache y archivos .pyc).
3. Una guía de estilo básica para el linter de VS Code en '.vscode/settings.json' que configure el formateador 'black' o 'autopep8' al guardar.
```
#### C. Prompt para generación de reglas persistentes (`/create-instructions`)

**Instrucción para pegar en Copilot Chat:**
```
/create-instructions Genera directrices para el desarrollo de este proyecto de Machine Learning. Especifica que todo código nuevo generado debe:
- Ser compatible con Python 3.10+.
- Cumplir con PEP 8.
- Implementar manejo de excepciones robusto, especialmente en la lectura de datos.
- Separar la lógica de negocio (entrenamiento del modelo) de la interfaz de consola o script principal.
```
