# 🛡️ Sistema de Visión Artificial para la Auditoría Automatizada de Cascos de Seguridad mediante YOLO

## 👥 Integrantes del Equipo
* **Erick Oswaldo Ramirez Gonzalez** - Registro: 23310402
* **Victor Habib Flores Alfaro** - Registro: 23310377

---

## 🎯 1. Objetivo del Proyecto
Aplicar conceptos de Visión Artificial mediante el entrenamiento de un modelo de la familia YOLO (You Only Look Once) para detectar en tiempo real si el personal operativo en entornos industriales porta correctamente sus cascos de seguridad de acuerdo a los estandares, mitigando riesgos de accidentes y automatizando auditorías de seguridad ocupacional.

---

## 📊 2. Dataset Utilizado
Para el entrenamiento de este modelo se utilizó un conjunto de datos optimizado para la detección de elementos de seguridad industrial. Debido a las limitaciones de almacenamiento de GitHub para archivos de gran volumen, las imágenes originales no se encuentran alojadas directamente en este repositorio.

* **Dataset:** Safety Helmet Computer Vision Dataset (1,375 imágenes)
* **Origen:** [Roboflow Universe - v10](https://universe.roboflow.com/vega-n6rdu/safety-helmet-tsqdw/dataset/10)

### 📥 Instrucciones de descarga del Dataset:
1. Ingrese al enlace de Roboflow proporcionado arriba.
2. Haga clic en el botón **"Download Dataset"** (o "Export").
3. Seleccione el formato estrictamente como **YOLOv8**.
4. Elija la opción **"Download ZIP"** para guardarlo localmente o **"show code"** para obtener el snippet de descarga directa en Google Colab.

---

## 🏭 3. Caso de Estudio: Implementación en Entorno Real

### ⚠️ A. Problema a Resolver
En plantas manufactureras, de ensamble o zonas de construcción, el factor humano y la complacencia operativa derivan frecuentemente en omisiones críticas de seguridad, tales como ingresar a zonas de riesgo sin casco. Las auditorías visuales realizadas por supervisores de seguridad (HSE) son intermitentes, costosas y propensas a errores por fatiga. 

La solución propuesta consiste en un sistema automatizado de videovigilancia inteligente continuo que actúe como un filtro de control de acceso y monitor de áreas comunes, identificando infracciones en milisegundos y restringiendo el paso o emitiendo alertas físicas antes de que ocurra un siniestro.

### ⚙️ B. Arquitectura de Hardware Propuesta
Para desplegar el modelo entrenado en la línea de producción o accesos, se requiere la siguiente arquitectura física:

* **🎥 Dispositivos de Captura (Cámaras):** Cámaras IP de grado industrial con resolución Full HD (1080p) posicionadas a una altura de 2.5 metros con un ángulo de inclinación de 45 grados en los torniquetes de entrada y pasillos principales para asegurar una vista clara del cuerpo completo del trabajador.
* **🖥️ Unidad de Procesamiento Central (Edge Computing):** Servidor local capaz de procesar múltiples flujos de video en tiempo real a más de 30 FPS utilizando acelaración de hardware (TensorRT).
* **🚧 Hardware de Actuación y Maquinaria:** Torniquetes electro-mecánicos de acceso equipados con relevadores de control de compuerta, y una interfaz de alerta visual/auditiva compuesta por una torreta de iluminación industrial de tres estados (Verde/Rojo) y una bocina piezoeléctrica instalada sobre el punto de control.

### 🔄 C. Flujo de Funcionamiento del Sistema (Flujo de Trabajo)
El ciclo de ejecución lógica del sistema de visión artificial opera bajo el siguiente proceso secuencial:

1. **🚶‍♂️ Fase de Aproximación y Captura:** El trabajador se aproxima al torniquete de acceso para ingresar a la planta. La cámara IP captura el flujo de video continuo y lo transmite al servidor Edge mediante una dirección de red privada bajo el protocolo RTSP.
2. **🧠 Fase de Inferencia e Identificación:** El script de ejecución en Python intercepta el frame del video en tiempo real, normaliza las dimensiones de la imagen y la procesa a través de la red neuronal del modelo YOLO entrenado. El algoritmo genera mapas de características y extrae las Bounding Boxes (Cajas delimitadoras), clasificando los objetos en la categoria especifica.
3. **🔍 Fase de Lógica de Validación Colectiva:** Para cada objeto clasificado como Persona, el sistema verifica automáticamente que existan cajas delimitadoras de Casco superpuestas en el mismo espacio vectorial.
4. **⚡ Fase de Actuación Física Automática:**
   * ✅ **Escenario de Cumplimiento (Acceso Autorizado):** Si el modelo detecta la presencia de los elementos de seguridad requeridos asociados al cuerpo del trabajador, el software envía un pulso digital mediante pines GPIO al relevador del torniquete para desbloquear el paso e ilumina la torreta en color verde.
   * ❌ **Escenario de Infracción (Acceso Denegado):** Si el modelo detecta a la persona pero identifica la ausencia de casco, el torniquete permanece bloqueado mecánicamente. Simultáneamente, se activa la torreta en color rojo parpadeante junto a la alerta sonora, y el sistema envía de forma automática una captura de pantalla con las cajas de infracción marcadas vía Webhook al canal de supervisión de seguridad industrial.

---

## 🚀 4. Instrucciones de Ejecución y Configuración

Siga estos pasos para replicar el entorno de desarrollo y ejecutar la demostración localmente:

### 📌 Prerrequisitos
* Python 3.9 o superior instalado.
* Tarjeta gráfica dedicada (Opcional, para ejecución óptima por CUDA).

### 🛠️ Paso 1: Clonar el repositorio
```bash
git clone [https://github.com/ErickRamirezg04/Proyecto-Sistema-de-Detecci-n-de-Equipo-de-Protecci-n.git](https://github.com/ErickRamirezg04/Proyecto-Sistema-de-Detecci-n-de-Equipo-de-Protecci-n.git)
```

### 📦 Paso 2: Instalar dependencias necesarias
```bash
pip install -r requirements.txt
```
