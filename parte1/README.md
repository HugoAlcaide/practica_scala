# Parte 1 — Entornos de Trabajo en Scala[cite: 1]

## 0. Prerrequisitos del Sistema: Java JDK 17[cite: 1]

Para garantizar la compatibilidad con Scala 2.12.21 y las herramientas de compilación (`sbt`), se requiere Java JDK 17 en Windows 11.[cite: 1]

### Configuración e Incidencias Encontradas[cite: 1]
1. **Conflicto inicial de versiones:** El sistema contaba previamente con OpenJDK 22, lo que impedía la correcta resolución de dependencias para Scala 2.12.[cite: 1]
2. **Instalación de JDK 17:** Se instaló Oracle JDK 17.0.12 mediante su instalador oficial MSI.[cite: 1]
3. **Aislamiento de entorno (`JAVA_HOME`):**[cite: 1]
   - Para no alterar dependencias globales del sistema operativo ni desinstalar otras versiones, se configuró la variable de sistema `JAVA_HOME` apuntando a:[cite: 1]
     `C:\Program Files\Java\jdk-17`[cite: 1]
   - Se verificó que las llamadas directas a `%JAVA_HOME%\bin\java.exe` y `javac.exe` apunten con éxito a la versión 17.0.12.[cite: 1]

### Evidencia de Verificación[cite: 1]
![Verificación de Java 17](../images/jdk17-verificacion.png)[cite: 1]

---

## 1. Entorno 1 — JupyterLab + Almond Kernel + Scala 2.12.21

### 1.1 Descripción y Especificaciones del Entorno
Entorno interactivo tipo REPL basado en la web para experimentación ágil, prototipado y análisis de datos en Scala con Apache Spark.

* **Plataforma:** JupyterLab
* **Kernel JVM:** Almond
* **Versión de Scala fijada:** 2.12.21
* **Máquina virtual base:** Oracle JDK 17 (17.0.12)

---

### 1.2 Instalación de Componentes y Requisitos Previos

#### A. Instalación de JupyterLab
Aprovisionamiento del entorno web de cuadernos mediante el gestor `pip` de Python:

pip install jupyterlab

#### B. Aprovisionamiento de Almond mediante Coursier (`cs.exe`)
Almond es una aplicación basada en la JVM y no un paquete Python convencional. Se utilizó **Coursier**, el gestor oficial de dependencias y binarios de Scala, para descargar sus artefactos y registrarlo en Jupyter.

1. **Descarga del binario de Coursier:**
   Invoke-WebRequest -Uri "https://github.com/coursier/launchers/raw/master/cs-x86_64-pc-win32.exe" -OutFile "$env:TEMP\cs.exe"

2. **Compilación e inyección del kernel en Jupyter:**
   & "$env:TEMP\cs.exe" launch --fork almond --scala 2.12.21 -- --install

3. **Comprobación de registro de kernels:**
   jupyter kernelspec list

*Salida:* Se confirmó la presencia de la entrada `scala` bajo el directorio `%APPDATA%\jupyter\kernels\scala`.

---

### 1.3 Incidencias Técnicas y Resolución de Dependencias

* **Incidencia de resolución en Maven Central (`404 Not Found`):**  
  * **Problema:** Al ejecutar la instalación fijando una versión concreta de Almond mediante `almond:0.13.14 --scala 2.12.21`, Maven Central rechazó la petición por no existir un binario precompilado de esa versión de Almond para el parche específico `2.12.21` (`sh.almond:scala-kernel_2.12.21:0.13.14`).
  * **Solución aplicada:** Se ejecutó el aprovisionamiento delegando la resolución de la versión de Almond en Coursier con `--fork almond --scala 2.12.21`. Esto permitió compilar y descargar dinámicamente las librerías compatibles junto con el paquete oficial `scala-compiler-2.12.21.jar`.

---

### 1.4 Evidencias de Configuración y Ejecución

#### 1. JupyterLab y Kernel Almond Disponible
![JupyterLab Inicio](../images/jupyter-inicio.png)
![Launcher con Kernel Almond](../images/jupyter-almond.png)

#### 2. Ejecución del Cuaderno de Pruebas
Se creó el notebook [`parte1/notebook/entorno-scala.ipynb`](notebook/entorno-scala.ipynb) para validar la versión exacta y las operaciones básicas del lenguaje.

![Ejecución de Pruebas en Scala](../images/jupyter-scala-version.png)