# Predicción del caudal del día siguiente en cuencas chilenas (CAMELS-CL)

Proyecto para el ramo **EYP3407 – Tópicos Aplicados en Estadística**, Facultad de Matemáticas, Pontificia Universidad Católica de Chile, segundo semestre 2026.

- **Profesor**: Eloy Alvarado Narváez
- **Ayudante**: Andrés Díaz

## Equipo
- Javier Encina
- Camila Moreno
- Romina Navarro
- Javiera Sotolincoñir

## Pregunta de investigación
¿Cuánto mejora un modelo estadístico la predicción del caudal del día siguiente frente a mantener el caudal observado hoy (persistencia)?

Para responderla se comparan modelos de regresión penalizada (`glmnet`), modelos aditivos generalizados (`mgcv`) y Random Forest (`randomForest`) contra la persistencia, usando validación por ventanas temporales en el período 2000–2012 y una prueba final en 2013–2016.

## Datos
- **Fuente**: CAMELS-CL (Alvarez-Garreton et al., 2018), [PANGAEA.894885](https://doi.org/10.1594/PANGAEA.894885), licencia CC BY 4.0.
- **Subconjunto**: 30 cuencas con latitud de estación entre −33° y −40°, período 2000–2016.
- **Archivos** (carpeta `datos/`):
  - `caudal_m3s.csv`: caudal diario (m³/s)
  - `precipitacion_mm.csv`: precipitación diaria CR2MET (mm/día)
  - `temperatura_media_c.csv`: temperatura media diaria CR2MET (°C)
  - `atributos.csv`: atributos de cada cuenca
  - `diccionario_atributos.pdf`: descripción, unidades y fuentes de los atributos
  - `LEEME.txt`: detalle de la preparación de los datos

## Estructura del repositorio
- `Codigo_principal.R`: script principal (bloques 1 a 10: revisión de datos, construcción de variables, modelos y validación)
- `bloques_11_16.R`: comparación de modelos, prueba final, incertidumbre (bootstrap), diagnóstico y sensibilidades; se ejecuta automáticamente al final del script principal
- `resultados/`: tablas (`.csv`), objetos (`.rds`) y figuras (`.png`) generadas por el código
- `Informe_UC.qmd`: código fuente del informe en Quarto
- `Informe_UC.pdf`: informe final compilado
- `Diagrama.png`, `Diseño.png`: diagramas incluidos en el informe
- `borrador.R`: script de trabajo preliminar (no es necesario para reproducir los resultados)

## Software
- **R**: [https://cran.r-project.org/](https://cran.r-project.org/)
- **RStudio**: [https://posit.co/download/rstudio-desktop/](https://posit.co/download/rstudio-desktop/) o **VS Code**: [https://code.visualstudio.com/](https://code.visualstudio.com/)
- **Quarto**: [https://quarto.org/docs/get-started/](https://quarto.org/docs/get-started/)
- **Git**: [https://git-scm.com/downloads](https://git-scm.com/downloads)

## Reproducibilidad
Para asegurar que el código sea reproducible y el informe renderizable se necesitan algunas herramientas instaladas localmente dentro del computador a utilizar, por lo que se recomienda revisarlas antes de verificar los resultados. 

R utiliza los siguientes paquetes:
```r
install.packages(c("glmnet", "Matrix", "mgcv", "randomForest"))
```
el paquete `paralel` se incluye por defecto con la instalación de R.

El script `Codigo_principal.R` se debe ejecutar con la carpeta del repositorio como directorio de trabajo (Ej. Rstudio o VScode). El script está hecho para tomar los datos desde la carpeta `datos` y al finalizar ejecuta el segundo script `bloques_11_16.R` que guarda las tablas y las figuras en la carpeta `resultados`. Si R no encuentra los archivos de datos, se puede verificar el directorio de trabajo con `getwd()`. 

## Generación y renderización del informe
El informe está escrito en Quarto, guardado como "Informe_UC.qmd" y se compila a pdf mediante LaTeX.
Para ello se requiere:
- [Quarto](https://quarto.org/docs/get-started/)
- Una distribución de LaTeX. Se recomienda TinyTeX, que puede instalarse desde la terminal con:
```bash
quarto install tinytex
```

El informe se genera desde la terminal del sistema, no desde la consola de R, ubicándose en la carpeta del repositorio:
```bash
quarto render Informe_UC.qmd
```
Si es que sólo se quiere ver el informe sin correr los datos ni compilar, la versión final del informe se encuentra disponible en `Informe_UC.pdf`.

## Diagramas
- **Canva**: [Link de acceso](https://canva.link/503z7m0ovcm9jcj)

## Referencias
- Alvarez-Garreton, C., et al. (2018). The CAMELS-CL dataset: Catchment attributes and meteorology for large sample studies – Chile dataset. *Hydrology and Earth System Sciences, 22*(11), 5817–5846. [https://doi.org/10.5194/hess-22-5817-2018](https://doi.org/10.5194/hess-22-5817-2018)