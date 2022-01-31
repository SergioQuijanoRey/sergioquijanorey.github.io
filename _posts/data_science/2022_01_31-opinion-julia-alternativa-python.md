---
title: "Mi opinión de Julia como alternativa a Python"
categories: linux programacion datascience machinelearning julia python
date: 2022-01-31
---

Antes de empezar quiero decirte que este *post* está motivado por un directo que hice en [mi canal de Twitch](https://www.twitch.tv/sergioquijano) explorando este lenguaje de programación, como alternativa a *Python*. En concreto, me he querido centrar en su uso para proyectos de *Data Science / Machine Learning*, donde *Python* es el claro lenguaje predominante.

Dicho directo está resubido en el siguiente vídeo:

<iframe width="560" height="315" src="https://www.youtube.com/embed/gaN74zda5vE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Dicho vídeo tiene *timestamps* para que puedas consultar partes concretas de lo que hice en directo. En dicho directo supongo que tienes nociones básicas de programación, pues exploramos características y detalles fundamentales del lenguaje, que no apreciarás si no tienes conocimiento previo (aunque muy básico) en programación.

# ¿Qué es Julia y por qué debería interesarme?

*Julia* es un lenguaje de programación. Entre sus principales características se encuentran:

1. Sintaxis muy sencilla, parecida a la de *Python*. Por tanto es fácil de escribir y de leer
2. Dinámico, como *Python*, pero con algunas diferencias. Podemos lanzar una *shell* interactiva para explorar pequeñas ideas
3. Rápido. El código se ejecuta siguiendo el paradigma *Just In Time (JIT) compilation*. Un *benchmark* básico, y referencias a otros *benchmarks*, se pueden encontrar en [la documentación oficial](https://julialang.org/benchmarks/)
4. No tiene orientación a objetos. Sin embargo, otras características novedosas del lenguaje permitirán que trabajes con los tipos obteniendo las mismas (o parecidas) funcionalidades que con orientación a objetos. Principalmente:
    - Podemos especificar los tipos de las funciones y forzar su correcto uso
    - Gracias a ese sistema de tipos, tenemos *Multiple Dispatch* (el mismo nombre de una función puede usarse con distintos argumentos, como ocurre en lenguajes como *java*)
5. Lenguaje diseñado para la computación numérica
    - Puedes usar caracteres unicode, como símbolos matemáticos, escribiéndolos previamente en un comando de *latex*. Creo que *Python* también soporta esto, pero no está tan extendido su uso en la comunidad como en el caso de la comunidad de *Julia*
    - Fácil vectorización de cualquier función colocando un `.` delante de la llamada (esto puede verse en el vídeo que he enlazado previamente)
    - Fácil composición de funciones con el comando `\circ` o con el uso de *pipes*. Por ejemplo, `dato_procesado = dato_entrada |> funcion1 |> funcion2`
    - Una gran comunidad de científicos usando este lenguaje

Ahora, **personalmente**, para mí las características por las que creo que es interesante probar este lenguaje son las siguientes:

1. La sintaxis es extremadamente parecida a la de *Python*. Por lo tanto, no debería costarte demasiado esfuerzo aprender este lenguaje si ya conoces *Python*. De hecho, en el vídeo enlazado previamente, adapto el código para computar la sucesión de Fibonacci, escrito en *Julia*, a *Python*, en prácticamente menos de un minuto
2. *Julia* promete ser mucho más rápido que *Python*. En muchos casos aseguran tener una velocidad comparable a código escrito en *C*. Como comentaremos más adelante, no sé si esto es realmente cierto.
3. Sin embargo, muchas librerías de *machine learning* para *Julia* están escritas 100% en Julia.
    - Por ejemplo, la librería *Flux.jl* está escrita al 100% en *Julia*, como podemos ver en su [código fuente](https://github.com/FluxML/Flux.jl)
    - Mientras que las dos librerías de referencia en *Python*, no son más que *wrapper* para llamar código *C/C++* desde *Python*. Esto se puede ver en el código fuente de [Pytorch](https://github.com/pytorch/pytorch) y en el de [Tensorflow](https://github.com/tensorflow/tensorflow)
    - Por tanto, en el caso de *Python*, si queremos escribir código novedoso, que no esté ya incorporado en las librerías que estemos usando, y que sea pesado computacionalmente, o lo escribimos en *Python* haciendo todos los trucos posibles para acelerarlo, o lo escribimos en *C/C++* y lo llamamos desde *Python*
    - En *Julia*, sin embargo, podemos utilizar el mismo lenguaje y confiar en que correrá a una velocidad razonable. Por tanto, podemos escribir algoritmos pesados en el mismo lenguaje. O es más, incorporar dichos cambios en la librería que estemos consumiendo (ie. *Flux.jl*) con un *pull request*, pues estas librerías normalmente están escritas completamente en *Julia*
    - Esto me ha pasado en un proyecto de *machine learning*. Tuve que escribir un algoritmo para realizar lo que se conoce como minería de triples difíciles (si quieres saber más sobre esto, puedes consultar [el repositorio github del proyecto](https://github.com/SergioQuijanoRey/ComputerVisionPracticaFinal), y en concreto el *PDF* con la [explicación del proyecto](https://github.com/SergioQuijanoRey/ComputerVisionPracticaFinal/blob/main/memoria/Memoria.pdf)). Tuve que introducir muchos *"trucos"* para hacer que el código *Python* algo más rápido. Y con esto ensuciamos el código, por lo que pierde totalmente el sentido usar *Python*, cuya característica principal es lo simple de su sintaxis
    - Jeremy Howard ha comentado esto mismo multitud de veces, por ejemplo, en [esta entrevista](https://www.youtube.com/watch?v=4I1ejhQqD4c&ab_channel=Weights%26Biases)
4. La comunidad de *julia* me parece muy interesante. Al estar enfocada en computación científica / computación numérica / *data science*, creo que van a desarrollar paquetes realmente interesantes en estos campos
5. El lenguaje está diseñado para computación numérica, y por tanto tiene características muy interesantes si trabajas en alguno de los campos anteriormente citados. Por esto mismo, no estoy seguro de que en el futuro sea un lenguaje tan ampliamente usado en ámbitos tan diversos como lo es *Python*.
6. Trae un gestor de paquetes *"oficial"*, que en mi cortísima experiencia funciona perfectamente. Si has trabajado lo suficiente con *Python*, seguramente te hayas encontrado con problemas en la gestión de paquetes. Da igual que hayas usado *conda*, *env*, *pipenv*, *poetry*... Todos ellos tienen sus problemas.
    - Además, este gestor de paquetes gestiona también entornos, que quedan reflejados en archivos de proyectos para que sean fácilmente reproducibles
    - Esto es algo completamente positivo, pues definen un estándar a seguir. Al funcionar, a mi parecer, bien, en vez de surgir mil proyectos alternativos, creo que la tendencia será a contribuir al gestor estándar.

# Mis primeros pasos para aprender Julia

En este caso, hablaré sobre cuál ha sido mi camino para aprender lo básico sobre *Julia*. Claramente, y como muestra el directo resubido, no soy un experto en el lenguaje y tengo muchas lagunas. Por tanto, lo que voy a comentar es suficiente para que puedas empezar a escribir código en *Julia* y puedas hacer pequeños proyectos, pero necesitarás profundizar más en aquellas áreas en las que estés interesado.

1. [Julia for Pythonistas](https://colab.research.google.com/github/ageron/julia_notebooks/blob/master/Julia_for_Pythonistas.ipynb)
    - *Notebook* en *Google Colab* (si has trabajado con *machine learning* seguramente conozcas esta herramienta) listo para ejecutarse.
    - Expone un *tour* sobre muchas de las características del lenguaje. Es prácticamente suficiente para que puedas empezar a programar tus primeros proyectos
    - Además, durante todo el *notebook*, realiza una comparativa con *Python*, por lo que si estás acostumbrado a trabajar con este lenguaje, el aprendizaje será más efectivo
2. [Getting Started Oficial](https://docs.julialang.org/en/v1/manual/getting-started/)
    - Es el *getting started* de la página oficial del lenguaje
    - Dividido en varias páginas, una por cada característica del lenguaje
    - Se puede leer de forma secuencial, aunque es muy pesado, y para leerlo de esta forma usaría primeramente el recurso del *Notebook* previamente citado
    - Lo he usado más como un recurso de consulta sobre elementos concretos del lenguaje
3. [Ejemplo de modelo de machine learning usando Flux](https://machinelearninggeek.com/mnist-with-julia/)
    - Con los dos recursos anteriores, y si estás interesado, estás listo para programar tu primer modelo de *machine learning* usando *Julia*
    - Como puedes ver en el directo resubido, empecé intentando crear un modelo para la conocida base de datos *MNIST*
    - Esta página es un tutorial para crear un modelo simple (un *Multilayer Perceptron*) para resolver el problema. Directo al grano, explicando de forma sencilla las técnicas que usa
4. [Página oficial de Flux](https://fluxml.ai/Flux.jl/stable/models/overview/)
    - Puede usarse a la vez que consultamos el recurso anterior para desarrollar un modelo de *machine learning*
    - Lo he usado a modo de recurso de consulta, buscando las partes concretas en las que he estado interesado en cada momento
    - Se puede leer de forma secuencial, pero es bastante más pesado (pero también mucho más profundo) que el anterior recurso

# Lo bueno de Julia

# Lo malo de Julia

# Conclusiones
