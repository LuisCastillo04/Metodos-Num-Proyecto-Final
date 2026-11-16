# Proyecto final de Métodos Numéricos

Proyecto académico en Python que aplica métodos numéricos a dos problemas: la dinámica de poblaciones de conejos y zorros mediante el modelo de Lotka–Volterra, y la relación entre horas de estudio y puntaje de examen mediante regresión lineal. El desarrollo, los cálculos y las visualizaciones están en el notebook [final.ipynb](final.ipynb).

## Funcionalidades

### 1. Modelo presa–depredador de Lotka–Volterra

- Implementación del método de Runge–Kutta de cuarto orden (RK4) para sistemas de ecuaciones diferenciales, mediante `rk4_sistemas(t, f, y0)`.
- Simulación de las poblaciones de conejos (presas) y zorros (depredadores).
- Gráficas de las poblaciones frente al tiempo, diagramas de fase y campo de direcciones normalizado con la trayectoria calculada.

El sistema implementado es:

$$
\frac{dx}{dt}=\alpha x-\beta xy, \qquad
\frac{dy}{dt}=\delta xy-\gamma y
$$

Los parámetros del notebook son `alpha = 0.5`, `beta = 0.002`, `gamma = 0.3` y `delta = 0.001`, con intervalo temporal de 0 a 80 y paso `h = 0.1`.

**Condiciones iniciales:** la gráfica de poblaciones utiliza 40 conejos y 40 zorros. Después, el notebook recalcula la solución con 40 conejos y 20 zorros para los diagramas de fase y el campo de direcciones. Estos gráficos corresponden a condiciones iniciales distintas.

### 2. Horas de estudio y puntaje de examen

- Lectura de [student_scores.csv](student_scores.csv) con pandas: 11 observaciones y columnas `Hours` y `Scores`.
- Ajuste de una recta `Scores ≈ a + b × Hours` mediante mínimos cuadrados, implementado en `ajuste_minimos_cuadrados(x, y)` con operaciones de NumPy.
- Cálculo del error cuadrático medio (MSE) y del coeficiente de determinación R², este último mediante `r_2(x, y)`.
- Visualización de los datos y de la recta ajustada.

## Tecnologías y requisitos

| Tecnología | Uso |
| --- | --- |
| Python 3 | Lenguaje del notebook; verificado con Python 3.12.2, versión registrada en sus metadatos. |
| JupyterLab | Entorno propuesto para abrir y ejecutar `final.ipynb`. |
| NumPy | Arreglos, integración RK4 y cálculos del ajuste lineal. |
| pandas | Lectura y exploración del archivo CSV. |
| Matplotlib | Gráficas de poblaciones, diagramas de fase, campo de direcciones y regresión. |

Para instalar se necesita Python con `pip`, acceso a Internet para descargar las dependencias y Git si se utiliza la clonación. También se puede descargar el repositorio desde **Code → Download ZIP** en GitHub y descomprimirlo. Las versiones de las bibliotecas no están fijadas en un archivo de dependencias.

## Instalación y ejecución local

Los siguientes comandos están preparados para **Windows PowerShell**, con Python disponible como `python`:

```powershell
git clone https://github.com/LuisCastillo04/Metodos-Num-Proyecto-Final.git
cd Metodos-Num-Proyecto-Final
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install jupyterlab numpy pandas matplotlib
.\.venv\Scripts\python.exe -m jupyterlab final.ipynb
```

Si descargaste el ZIP, abre PowerShell en la carpeta descomprimida y comienza en `python -m venv .venv`. Si Windows reconoce el lanzador `py` en lugar de `python`, utiliza `py -3 -m venv .venv` para crear el entorno. Los comandos posteriores usan directamente el Python del entorno, sin necesidad de activarlo.

### Preparar la ruta del CSV antes de ejecutar

**El notebook conserva una ruta absoluta del equipo del autor** en la celda que define `filename`. Para ejecutar la regresión en tu equipo, reemplaza esa asignación por:

```python
filename = "student_scores.csv"
```

Mantén `student_scores.csv` en la misma carpeta que `final.ipynb` y abre JupyterLab desde esa carpeta, como en los comandos anteriores. Si guardas el CSV en otra ubicación, asigna su ruta a `filename`.

## Uso

1. Abre `final.ipynb` en JupyterLab y selecciona el kernel de Python del entorno creado.
2. Ajusta la ruta del CSV según la sección anterior.
3. Usa **Kernel → Restart Kernel and Run All Cells** para ejecutar todas las celdas en orden. El notebook depende de variables y funciones definidas en celdas anteriores.
4. Consulta las gráficas de Lotka–Volterra y, al final, los coeficientes, métricas y gráfica de la regresión.

Para experimentar con el modelo de poblaciones, modifica los parámetros, las condiciones iniciales o el intervalo y paso temporal en sus celdas correspondientes; hay dos bloques de condiciones iniciales. `rk4_sistemas` utiliza una malla temporal equiespaciada con al menos dos nodos.

Para probar otros datos de regresión, conserva las columnas numéricas `Hours` y `Scores` o adapta las líneas que las seleccionan. El ajuste necesita valores de `Hours` que no sean todos iguales; el cálculo de R² también requiere variación en `Scores`. El código no incorpora validación automática de estos casos.

### Resultados de referencia

Con las 11 observaciones del CSV incluido, la regresión produce aproximadamente:

| Resultado | Valor |
| --- | ---: |
| Intercepto `a` | -0.4992 |
| Pendiente `b` | 9.7832 |
| MSE | 26.0844 |
| R² | 0.9625 |

La recta resultante es `Scores ≈ -0.4992 + 9.7832 × Hours`. Estos valores describen el ajuste al conjunto de datos incluido; no establecen una relación causal ni garantizan resultados para otros datos.

## Estructura del repositorio

```text
Metodos-Num-Proyecto-Final/
├── README.md                                  # Descripción e instrucciones
├── final.ipynb                                # Implementación y visualizaciones
├── student_scores.csv                         # Datos de horas y puntajes
├── ActividadFinalMetodosNum.pdf                # Material académico de apoyo
└── Metodos_Numericos_Presentacion_Final.pdf    # Presentación del proyecto
```

El punto de entrada para trabajar con el proyecto es `final.ipynb`. Los PDF son documentos de apoyo y pueden consultarse directamente desde GitHub.
