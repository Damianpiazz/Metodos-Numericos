# Métodos Numéricos

Resolución computacional de los trabajos prácticos de la asignatura mediante notebooks de Jupyter. Cada notebook desarrolla un conjunto de enunciados con su formulación matemática, la implementación de los algoritmos correspondientes, la verificación numérica de los resultados y la representación gráfica de los procesos iterativos y de propagación de errores.

| Notebook | Contenido |
|---|---|
| `errores.ipynb` | Teoría de errores: método directo (enunciados 1 a 10) y método inverso (enunciados 1 a 5) |
| `raices.ipynb` | Búsqueda de raíces: bisección, falsa posición, Newton-Raphson y secante, con comparación convergencial |
| `sistemas-de-ecuaciones.ipynb` | Sistemas lineales: factorización $LU$, Jacobi, Gauss-Seidel, relajación (SOR) y análisis espectral |

## Requisitos previos

- Python 3.14.8 o superior, disponible en el `PATH` del sistema.
- Un intérprete de comandos. Las instrucciones siguientes se indican para PowerShell; en sistemas POSIX los nombres de los ejecutables carecen del sufijo `.ps1` y las rutas emplean `/` como separador.

## Configuración del entorno virtual

El proyecto se aísla en un entorno virtual propio de modo que las dependencias no se propagan al intérprete del sistema. Desde la raíz del repositorio:

```powershell
# 1. Crear el entorno virtual en .venv
python -m venv .venv

# 2. Activar el entorno
.\.venv\Scripts\Activate.ps1

# 3. Actualizar el gestor de paquetes
python -m pip install --upgrade pip
```

Si el intérprete bloquea la ejecución de scripts en Windows, se levanta la restricción para la sesión en curso antes de activar el entorno:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

## Instalación de dependencias

Con el entorno activo, las dependencias declaradas en `requirements.txt` se instalan con:

```powershell
python -m pip install -r requirements.txt
```

El manifiesto fija las versiones con las que se verificó la ejecución completa de los tres notebooks:

| Grupo | Paquetes |
|---|---|
| Bibliotecas numéricas y de visualización | `numpy` 2.5.4, `pandas` 3.1.0, `matplotlib` 3.11.2, `sympy` 1.14.0 |
| Ejecución de notebooks | `ipykernel` 7.4.0, `jupyterlab` 4.6.4, `nbconvert` 7.17.2 |

La correspondencia entre notebook y dependencias es la siguiente:

| Notebook | Dependencias |
|---|---|
| `errores.ipynb` | `numpy`, `pandas`, `matplotlib` |
| `raices.ipynb` | `numpy`, `pandas`, `matplotlib` |
| `sistemas-de-ecuaciones.ipynb` | `numpy`, `pandas`, `matplotlib`, `sympy` |

Los módulos `math` y `IPython` se distribuyen con el intérprete y con el kernel de Jupyter respectivamente, y no requieren instalación independiente.

Para regenerar el entorno desde cero en otra máquina, basta con repetir los pasos anteriores: la creación del entorno virtual y la instalación del manifiesto reproducen el estado verificado.

## Ejecución de los notebooks

### Interfaz interactiva

```powershell
python -m jupyter lab
```

El servidor abre el árbol de directorios en el navegador. Se selecciona el kernel **Python 3** (asociado a `.venv`) y se ejecutan las celdas en orden mediante *Run All*. Los notebooks están entregados con las salidas ya almacenadas, de modo que las tablas y las figuras son visibles sin necesidad de ejecutarlos.

### Ejecución por lotes

Para reejecutar un notebook de punta a punta y escribir las salidas en el propio archivo, sin pasar por la interfaz:

```powershell
python -m jupyter nbconvert --to notebook --execute --inplace errores.ipynb
python -m jupyter nbconvert --to notebook --execute --inplace raices.ipynb
python -m jupyter nbconvert --to notebook --execute --inplace "sistemas-de-ecuaciones.ipynb"
```

El tiempo límite de ejecución por celda se controla con `--ExecutePreprocessor.timeout`, expresado en segundos.

### Verificación del kernel

Para comprobar que el notebook apunta al entorno correcto:

```powershell
python -m jupyter kernelspec list
```

Si el entorno `.venv` no figura entre los kernels disponibles, se registra con:

```powershell
python -m ipykernel install --user --name python3 --display-name "Python 3"
```

## Estructura del repositorio

```
.
├── errores.ipynb                    # Trabajo práctico 1
├── raices.ipynb                     # Trabajo práctico 2
├── sistemas-de-ecuaciones.ipynb     # Trabajo práctico 3
├── requirements.txt                 # Dependencias fijadas
├── .gitignore                       # Reglas de exclusión de versionamiento
└── README.md                        # Este documento
```

## Notas sobre reproducibilidad

- Todos los cálculos numéricos se verifican en aritmética de doble precisión IEEE 754. Los resultados se expresan en notación científica con la cifra significativa correspondiente a la precisión de los datos de entrada.
- Las tablas de iteraciones y las figuras se generan íntegramente en celdas de código, de modo que su contenido es reproducible a partir de la ejecución secuencial del notebook.
- Las versiones de las dependencias están fijadas en `requirements.txt`; la actualización de cualquiera de ellas puede alterar los últimos decimales de las salidas, sin afectar a la validez de los desarrollos.
