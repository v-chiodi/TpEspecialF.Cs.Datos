# Trabajo Práctico Especial - Fundamentos de la Ciencia de Datos

Análisis de Stack Overflow Developer Survey 2025. El trabajo está en `tp_especial.ipynb` e incluye exploración, limpieza, tres hipótesis del grupo y las tres preguntas propuestas por la cátedra.

[Informe de reentrega (PDF)](INFORME%20-%20Reentrega%20Grupo%2011.pdf)

## Instalación y ejecución

La ejecución se comprueba con Python 3.14.7. Las versiones de las dependencias están fijadas en `requirements.txt`.

Desde la carpeta del repositorio, en Windows:

~~~powershell
python -m venv venv
.\venv\Scripts\python.exe -m pip install -r requirements.txt
.\venv\Scripts\python.exe -m ipykernel install --user --name fundamentos-tpe --display-name "Fundamentos TPE"
.\venv\Scripts\python.exe -m jupyterlab tp_especial.ipynb
~~~

En Linux o macOS, los comandos equivalentes usan `venv/bin/python` en lugar de `.\venv\Scripts\python.exe`.

En JupyterLab, seleccionar el kernel **Fundamentos TPE** y ejecutar **Kernel → Restart Kernel and Run All Cells**. Guardar el notebook al finalizar. No es necesario ejecutar celdas de otra notebook.

## Datos

La primera celda descarga `results.csv` y `schema.csv` si no están en la carpeta de ejecución. Ambos corresponden a la misma versión del [repositorio oficial](https://github.com/StackExchange/Survey/tree/6ae2209cd35a55e92739ba82f7887fb86807a069/packages/archive/2025). El repositorio incluye `results.csv` mediante Git LFS. Si al clonar quedó solo el puntero de LFS, ejecutar `git lfs pull` desde la carpeta del repositorio antes de abrir el notebook. La descarga de `results.csv` ocupa aproximadamente 141 MB. Para descargar los archivos que falten, el notebook necesita conexión a Internet.

El archivo de respuestas tiene 49.191 registros y 172 columnas. Se conserva como entrada y las transformaciones se realizan sobre una copia. El notebook genera `dataset_limpio.pkl` con las variables seleccionadas y derivadas. Ese archivo se vuelve a generar durante la ejecución; no es una entrada necesaria.

## Organización del notebook

1. Exploración: origen, metadatos, tipos, distribuciones, faltantes y extremos.
2. Limpieza: selección de columnas, información disponible, respuestas desconocidas, coherencia con la edad, herramientas y variables derivadas.
3. Planteo de las hipótesis y definición del grupo profesional.
4. Evaluación, gráficos, controles de sensibilidad, resumen y límites.

## Criterios de interpretación

La hipótesis multivariada estudia la probabilidad de declarar trabajo totalmente remoto (`RemoteWork`) entre profesionales de Estados Unidos. La regresión logística incluye tamaño de empresa (`OrgSize`), rol (`ICorPM`), tramo de experiencia (`WorkExp`) y sector (`Industry`). Los odds ratios comparan cada tamaño con empresas de 1.000 a 4.999 empleados. La decisión sobre H₀ corresponde a la comparación entre empresas de 500 a 999 y de 1.000 a 4.999 empleados y se interpreta a partir del intervalo de confianza del 95 %.

La prueba de la mediana compara la compensación anual total en USD de Estados Unidos e India. Para Argentina se usa la prueba del signo para comparar la mediana de esa compensación con tres SMVM anualizados. El escenario del grupo usa un SMVM de ARS 391.200 mensuales y un tipo de cambio de ARS 1.570 por USD. Esas referencias corresponden a 2026 y las compensaciones a la encuesta de 2025.

En la hipótesis C se distinguen satisfacción general y prioridades laborales. `JobSatPoints_*` contiene rankings de importancia; no son calificaciones de satisfacción por aspecto. Se contrastan por separado la satisfacción general y el aspecto elegido como prioridad principal con la situación de cambio laboral.

La encuesta es voluntaria. Los resultados corresponden a las respuestas analizadas, no permiten establecer causalidad y pueden estar afectados por faltantes y selección de participantes.