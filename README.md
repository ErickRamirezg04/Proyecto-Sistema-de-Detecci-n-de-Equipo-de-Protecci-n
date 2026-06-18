# Sistema de Vision Artificial para la Auditoria Automatizada de Equipo de Proteccion Personal mediante YOLO

## Integrantes del Equipo
* **Erick Oswaldo Ramirez Gonzalez** - Registro: 23310402
* **Victor Habib Flores Alfaro** - Registro: 23310377

---

## 1. Objetivo del Proyecto
Aplicar conceptos de Vision Artificial mediante el entrenamiento de un modelo de la familia YOLO (You Only Look Once) para detectar en tiempo real si el personal operativo en entornos industriales porta correctamente su Equipo de Proteccion Personal (Casco de seguridad, Chaleco antirreflejante y Lentes de proteccion), mitigando riesgos de accidentes y automatizando auditorias de seguridad ocupacional.

---

## 2. Caso de Estudio: Implementacion en Entorno Real

### A. Problema a Resolver
En plantas manufactureras, de ensamble o zonas de construccion, el factor humano y la complacencia operativa derivan frecuentemente en omisiones criticas de seguridad, tales como ingresar a zonas de riesgo sin casco o chaleco. Las auditorias visuales realizadas por supervisores de seguridad (HSE) son intermitentes, costosas y propensas a errores por fatiga. 

La solucion propuesta consiste en un sistema automatizado de videovigilancia inteligente continuo que actue como un filtro de control de acceso y monitor de areas comunes, identificando infracciones en milisegundos y restringiendo el paso o emitiendo alertas fisicas antes de que ocurra un siniestro.

### B. Arquitectura de Hardware Propuesta
Para desplegar el modelo entrenado en la linea de produccion o accesos, se requiere la siguiente arquitectura fisica:

1. **Dispositivos de Captura (Camaras):** Camaras IP de grado industrial con resolucion Full HD (1080p) posicionadas a una altura de 2.5 metros con un angulo de inclinacion de 45 grados en los torniquetes de entrada y pasillos principales para asegurar una vista clara del cuerpo completo del trabajador.
2. **Unidad de Procesamiento Central (Edge Computing):** Servidor local capaz de procesar multiples flujos de video en tiempo real a mas de 30 FPS utilizando aceleracion de hardware (TensorRT).
3. **Hardware de Actuacion y Maquinaria:** Torniquetes electro-mecanicos de acceso equipados con relevadores de control de compuerta, y una interfaz de alerta visual/auditiva compuesta por una torreta de iluminacion industrial de tres estados (Verde/Rojo) y una bocina piezoelectrica instalada sobre el punto de control.

### C. Flujo de Funcionamiento del Sistema (Flujo de Trabajo)
El ciclo de ejecucion logica del sistema de vision artificial opera bajo el siguiente proceso secuencial:

1. **Fase de Aproximacion y Captura:** El trabajador se aproxima al torniquete de acceso para ingresar a la planta. La camara IP captura el flujo de video continuo y lo transmite al servidor Edge mediante una direccion de red privada bajo el protocolo RTSP.
2. **Fase de Inferencia e Identificacion:** El script de ejecucion en Python intercepta el frame del video en tiempo real, normaliza las dimensiones de la imagen y la procesa a traves de la red neuronal del modelo YOLO entrenado. El algoritmo genera mapas de caracteristicas y extrae las Bounding Boxes (Cajas delimitadoras), clasificando los objetos en las categorias definidas: Casco, Chaleco o Lentes.
3. **Fase de Logica de Validacion Colectiva:** Para cada objeto clasificado como Persona, el sistema verifica automaticamente que existan cajas delimitadoras de Casco y Chaleco superpuestas en el mismo espacio vectorial.
4. **Fase de Actuacion Fisica Automatica:**
   * **Escenario de Cumplimiento (Acceso Autorizado):** Si el modelo detecta la presencia de todos los elementos de seguridad requeridos asociados al cuerpo del trabajador, el software envia un pulso digital mediante pines GPIO al relevador del torniquete para desbloquear el paso e ilumina la torreta en color verde.
   * **Escenario de Infraccion (Acceso Denegado):** Si el modelo detecta a la persona pero identifica la ausencia de casco o chaleco, el torniquete permanece bloqueado mecanicamente. Simultaneamente, se activa la torreta en color rojo parpadeante junto a la alerta sonora, y el sistema envia de forma automatica una captura de pantalla con las cajas de infraccion marcadas via Webhook al canal de supervision de seguridad industrial.

---

## 3. Instrucciones de Ejecucion y Configuracion

Siga estos pasos para replicar el entorno de desarrollo y ejecutar la demostracion localmente:

### Prerrequisitos
* Python 3.9 o superior instalado.
* Tarjeta grafica dedicada (Opcional, para ejecucion optima por CUDA).

### Paso 1: Clonar el repositorio
```bash
git clone [https://github.com/TU_USUARIO/TU_REPOSITORIO.git](https://github.com/TU_USUARIO/TU_REPOSITORIO.git)
cd TU_REPOSITORIO
