# Tarea 03 · Guía de los datos

## Abrir y empezar

Mantén los notebooks y la subcarpeta `dades` dentro de `Tasca_03`. Abre el notebook de enunciado y ejecuta las celdas en orden. La carga ya está escrita y utiliza `dades/observaciones_meteorologicas.csv`, una ruta relativa a la carpeta del notebook. Puedes reiniciar el núcleo y ejecutar desde el principio para recuperar la tabla inicial.

El trabajo requiere un entorno Jupyter con Pandas. Matplotlib solo hace falta si decides añadir una figura. Todos los datos están incluidos y se pueden leer sin conexión.

## Qué contiene el CSV

Es una tabla creada expresamente para esta actividad. **Todos los valores son sintéticos**, construidos manualmente con decimales sencillos. Litoral e Interior son nombres ficticios sin correspondencia con estaciones reales. Los valores diarios no se han calculado a partir de mediciones horarias.

Hay un registro por estación y día entre el 4 y el 17 de mayo de 2026, ambos incluidos. Cada fecha identifica el día UTC completo, desde su inicio hasta el inicio del día siguiente. La misma fecha aparece una vez por estación. No hay días enteros omitidos del calendario, aunque algunos valores están ausentes.

| Columna | Significado | Unidad o formato |
|---|---|---|
| `Fecha` | Día al que pertenece el registro | Texto `AAAA-MM-DD` al leer el CSV |
| `Estacion` | Identificador de la estación ficticia | Litoral o Interior |
| `Temperatura_C` | Temperatura media diaria | °C |
| `Precipitacion_mm` | Cantidad de precipitación acumulada durante ese día | mm |
| `Viento_m_s` | Media diaria de la velocidad del viento, entendida como módulo | m/s |

El archivo utiliza codificación UTF-8, comas entre campos y punto decimal. Las celdas vacías se interpretan como `NaN` con la lectura proporcionada. Cada hueco afecta solo a esa variable. Un cero sigue siendo un dato válido. La ausencia no debe sustituirse por cero.

## Algunas pistas para trabajar

`head()` permite empezar por pocas filas y `dtypes` ayuda a reconocer texto, números y fechas. Para convertir `Fecha`, utiliza `pd.to_datetime()` con `format="%Y-%m-%d"`. Después de seleccionar una estación, `set_index("Fecha")` y `sort_index()` preparan las selecciones temporales.

`len()` cuenta filas. `count()` cuenta los valores disponibles de la variable seleccionada. `isna()` localiza los huecos y `dropna(subset=[...])` permite retirar filas solo por la variable necesaria. Guarda el resultado con otro nombre si quieres conservar la tabla anterior.

Una media utiliza los valores disponibles. Una suma de precipitación debe acompañarse de los días que aportan datos. `sum(min_count=1)` evita que una selección sin datos dé cero, pero no garantiza que el periodo esté completo.

Las conclusiones se refieren a estos días sintéticos. Las diferencias entre estaciones no representan diferencias climáticas ni permiten atribuir efectos a una ubicación real.
