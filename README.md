# SpectraFlow 🌊
### Dispositivo de Medición de Caudal Portátil Basado en Tecnología Ultrasónica (Clamp-on)

SpectraFlow es un instrumento de medición industrial no invasivo diseñado para la monitorización, diagnóstico y control de flujo en tuberías de PVC. El sistema aprovecha el método de **Tiempo de Tránsito (Transit-Time)** para calcular el caudal con alta resolución, integrando capacidades de **Edge AI** y análisis espectral para el mantenimiento predictivo de sistemas hidráulicos (como la detección temprana de cavitación y anomalías de bombeo).

---

## 🏛 Contexto Académico
* **Institución:** Universidad Nacional Experimental Politécnica "Antonio José de Sucre" (UNEXPO)
* **Vicerrectorado:** Barquisimeto
* **Departamento:** Ingeniería Electrónica
* **Asignatura:** Trabajo Especial 1 (EL-5112)
* **Autor:** Alejandro David Silva Lucena
* **Tutor:** Ing. Elvis Morillo
* **Co-Tutor:** Ing. Lenin Becerra

---

## 🎯 Objetivos del Proyecto

### Objetivo General
Desarrollar un dispositivo portátil de medición de caudal no invasivo basado en tecnología ultrasónica transit-time y procesamiento embebido en la plataforma ESP32-S3 para el diagnóstico operativo de tuberías de PVC.

### Objetivos Específicos
1. Diseñar la etapa de hardware para el acondicionamiento de señal, incluyendo el circuito de excitación (pulser) de alta tensión y la etapa de amplificación de bajo ruido (LNA) para transductores piezoeléctricos.
2. Integrar el conversor de tiempo a digital de alta precisión (TDC-GP22) para la captura del Tiempo de Vuelo (Time-of-Flight) en el orden de los picosegundos.
3. Desarrollar el firmware modular del sistema utilizando el framework **ESP-IDF** bajo programación multitarea en tiempo real (FreeRTOS).
4. Implementar el motor de control y enrutamiento de eventos mediante el framework **ESP-Claw** para permitir la configuración dinámica y diagnóstico mediante scripts Lua.
5. Desarrollar los algoritmos matemáticos de procesamiento de señales para el cálculo de velocidad de fluido y compensación por número de Reynolds.
6. Validar experimentalmente la precisión del prototipo frente a patrones de medición volumétricos de referencia.

---

## ⚙️ Arquitectura Técnica

### 1. Hardware y Adquisición (Edge)
* **Unidad Central:** SoC ESP32-S3 (Módulo N16R8: 16 MB de memoria Flash, 8 MB de PSRAM) configurada con bus de datos Octal SPI (`qio_opi`) para la ejecución veloz de algoritmos de filtrado.
* **Núcleo de Medición:** Chip TDC-GP22 comunicado por interfaz SPI para la discriminación estricta de tiempos de llegada de los pulsos ultrasónicos (Upstream / Downstream).
* **Transductores:** Sensores piezoeléctricos externos acoplados en configuración no invasiva (*clamp-on*).

### 2. Software y Control Embebido
* **Sistema Operativo:** FreeRTOS (nativo en ESP-IDF) para la priorización de tareas críticas de medición frente a la pila de comunicaciones.
* **Capa Extensible:** Framework **ESP-Claw** embebido en el firmware, actuando como el motor de interfaz, persistencia de datos y máquina de estados interactiva.
* **Conectividad:** Servidor web local integrado para calibración en campo, monitorización en tiempo real y descarga de perfiles de flujo.

---

## 📂 Estructura Organizada del Repositorio

El espacio de trabajo se divide en aristas bien definidas para cumplir tanto con las entregas académicas IEEE como con las buenas prácticas de la ingeniería de software:

```text
SpectraFlow/
├── assets/             # Recursos visuales, esquemas de bloques, logotipos y mockups de la interfaz.
├── docs/               # Informes de avance de TE1, guías de diseño de software/hardware y plantillas de evaluación.
├── hardware/           # Archivos de diseño electrónico (esquemáticos, layout de PCB, diagramas de conexión).
└── firmware/           # 💻 ENTORNO DE DESARROLLO (Proyecto PlatformIO Autónomo)
    ├── .pio/           # Archivos temporales de compilación y toolchains (ignorado en Git).
    ├── include/        # Definiciones globales y archivos de cabecera (.h) del firmware.
    ├── lib/            # Bibliotecas de terceros aisladas.
    │   └── esp-claw/   # Núcleo del framework ESP-Claw integrado localmente.
    ├── src/            # Lógica principal del sistema en C (main.c, tareas FreeRTOS).
    └── platformio.ini  # Configuración maestra del hardware del ESP32-S3 y directivas CMake.