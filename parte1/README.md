# Parte 1 — Entornos de Trabajo en Scala

## 0. Prerrequisitos del Sistema: Java JDK 17

Para garantizar la compatibilidad con Scala 2.12.21 y las herramientas de compilación (`sbt`), se requiere Java JDK 17 en Windows 11.

### Configuración e Incidencias Encontradas
1. **Conflicto inicial de versiones:** El sistema contaba previamente con OpenJDK 22, lo que impedía la correcta resolución de dependencias para Scala 2.12.
2. **Instalación de JDK 17:** Se instaló Oracle JDK 17.0.12 mediante su instalador oficial MSI.
3. **Aislamiento de entorno (`JAVA_HOME`):**
   - Para no alterar dependencias globales del sistema operativo ni desinstalar otras versiones, se configuró la variable de sistema `JAVA_HOME` apuntando a:
     `C:\Program Files\Java\jdk-17`
   - Se verificó que las llamadas directas a `%JAVA_HOME%\bin\java.exe` y `javac.exe` apunten con éxito a la versión 17.0.12.

### Evidencia de Verificación
![Verificación de Java 17](../images/jdk17-verificacion.png)

---

## 1. Entorno 1 — JupyterLab + Almond Kernel
*(En proceso de configuración...)*