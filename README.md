# Actividad 09 — Análisis del Dataset del Titanic

---

## Tabla de contenidos

- [Descripción del proyecto](#descripción-del-proyecto)
  - [Pipeline del análisis](#pipeline-del-análisis)
  - [Resultado principal](#resultado-principal)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Librerías utilizadas](#librerías-utilizadas)
- [Cómo ejecutar el proyecto](#cómo-ejecutar-el-proyecto)
  - [Opción A — Con `uv` (recomendado)](#opción-a--con-uv-recomendado)
  - [Opción B — Google Colab](#opción-b--google-colab)
  - [Opción C — Jupyter clásico (Anaconda / pip)](#opción-c--jupyter-clásico-anaconda--pip)
  - [Opción D — VS Code](#opción-d--vs-code)

---

## Descripción del proyecto

Este proyecto realiza un análisis del dataset clásico del Titanic con el objetivo de identificar qué características sociodemográficas determinaron la probabilidad de supervivencia de los pasajeros.

El análisis parte de dos hipótesis:

1. **Hipótesis de evacuación:** El protocolo "mujeres y niños primero" generó una tasa de supervivencia significativamente mayor en el sexo femenino y en los menores de edad.
2. **Hipótesis socioeconómica:** Los pasajeros de primera clase tuvieron mayor probabilidad de sobrevivir debido a la ubicación de sus camarotes respecto a la cubierta.

### Pipeline del análisis

El flujo de trabajo sigue un pipeline estándar de ciencia de datos:

| Paso | Descripción |
|------|-------------|
| 1 | Planteamiento del problema e hipótesis |
| 2 | Carga y exploración inicial del dataset |
| 3 | Limpieza de datos (nulos, duplicados) |
| 4 | Ingeniería de características (`FamilySize`, `IsAlone`, `AgeGroup`, `Title`) |
| 5 | Análisis con `groupby` por género, clase y grupo de edad |
| 6 | Conclusiones y validación de hipótesis |
| 7 | Exportación del dataset limpio a `titanic_clean.csv` |

### Resultado principal

El género fue el factor de mayor peso (mujeres: 74% de supervivencia vs. hombres: 18%), seguido por la clase del boleto (1ra clase: 62% vs. 3ra clase: 24%) y el grupo de edad (niños: 58%).

---

## Estructura del proyecto

```
ai-titanic-actividad09/
├── Quispe_Bartolo_Carlos_Martin_Actividad09.ipynb   # Notebook principal
├── titanic_clean.csv                                # Dataset exportado tras la limpieza
├── pyproject.toml                                   # Dependencias del proyecto (uv)
├── uv.lock                                          # Lockfile de versiones exactas
└── README.md
```

---

## Librerías utilizadas

Las dependencias están declaradas en `pyproject.toml` y requieren **Python 3.13 o superior**.

| Librería | Versión mínima | Uso en el proyecto |
|----------|---------------|--------------------|
| `pandas` | 3.0.3 | Carga, limpieza, transformación y análisis del dataset |
| `ipykernel` | 7.2.0 | Ejecución del notebook en entornos Jupyter / VS Code |

> El dataset del Titanic se descarga automáticamente desde una URL pública al ejecutar la primera celda del notebook, por lo que no se requiere descarga manual.

---

## Cómo ejecutar el proyecto

### Opción A — Con `uv` (recomendado)

`uv` es un gestor de entornos y dependencias para Python extremadamente rápido. Es el método recomendado porque lee el `pyproject.toml` y `uv.lock` para reproducir el entorno exacto.

**1. Instalar `uv`**

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Verifica la instalación:

```bash
uv --version
```

**2. Clonar o descomprimir el proyecto y navegar a la carpeta**

```bash
cd ai-titanic-actividad09
```

**3. Crear el entorno virtual e instalar dependencias**

```bash
uv sync
```

Esto crea automáticamente un entorno `.venv/` con las versiones exactas del `uv.lock`.

**4. Lanzar Jupyter y abrir el notebook**

```bash
uv run jupyter notebook
```

Se abrirá el navegador. Haz clic en `Quispe_Bartolo_Carlos_Martin_Actividad09.ipynb` y ejecuta las celdas con **Shift + Enter** o usando *Kernel → Restart & Run All*.

---

### Opción B — Google Colab

No requiere instalación local. Solo necesitas una cuenta de Google.

1. Ve a [colab.research.google.com](https://colab.research.google.com)
2. Selecciona **Archivo → Subir notebook** y sube el archivo `.ipynb`
3. Sube también `titanic_clean.csv` al panel lateral de archivos si quieres omitir el paso de exportación
4. Ejecuta todas las celdas con *Runtime → Run all*

> Las librerías `pandas` e `ipykernel` ya vienen preinstaladas en Colab, no se necesita instalar nada adicional.

---

### Opción C — Jupyter clásico (Anaconda / pip)

**Con Anaconda:**

```bash
conda create -n titanic-env python=3.13
conda activate titanic-env
conda install pandas jupyter
jupyter notebook
```

**Con pip:**

```bash
python -m venv .venv
source .venv/bin/activate        # Linux / macOS
.venv\Scripts\activate           # Windows

pip install pandas>=3.0.3 ipykernel>=7.2.0 jupyter
jupyter notebook
```

---

### Opción D — VS Code

1. Abre la carpeta del proyecto en VS Code
2. Instala la extensión **Jupyter** (Microsoft) si no la tienes
3. Abre el archivo `.ipynb` — VS Code lo mostrará como notebook
4. En la esquina superior derecha, selecciona el intérprete de Python de tu entorno (`.venv` si usaste `uv sync`)
5. Ejecuta las celdas con el botón ▶ o con **Shift + Enter**

> Si usaste `uv sync`, el entorno ya está en `.venv/`. VS Code lo detecta automáticamente al abrir la carpeta.
