# Taller Práctico 01 — Centauros

**Curso:** Fundamentos en Ciencia de Datos — Maestría en Ciencia de Datos y Analítica, EAFIT

**Conjunto de datos elegido:** C - Movilidad

**Fecha límite de entrega:** lunes 27 de julio de 2026

**Fecha de entrega real:** 27/07/2026

**Integrantes del equipo:**

| Nombre completo              | Cédula         |
| ---------------              | -------------- |
| Delvin José Rodriguez Jimenez| 1236422        |
| John Esteban Úsuga Duarte    | 1038926380     |
| Nathaly Ramirez Henao        | 1025641821     |

---

## 1. Resumen ejecutivo (máx. 8 líneas)

Se respondió a la pregunta de **¿Cuál es la probabilidad de que un sensor detecte alta frecuencia de autos dada una combinacion de clima, horas pico y no pico, y vía?**. Se encontraron patrones comportamentales respecto a la cantidad de vehículos según las horas y el clima de los sensores instalados en vías de la ciudad de Medellín. Se observa que, independientemente del sensor escogido, se genera congestión vehicular/aumenta la cantidad de vehículos detectados entre las horas de mayor actividad en la ciudad (6-9, 15 - 17).  A partir de esta información, se podría recomendar a organizaciones públicas responsables del tráfico en Medellín, tomar decisiones que mitiguen las congestiones (reorganización y planeación en vías, categorización de vehículos permitidos según el día, etc.)

## 2. Pregunta de negocio

- **Pregunta ancla del conjunto de datos:** ¿En qué corredores y horarios se debe pilotear semaforización inteligente?
- **Pregunta específica que su equipo decidió responder:** ¿Cuál es la probabilidad de que un sensor detecte alta frecuencia de autos dada una combinacion de clima, horas pico y no pico, y vía?

## 3. Estructura del repositorio

```
.
├── README.md
├── data/
│   ├── raw/                  # datos originales (sin modificar)
│   └── processed/            # datos ya limpios, generados por el notebook
├── notebooks/
│   └── taller_practico_01_analisis.ipynb
├── src/                      # funciones auxiliares (opcional)
├── results/
│   ├── figuras/
│   └── tabla_diagnostico_gigo.csv
└── docs/
    └── declaracion_uso_IA.md
```

## 4. Cómo reproducir el análisis (Solamente vía terminal)

```bash
# 1. Clonar el repositorio
git clone https://github.com/Nath-Ramirez/Challenge01_FundCienciaDatos.git
cd Challenge01_FundCienciaDatos

# 2. Crear entorno e instalar dependencias
pip install -r requirements.txt

# 3. Ejecutar el notebook de inicio a fin
jupyter notebook notebooks/taller_practico_01_analisis.ipynb
```

## 5. Principales hallazgos

| #   | Hallazgo | Evidencia (tabla/figura) |
| --- | -------- | ------------------------ |
| 1   | Valores faltantes      |  Antes: <img width="441" height="208" alt="image" src="https://github.com/user-attachments/assets/a0e28bf2-66ec-467e-bbfc-872b49622e0d" /><br />Despues: <img width="548" height="226" alt="image" src="https://github.com/user-attachments/assets/79d90da2-2dfc-484a-8565-c705a5b4d3c6" />
| 2   | Rangos y valores imposibles      |  Antes: <img width="1033" height="377" alt="image" src="https://github.com/user-attachments/assets/7f5a5dfd-250d-4a5b-ba9d-e10d5c2a8e5d" /><br/><img width="870" height="558" alt="image" src="https://github.com/user-attachments/assets/09cdb28e-e6f6-4cb6-a1c4-bf03e782953f" /><br/>Despues: <img width="1019" height="379" alt="image" src="https://github.com/user-attachments/assets/328c5dce-05e1-44bf-9cae-1b1dbac437fc" /><br/><img width="860" height="558" alt="image" src="https://github.com/user-attachments/assets/798f24fb-dd47-4d4f-8156-91d9856bcf27" />
| 3   | Formatos de fechas variables         | Antes: <img width="548" height="368" alt="image" src="https://github.com/user-attachments/assets/2a4e83be-b417-480b-85dc-d0671081aa79" /><br/>Despues:<img width="574" height="168" alt="image" src="https://github.com/user-attachments/assets/8a3553dd-d433-4b74-9660-f6265a9f4fff" />

