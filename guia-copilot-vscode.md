# Guía Técnica: Automatización del Ciclo de Vida del Proyecto con GitHub Copilot en VS Code

Esta guía unifica el flujo de trabajo secuencial y avanzado para inicializar, estructurar, desarrollar y gobernar un proyecto de software o ciencia de datos utilizando las capacidades de agente y comandos de barra diagonal (`/`) en GitHub Copilot para VS Code, junto con plantillas de prompts listas para usar en cada fase.

---

## Flujo de Trabajo Secuencial

```text
[0. Planificación] ──> [1. /new] ─────────> [2. /init] ─────────> [3. Modo Plan] ─────────> [4. /create-instructions]
Alcance y            Scaffolding          Gobernanza            Lógica de Negocio         Especialización
Requisitos           Inicial              Global (.github)      @workspace (Agente)       Subcarpetas (applyTo)
```

### Paso 0: Definición del Alcance y Requisitos

Antes de escribir código o interactuar con la IA, define el objetivo del proyecto, el lenguaje de programación principal (ej. Python), las librerías clave y la arquitectura general. Si ya cuentas con documentos de contexto (`objetivos-proyecto.md`, `especificaciones-proyecto.md`), consulta [archivos-objetivos-especificaciones.md](archivos-objetivos-especificaciones.md) para integrarlos al flujo.

---

## 1. `/new` | Generación de la Estructura Base (Scaffolding)

El comando `/new` en Copilot Chat permite estructurar un proyecto completo desde cero, generando directorios y archivos de configuración iniciales basados en un stack tecnológico específico.

### Propósito Técnico

Configurar el esqueleto (*scaffolding*) del proyecto evitando la creación manual de directorios y la configuración repetitiva de archivos base (`README.md`, `.gitignore`, `requirements.txt`, etc.).

### Cómo funciona

Le indicas a Copilot qué tipo de aplicación deseas (puede invocarse también como `/newNotebook` para notebooks) y este te sugerirá una estructura completa de carpetas y archivos. Puedes previsualizarlos y, con un solo botón (`Create Workspace`), Copilot los creará físicamente en disco y abrirá la nueva ventana de VS Code.

### Ejemplo de Prompt para Copilot Chat

```text
@workspace /new Crea un proyecto de Ciencia de Datos en Python utilizando POO y PEP 8. Debe incluir una carpeta 'src' con subcarpetas para 'data_ingestion', 'models' y 'utils', una carpeta 'tests' con la configuración de pytest, un archivo 'main.py' como punto de entrada, un '.gitignore' para Python y un 'requirements.txt' con dependencias clave como pandas, scikit-learn y mlflow.
```

---

## 2. `/init` | Establecimiento de la Gobernanza y Reglas Globales

Una vez generada la estructura, el comando `/init` en Copilot Chat se utiliza para inicializar configuraciones del entorno de desarrollo y reglas globales que guiarán el comportamiento de la IA y el equipo.

### Propósito Técnico

Crear el archivo de configuración global de Copilot (`.github/copilot-instructions.md`) o configuraciones del espacio de trabajo (`.vscode/settings.json`), asegurando que cualquier interacción posterior respete el stack, idioma y estándares definidos.

### Cómo funciona

Ayuda a preparar el entorno de ejecución del proyecto: puede generar configuraciones para Git (`.gitignore`), Docker (`Dockerfile`), linters y ajustes de VS Code, entre otros.

### Ejemplo de Prompt para Copilot Chat

```text
@workspace /init Genera un archivo de gobernanza global para el espacio de trabajo en .github/copilot-instructions.md. Especifica que el idioma oficial del código y documentación es inglés, que todo el código Python debe cumplir estrictamente con PEP 8, que se prefiere la programación funcional sobre el estado mutable cuando sea posible, y que todas las funciones deben incluir type hints y docstrings en formato Google.
```

---

## 3. Agente en Modo Plan (`@workspace`) | Desarrollo Estructurado de la Lógica de Negocio

El **Modo Plan** de GitHub Copilot (activado mediante `@workspace` en la interfaz de chat de tipo Agente) divide la ejecución del código en dos fases críticas: **Planificación** y **Ejecución**.

### Flujo de Aprobación y Ejecución

1. **Fase de Planificación:** el agente analiza el espacio de trabajo (`@workspace`), interpreta el requerimiento y propone una lista secuencial de cambios detallando qué archivos se crearán o modificarán.
2. **Revisión del Usuario:** el desarrollador evalúa el plan propuesto, solicita ajustes si es necesario y otorga su aprobación explícita.
3. **Fase de Ejecución:** con la aprobación dada, el agente procede a implementar el código de manera iterativa, aplicando refactorizaciones y solicitando confirmación al finalizar el bloque de tareas.

### Ejemplo de Prompt para el Agente (`@workspace`)

