# Herramientas de Software para Big Data — Obligatorio 2026

> **Facultad de Ingeniería — Bernard Wand-Polak**  
> Cuareim 1451 · 11.100 Montevideo, Uruguay  
> Tel. 2902 15 05 · Fax 2908 13 70 · [www.ort.edu.uy](https://www.ort.edu.uy)

---

## Evaluación

| Campo | Detalle |
|-------|---------|
| **Materia** | Herramientas de Software para Big Data |
| **Carrera** | Ingeniería en Sistemas, Licenciatura en Sistemas |
| **Condición** | Obligatorio |
| **Grupo** | N7, M7 |
| **Fecha** | 4/05/2026 |
| **Puntaje máximo** | 30 puntos |
| **Puntaje mínimo** | 0 puntos |
| **Fecha de entrega** | 13/07/2026 hasta las 21:00 horas en [gestion.ort.edu.uy](https://gestion.ort.edu.uy) (máx. 40 MB en formato zip, rar o pdf) |

---

## Uso de material de apoyo y/o consulta — Inteligencia Artificial Generativa

- Seguir las pautas de los docentes: se deben seguir las instrucciones específicas de los docentes sobre cómo utilizar la IA en cada curso.
- Citar correctamente las fuentes y usos de IA: siempre que se utilice una herramienta de IA para generar contenido, se debe citar adecuadamente la fuente y la forma en que se utilizó. Se debe indicar:
  - a. la/las herramientas utilizadas, y
  - b. el contexto de uso: por ejemplo, generación de ideas, redacción inicial, análisis de datos, corrección de estilo, etc.
- Todo contenido producido por IAG debe ser revisado y verificado; cualquier error presente será responsabilidad del estudiante.
- Ser responsables con el uso de la IA: conocer los riesgos y desafíos, como la creación de "alucinaciones", los peligros para la privacidad, las cuestiones de propiedad intelectual, los sesgos inherentes y la producción de contenido falso.
- El uso de herramientas de Inteligencia Artificial Generativa (IAG) puede emplearse como apoyo en el proceso de aprendizaje. Sin embargo, no sustituye el razonamiento crítico ni la elaboración personal. El estudiante es responsable de que el trabajo presentado refleje su propia comprensión, análisis y proceso cognitivo sobre el tema.

---

## Defensa

| Campo | Detalle |
|-------|---------|
| **Fecha de defensa** | 14/07/2026 |
| **Modalidad** | Obligatoria y eliminatoria. El docente es quien definirá y comunicará la modalidad y mecánica de defensa. La defensa será presencial salvo en casos en que se habilite la defensa oral sincrónica en forma remota. |
| **Consecuencia** | La no presentación a la misma implica la pérdida de la totalidad de los puntos del Obligatorio. |

---

## Importante

1. Inscribirse.
2. Formar grupos de hasta 3 personas del mismo dictado.
3. Subir el trabajo a Gestión antes de la hora indicada (ver sección [Recordatorio](#recordatorio-importante-para-la-entrega) al final del documento).

Aquellos de ustedes que presenten alguna dificultad con su inscripción o tengan inconvenientes técnicos, por favor contactarse con la Coordinadora de cursos o Coordinación Adjunta **antes de las 20:00 h** del día de la entrega, a través del mail: [adjuntos_ei@ort.edu.uy](mailto:adjuntos_ei@ort.edu.uy).

---

## Propuesta de Obligatorio

### Parte 1

Para el obligatorio deberá utilizar las herramientas usadas en el curso, levantadas en la máquina virtual de Azure. (En su defecto, para quienes no tengan créditos, está disponible una VM que puede utilizar en su máquina local.)

Deberá seleccionar un conjunto de datos tabulares con **más de 4 tablas**, que deberá ser aprobado por los docentes, y deberá seleccionar **5 preguntas** relativas a los datos que seleccionó, para contestarlas con las herramientas analíticas que también deberán ser aprobados por los docentes. Se restarán puntos a quienes no tengan el conjunto de datos y las preguntas aprobadas.

Deberá indicar la fuente de dónde obtuvo los datos. **La misma no podrá ser Kaggle.**

En caso de tener un modelo de datos al estilo OBT, se podrá utilizar siempre y cuando se pase a modelo normalizado antes de la ingesta de datos y no se puede volver a un modelo OBT en la etapa de modelado. Deberá presentar el código utilizado para cambiar el modelo de datos de OBT a normalizado.

Alternativamente queda como opción armar el conjunto de datos con las herramientas que tenga disponible para crear 3 fuentes ficticias de datos a integrar luego en un modelo de datos, o utilizar datos reales de una organización que los brinde para realizar el obligatorio, respetando no utilizar datos personales o confidenciales.

#### Pasos a seguir

1. **Preparar la ingesta.** Se deben dejar los datos en un lugar accesible a NiFi. Puede ser, por ejemplo, un repositorio en git al que se accede de forma remota vía HTTP, o puede ser una carpeta en la máquina virtual donde están instaladas las herramientas. **No se debe subir a HDFS los datos directamente vía comando.**

2. **Crear en HDFS las regiones** que considere necesarias para trabajar con los datos. Estas deben ser exactamente las regiones que se dieron en clase. Recuerde que en HDFS se deben definir "zonas" utilizando la estructura de directorio del file system. Cada zona debe llevar un nombre acorde para lo que es utilizada; se deben definir los criterios para utilizar las zonas, dejarlos por escrito y respetarlos. La ingesta debe dejar los datos en un lugar predefinido para ese uso. Se debe utilizar buenas prácticas de NiFi a la hora de hacer la ingesta (usar process groups y utilizar funnels, entre otros).

3. **Análisis exploratorio de los datos**, identificando el tipo de datos que hay en cada columna y qué significado tienen dentro del dominio de los datos. Dentro de un Jupyter notebook se mostrará:
   - una vista previa de las primeras filas,
   - cantidad de columnas de cada tabla,
   - nombre de cada columna,
   - descripción de los datos de cada tabla,
   - cómo está compuesto el esquema de los datos,
   - revisar valores nulos o faltantes y limpiarlos si es necesario,
   - revisar registros duplicados,
   - claves primarias únicas,
   - reglas de negocio que deba considerar para el refinamiento.

   Estos nuevos archivos se guardarán en HDFS, en otra ubicación como la versión refinada de los datos. **Para todo se debe utilizar únicamente Spark.**

4. **Elegir una forma de modelar los datos** una vez terminada la exploración y limpieza. Puede ser: Normalizada, Diagrama Estrella, Data Vault u OBT. Si para el modelo seleccionado necesita crear nuevos archivos, deben guardarse en una nueva ubicación dentro de HDFS. A esta ubicación apuntarán las tablas externas que luego definirá con Hive.

5. **Bosquejar el esquema** que relaciona las tablas con el modelo elegido (se sugiere usar draw.io, mermaid o excalidraw, pero puede utilizar otra herramienta).

6. **Guardar las tablas del modelo como tablas de Hive** en un esquema nuevo, una vez que tenga los dataframes de las tablas que va a utilizar en su modelo de datos.

7. **Contestar las preguntas seleccionadas** a partir de las tablas de Hive en un nuevo notebook. Deberá utilizar Spark con sintaxis SQL o con los distintos métodos que provee PySpark. **No se pueden contestar las preguntas llevando los archivos a dataframe directamente.** Solo se contará como válido utilizar las tablas Hive del modelo de datos creado.

8. **Visualizaciones en Jupyter (3 preguntas).** Del resultado obtenido de tres de las preguntas contestadas, llevar ese resultado a dataframe de pandas y crear **dos visualizaciones distintas** en el notebook de Jupyter, utilizando alguna de las librerías de visualización vistas en clase.

9. **Resultados en HDFS (2 preguntas).** Para las otras dos preguntas, conservarlas como archivo dentro de HDFS en una región donde guarde resultados de analíticas de datos. Crear nuevas tablas Hive que apunten a esos archivos.

10. **Visualizaciones en SuperSet (2 preguntas).** Utilizar las tablas Hive para realizar una visualización en SuperSet que ayude a contestar las dos preguntas realizadas. *(Hive es solo utilizado para conectar a SuperSet en el obligatorio, pero no es lo recomendado para poner en producción para un caso de Big Data real.)*

#### Entrega final — Parte 1

La entrega final consiste en un **informe** donde se detalle todo el proceso realizado y todo lo aprendido durante la realización del obligatorio. Se puede apoyar mediante capturas de pantalla o code snippets para explicar lo realizado.

El informe debe incluir:

- el dominio de los datos seleccionados,
- qué significa cada columna de cada tabla y qué tipo de dato debe tener,
- las preguntas seleccionadas planteadas y respondidas,
- la arquitectura del datalake, las tecnologías utilizadas y cómo contribuyen a su solución de big data para hacer análisis de datos.

También se deben entregar los notebooks utilizados, los dashboards creados en SuperSet y todo lo que resulte relevante para el trabajo que los alumnos consideren necesario como evidencia de que se cumplieron todos los pasos de la Parte 1.

---

### Parte 2

Seleccionar una organización, real o ficticia. Si en la Parte 1 utilizó los datos de una organización real, puede utilizar las mismas fuentes de datos; de lo contrario deberá utilizar datos distintos.

Deberán:

- listar las fuentes de datos, sus esquemas si es que los tienen, y cómo los integrarían en un nuevo modelo de datos,
- indicar qué preguntas de negocio contestarían con ese modelo de datos,
- investigar una posible solución para armar un datalake con **otras tecnologías distintas a las utilizadas para el obligatorio** (a excepción de Spark), sean nativas de una nube, de software libre o propietarias,
- explicitar con qué otras herramientas armarían su datalake y qué función cumpliría cada una,
- describir todo el proceso desde el origen de los datos hasta los consumidores finales para el nuevo caso seleccionado,
- realizar un diagrama con su nuevo stack para armar otro datalake,
- redactar todo el proceso desde la fuente hasta los consumidores de datos con el nuevo datalake.

> **Restricción:** si selecciona herramientas nativas de un proveedor cloud, **no puede mezclar** con herramientas de otra nube.

---

## Recordatorio: importante para la entrega

La entrega de los obligatorios será en formato digital online, a excepción de algunas materias que se entregarán en Bedelía y en ese caso recibirá información específica en el dictado de la misma.

Los principales aspectos a destacar sobre la entrega online de obligatorios son:

1. Ingresá al sistema de Gestión.
2. En el menú, seleccioná el ítem **"Evaluaciones"** y la instancia de evaluación correspondiente, que figura bajo el título **"Inscripto"**.
3. Para iniciar la entrega hacé clic en el ícono de entrega.
4. Ingresá el número de estudiante de cada uno de los integrantes y hacé clic en **"Agregar"**. El sistema confirmará que los integrantes estén inscriptos al obligatorio y, de ser así, mostrará el nombre y la fotografía de cada uno de ellos. Una vez agregados todos los integrantes, hacé clic en **"Crear equipo"**.

   Cualquier integrante podrá:
   - modificar la integración del equipo,
   - subir el archivo de la entrega.

5. Seleccioná el archivo que deseás entregar. Verificá el nombre del archivo que aparecerá en la pantalla y hacé clic en **"Subir"** para iniciar la entrega. Cada equipo (hasta 3 estudiantes) debe entregar un único archivo en formato zip o rar (los documentos de texto deben ser pdf, y deben ir dentro del zip o rar). El archivo a subir debe tener un tamaño máximo de **40 MB**.

   Cuando el archivo quede subido, se mostrará el nombre generado por el sistema, el tamaño y la fecha en que fue subido.

6. El sistema enviará un e-mail a todos los integrantes del equipo informando los detalles del archivo entregado y confirmando que la entrega fue realizada correctamente.
7. Podés cerrar la pestaña de entrega y continuar utilizando Gestión o salir del sistema.
8. La hora tope para subir el archivo será las **21:00** del día fijado para la entrega.
9. La entrega se podrá realizar desde cualquier lugar (ej. hogar del estudiante, laboratorios de la Universidad, etc.).
10. Aquellos de ustedes que presenten alguna dificultad con su inscripción o tengan inconvenientes técnicos, por favor contactarse con la Coordinadora de Cursos o Coordinación Adjunta **antes de las 20:00 h** del día de la entrega, a través del mail: [adjuntos_ei@ort.edu.uy](mailto:adjuntos_ei@ort.edu.uy).

---

*Escuela de Ingeniería — Documento original: Obligatorio Herramientas Software Big Data 2026*
