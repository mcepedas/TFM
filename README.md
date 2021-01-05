# TFM: Construcción y validación de modelos predictivos de moléculas activas para el cáncer de mama.
Este proyecto tiene el objetivo de construir y evaluar diferentes modelos para predecir moléculas activas para la diana Breast Cancer Resistance Protein (BCRP).
En este repositorio se incluye el script con todos los modelos construidos y los ficheros necesarios para reproducir el trabajo en cualquier punto de interés. También se incluye un apartado con la evaluación de los modelos a diferentes concentraciones IC50 y diferentes separaciones de datos, que se realizaron durante el desarrollo del proyecto. 
El mejor modelo obtenido, guardado en el archivo model_SVM, puede usarse siguiendo las instrucciones siguientes:

**1.- Cargar modelo en R:**

`library(kernlab)`<br>
`load(“modelo_SVM.RData”)`

**2.- Para obtener los descriptores de las moléculas es necesario partir de los SMILES. Se puede usar el archivo Workflow_KNIME adjunto en este repositorio, modificando tan solo el nombre del archivo de entrada y el nombre del archivo de salida. Los descriptores a obtener en este mismo orden son los siguientes:**

- Mannhold LogP
- Aromatic Bonds Count
- Hydrogen Bond Acceptors
- Hydrogen Bond Donors
- Largest Chain 
- Largest Pi Chain
- Petitjean Number
- Lipinski’s Rule of Five
- Topological Polar Surface Area
- XLogP
- Formal Charge (pos)
- SP3 Character
- ALogP1
- ALogP2
- Moreau-Broto Autocorrelation (mass) descriptors1
- Moreau-Broto Autocorrelation (charge) descriptors1
- Moreau-Broto Autocorrelation (charge) descriptors3
- Moreau-Broto Autocorrelation (charge) descriptors5
- Moreau-Broto Autocorrelation (polarizability) descriptors5

**3.- Finalmente se aplica la normalización a los datos obtenidos en KNIME. Esta normalización esta guardada en el archivo scale y puede aplicarse de la manera siguiente:**

`load(“scale.RData”)`<br>
`datos_normalizados <- as.data.frame(scale(datos, center = center, scale = scale))`

**4.- Ejecutar el modelo con los datos normalizados:**

`resultados <- predict(svm_model_imp_z, datos_normalizados)`