## 6. Problemas de calidad de datos encontrados (resumen GIGO)

<img width="1225" height="658" alt="image" src="https://github.com/user-attachments/assets/f7c33b18-ced4-43ab-9236-e637fe6ed5fe" />


*(Tabla completa en `results/tabla_diagnostico_gigo.csv`)*

## 7. Decisión recomendada

- **Recomendación:** Tomar los datos de tiempo, clima y ubicación que los sensores extraen, los cuales muestran en mayor medida el comportamiento de los vehículos en distintas avenidas, la frecuencia de estos según el tipo de clima (tener en cuenta vehículos como motocicletas, por ejemplo), y las congestiones que se dan en horas de la mañana y tarde. A partir de esta información, por ejemplo, organizaciones públicas responsables del tráfico en Medellín podrían tomar decisiones que mitiguen las congestiones (Reorganización y planeación en vías, categorización de vehículos permitidos según el día, etc.)

  La calidad de la decisión está basada mayoritariamente por la cantidad de datos obtenidos y su alcance, límites los cuales serán explicados posteriormente.

- **Costo de un Falso Positivo:** Se predice alta congestión (se activa una intervención), pero no ocurre.

  La organizacion encargada podria tomar decisiones que no atacarian el problema, como una movilización innecesaria de policias de tránsito, ajustar semáforos que no eran críticos, enviar alertas falsas, que generan desconfianza en los usuarios. Esas acciones generarian ineficiencia operativa y economica porque habria que destinar recursos y personal.

- **Costo de un Falso Negativo:** No se predice alta congestión (no se activa una intervención), pero sí ocurre.

  La organizacion encargada tomaria decisiones que no son acordes al estado real de la movilidad y congestion en la cliudad, lo cual generaria un Aumento de los tiempos de viaje, frustración ciudadana, contaminación ambiental por vehículos detenidos, retrasos en servicios esenciales (emergencias, transporte público).
  
- **Limitación principal de los datos que persiste tras la limpieza:**

  Inicialmente, existe incertidumbre estadística que ninguna limpieza de datos puede eliminar. Por lo tanto, los resultados deben interpretarse como probabilidades y no como certezas absolutas al momento de tomar decisiones

**Tamaño de la muestra**

  El dataset cuenta con un tamaño de muestra reducido (1,440 registros). Esto implica que las relaciones observadas entre clima, cantidad de vehículos, tipo de vía y tiempo, son estimaciones basadas en una muestra limitada, no verdades absolutas.

**Concentración temporal**

  Aunque el dataset abarca fechas de marzo a diciembre de 2025, el 99% de los registros pertenece a marzo. Esto significa que el análisis refleja principalmente las condiciones de un solo mes, y las conclusiones sobre la relación entre clima y tráfico no pueden generalizarse a otras épocas del año (por ejemplo, temporada de lluvias, vacaciones, fin de año)

**Categorías de tráfico definidas estadísticamente**

  Los niveles 'bajo', 'medio' y 'alto' de tráfico se definieron con base en terciles de la propia muestra (no según un umbral técnico de capacidad vial real). Esto significa que 'tráfico alto' en este análisis es relativo a los datos observados, no necesariamente representa congestión real según estándares de tránsito

**Simplificación de la realidad**

  Los datos capturan solo algunas variables (clima, ubicación, cantidad de vehículos, tiempo), pero el comportamiento real del tráfico depende de muchos otros factores no controlados ni registrados (eventos, obras, accidentes, festivos, decisiones humanas). El modelo no puede reflejar toda esa complejidad, así que las conclusiones deben verse como una aproximación, no como la explicación completa del fenómeno de movilidad


## 8. Declaración de uso de Inteligencia Artificial

Ver `docs/declaracion_uso_IA.md`. Resumen: [1-2 líneas, ej. "Se usó IA generativa para
sintaxis de pandas en la Tarea 3; la elección de estrategia de imputación y la
interpretación de resultados fue realizada y validada por el equipo."]