```text
@workspace En modo plan, diseña e implementa el módulo de 'data_ingestion' en 'src/data_ingestion/'. Necesito una clase 'DataDownloader' que descargue archivos CSV desde una URL, maneje excepciones de conexión mediante reintentos exponenciales y guarde el archivo en 'data/raw/'. Muestra primero el plan de archivos antes de escribir el código.
```

---

## 4. `/create-instructions` | Segmentación y Especialización mediante `applyTo`

Para proyectos de gran envergadura, las reglas globales no son suficientes. El comando `/create-instructions` genera archivos de instrucciones (`.instructions.md` / `.copilot-instructions.md`) específicos para directorios determinados dentro del repositorio.

### Propósito Técnico

Definir directrices persistentes de estilo, diseño y arquitectura que Copilot respeta solo dentro del alcance indicado, evitando que reglas de un dominio contaminen a otro (por ejemplo, reglas de frontend afectando al backend).

### El Campo `applyTo` y Glob Patterns

| Glob Pattern | Significado Técnico | Caso de Uso |
| --- | --- | --- |
| `src/models/**` | Aplica a cualquier archivo o subcarpeta dentro de `src/models/`. | Reglas de entrenamiento de modelos ML. |
| `tests/**/*.py` | Aplica a todos los archivos `.py` dentro de la carpeta `tests/`. | Reglas de aserciones y mocks para testing. |
| `src/utils/*.py` | Aplica únicamente a archivos `.py` en la raíz de `src/utils/` (sin recursividad). | Estándares de funciones utilitarias puras. |

### Ejemplo de Prompt para Copilot Chat

```text
/create-instructions Genera un archivo de instrucciones específico para la carpeta 'src/models/'. Usa el campo 'applyTo' configurado para 'src/models/**'. Las reglas deben exigir que cualquier modelo de Machine Learning implementado use tracking de experimentos con MLflow, valide las dimensiones de los tensores/matrices de entrada mediante aserciones, y maneje semillas aleatorias (random_state) fijas para garantizar la reproducibilidad.
```

---

## 5. PROMPT Maestro (Diseñador de Prompts)

Cuando no tengas claro cómo formular el prompt ideal para `/new` o `/init`, copia y pega este meta-prompt en Copilot Chat (o en tu LLM preferido) para que te guíe con preguntas antes de generar el resultado final.

```text
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

### Ejemplo Práctico con Información Mínima

A continuación, se simula cómo interactuar con el Prompt Maestro utilizando los requisitos mínimos para un proyecto de ciencia de datos.

**Información mínima proporcionada por el usuario:**

- **Objetivo:** crear un pipeline básico de Machine Learning para entrenar un modelo de clasificación con el dataset Iris.
- **Lenguaje:** Python.
- **Restricciones de estilo:** seguir estrictamente PEP 8.

**Resultado generado por el Prompt Maestro:**

#### A. Prompt optimizado para `@workspace /new` (Estructura del Proyecto)

```text
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

```text
@workspace /init Genera los archivos de configuración iniciales para este proyecto de Python:
1. Un archivo 'requirements.txt' que incluya las versiones estables más recientes de scikit-learn, pandas, numpy y pytest.
2. Un archivo '.gitignore' estándar optimizado para Python (que ignore .venv, __pycache__, .pytest_cache y archivos .pyc).
3. Una guía de estilo básica para el linter de VS Code en '.vscode/settings.json' que configure el formateador 'black' o 'autopep8' al guardar.
```

#### C. Prompt para generación de reglas persistentes (`/create-instructions`)

```text
/create-instructions Genera directrices para el desarrollo de este proyecto de Machine Learning. Especifica que todo código nuevo generado debe:
- Ser compatible con Python 3.10+.
- Cumplir con PEP 8.
- Implementar manejo de excepciones robusto, especialmente en la lectura de datos.
- Separar la lógica de negocio (entrenamiento del modelo) de la interfaz de consola o script principal.
```

---

## Resumen de Comandos y Herramientas

| Comando / Modo | Fase del Proyecto | Salida Principal |
| --- | --- | --- |
| `/new` | Inicialización | Estructura de directorios y archivos base del proyecto. |
| `/init` | Configuración | Archivo de gobernanza global (`.github/copilot-instructions.md`). |
| `@workspace` (Modo Plan) | Desarrollo Activo | Implementación guiada, iterativa y segura de la lógica de negocio. |
| `/create-instructions` | Optimización / Escala | Reglas contextuales por carpeta (`applyTo`) con *Glob Patterns*. |

> Ver también [instrucciones-y-prompts-para-agentes.md](instrucciones-y-prompts-para-agentes.md) para la diferencia detallada entre `/init` y `/create-instructions`, y [creacion-objetivos-especificaciones-proyecto.md](creacion-objetivos-especificaciones-proyecto.md) para plantillas de documentos de contexto previos.
