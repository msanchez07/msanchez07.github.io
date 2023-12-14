# Modelos de clasificación
La elección de un modelo de clasificación puede depender de varios factores, y no todos los modelos tienen preferencia clara por problemas binarios o multiclase. Sin embargo, algunos modelos son comúnmente utilizados o se destacan en uno u otro escenario. 

Es importante tener en cuenta que la eficacia de un modelo también puede depender de la cantidad de datos, la complejidad del problema, la interpretabilidad requerida y otros factores específicos del escenario de aplicación. Además, la elección entre estrategias como OvO y OvR también influirá en cómo se implementa el clasificador multiclase. En la práctica, se recomienda probar varios modelos y estrategias para determinar cuál funciona mejor para un problema específico.

## Clasificadores binarios
Los modelos de clasificación binarios están dedicados a abordar problemas de clasificación que implican la categorización de instancias en dos grupos exclusivos. Estos modelos están diseñados para responder preguntas fundamentales de la forma "sí" o "no", siendo aplicables a una amplia variedad de escenarios. A continuación se muestra una lista de estos clsificadores:

[Regresión logística](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)

[Support Vector Machines (SVM)](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html)

[Árboles de Decisión](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html)

[SGDClassifiery](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.SGDClassifier.html)


## Clasificadores multiclase
Estos modelos no se limitan a respuestas "sí" o "no", sino qut tienen la capacidad de asignar instancias a múltiples clases distintas. Vamos a ver unos pocos de estos modelos:

[Regresión logística](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)

[Support Vector Machines (SVM) con OvO o OvR](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html)

[Random forest](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)

Muchos de estos modelos ya los hemos comentado en la parte de regresión, así que vamos a ver aquellos no explicados.

## Regresión logística
La regresión logística es una técnica fundamental en estadísticas y aprendizaje automático que se emplea para abordar problemas de clasificación. A pesar de su nombre, la regresión logística se utiliza para predecir la probabilidad de que una instancia pertenezca a una categoría específica. Este modelo es particularmente efectivo en situaciones donde la variable de salida es binaria, es decir, tiene dos posibles resultados, como "éxito" o "fracaso". A través de la función logística, transforma una combinación lineal de características de entrada en una probabilidad, permitiendo decisiones informadas sobre la pertenencia a una categoría particular. La regresión logística es conocida por su simplicidad, interpretabilidad y capacidad para adaptarse a diversos escenarios, lo que la convierte en una herramienta valiosa en la construcción de modelos de clasificación.