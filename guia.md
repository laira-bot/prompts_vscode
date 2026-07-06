
# Guía Técnica: Automatización del Ciclo de Vida del Proyecto con GitHub Copilot en VS Code

Esta guía proporciona el flujo de trabajo secuencial y avanzado para inicializar, estructurar, desarrollar y gobernar un proyecto de software utilizando las capacidades de agente y comandos de barra diagonal (`/`) en GitHub Copilot para VS Code.

---

## Flujo de Trabajo Secuencial

```text
[1. /new] ─────────> [2. /init] ─────────> [3. Modo Plan] ─────────> [4. /create-instructions]
Scaffolding          Gobernanza            Lógica de Negocio         Especialización
Inicial              Global (.github)      @workspace (Agente)       Subcarpetas (applyTo)

```

---

## 1. `/new` | Generación de la Estructura Base (Scaffolding)

El comando `/new` en Copilot Chat permite estructurar un proyecto completo desde cero, generando directorios y archivos de configuración iniciales basados en un stack tecnológico específico.

### Propósito Técnico

Configurar el esqueleto (*scaffolding*) del proyecto evitando la creación manual de directorios y la configuración repetitiva de archivos base (`README.md`, `.gitignore`, `requirements.txt`, etc.).

### Ejemplo de Prompt para Copilot Chat

```text
/new Crea un proyecto de Ciencia de Datos en Python utilizando POO y PEP 8. Debe incluir una carpeta 'src' con subcarpetas para 'data_ingestion', 'models' y 'utils', una carpeta 'tests' con la configuración de pytest, un archivo 'main.py' como punto de entrada, un '.gitignore' para Python y un 'requirements.txt' con dependencias clave como pandas, scikit-learn y mlflow.

```

---

## 2. `/init` | Establecimiento de la Gobernanza y Reglas Globales

Una vez generada la estructura, el comando `/init` en Copilot Chat se utiliza para inicializar configuraciones del entorno de desarrollo y reglas globales que guiarán el comportamiento de la IA y el equipo.

### Propósito Técnico

Crear el archivo de configuración global de Copilot (`.github/copilot-instructions.md`) o configuraciones del espacio de trabajo (`.vscode/settings.json`), asegurando que cualquier interacción posterior respete el stack, idioma y estándares definidos.

### Ejemplo de Prompt para Copilot Chat

```text
/init Genera un archivo de gobernanza global para el espacio de trabajo en .github/copilot-instructions.md. Especifica que el idioma oficial del código y documentación es inglés, que todo el código Python debe cumplir estrictamente con PEP 8, que se prefiere la programación funcional sobre el estado mutable cuando sea posible, y que todas las funciones deben incluir type hints y docstrings en formato Google.

```

---

## 3. Agente en Modo Plan (`@workspace`) | Desarrollo Estructurado de la Lógica de Negocio

El **Modo Plan** de GitHub Copilot (activado mediante `@workspace` en la interfaz de chat de tipo Agente) divide la ejecución del código en dos fases críticas: **Planificación** y **Ejecución**.

### Flujo de Aprobación y Ejecución

1. **Fase de Planificación:** El agente analiza el espacio de trabajo (`@workspace`), interpreta el requerimiento y propone una lista secuencial de cambios detallando qué archivos se crearán o modificarán.
2. **Revisión del Usuario:** El desarrollador evalúa el plan propuesto, solicita ajustes si es necesario y otorga su aprobación explícita.
3. **Fase de Ejecución:** Con la aprobación dada, el agente procede a implementar el código de manera iterativa, aplicando refactorizaciones y solicitando confirmación al finalizar el bloque de tareas.

### Ejemplo de Prompt para el Agente (`@workspace`)

```text
@workspace En modo plan, diseña e implementa el módulo de 'data_ingestion' en 'src/data_ingestion/'. Necesito una clase 'DataDownloader' que descargue archivos CSV desde una URL, maneje excepciones de conexión mediante reintentos exponenciales y guarde el archivo en 'data/raw/'. Muestra primero el plan de archivos antes de escribir el código.

```

---

## 4. `/create-instructions` | Segmentación y Especialización mediante `applyTo`

Para proyectos de gran envergadura, las reglas globales no son suficientes. El comando `/create-instructions` genera archivos `.copilot-instructions.md` específicos para directorios determinados dentro del repositorio.

### El Campo `applyTo` y Glob Patterns

El poder de esta característica radica en el campo `applyTo`, el cual utiliza **Glob Patterns** (patrones de coincidencia de rutas) para restringir el contexto y las reglas de Copilot a subcarpetas específicas. Esto evita que reglas de un dominio contaminen a otro (por ejemplo, reglas de frontend afectando al backend).

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

## Resumen de Comandos y Herramientas

| Comando / Modo | Fase del Proyecto | Salida Principal |
| --- | --- | --- |
| `/new` | Inicialización | Estructura de directorios y archivos base del proyecto. |
| `/init` | Configuración | Archivo de gobernanza global (`.github/copilot-instructions.md`). |
| `@workspace` (Modo Plan) | Desarrollo Activo | Implementación guiada, iterativa y segura de la lógica de negocio. |
| `/create-instructions` | Optimización / Escala | Reglas contextuales por carpeta (`applyTo`) con *Glob Patterns*. |

```

```
