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

## Su sintáxis

Como ya hemos comentado previamente, la sintáxis de *Julia* es muy sencilla y parecida a la de *Python*. Disponer de un lenguaje rápido, adecuado para ciertas tareas, con una sintáxis tan buena es maravilloso. Por poner un ejemplo, para computar la sucesión de Fibonacci basta con el siguiente código:

~~~julia
function fib(n::Int64) ::Int64
    # Caso base
    if n == 0 || n == 1
        return 1
    end

    # Recurrencia
    return fib(n-1) + fib(n-2)
end
~~~

Si queremos adaptar este código recursivo para usar *memoization*, podemos hacer lo siguiente:

~~~julia

# Diccionario que sirve para la memoizacion
memoization = Dict()
memoization[0] = 1
memoization[1] = 1

function fib(n::Int64) ::Int64
    # Comprobamos si esta posicion ya la hemos calculado
    if n ∈ keys(memoization)
        return memoization[n]
    end

    # Computamos el valor y lo guardamos en nuestra tabla
    value = fib(n-1) + fib(n-2)
    memoization[n] = value

    return value
end
~~~

Como puedes ver, el código es muy parecido a lo que escribiríamos en *Python*. Las anotaciones de tipos, que es lo que parece distinguir más este código de un código escrito en *Python*, no son necesarias en este caso, siendo totalmente válido el siguiente código:

~~~julia
function fib(n)
    # Caso base
    if n == 0 || n == 1
        return 1
    end

    # Recurrencia
    return fib(n-1) + fib(n-2)
end
~~~

Si estás más interesado en este código te recomiendo que veas el directo resubido, que es donde desarrollo dicho código. Es más, como ya he comentado, adapto en directo este código a código en *Python* en menos de un minuto.

En una sección más avanzada del directo, ya trabajando con el proyecto de *machine learning*, escribo expresiones al igual que lo haría en *Python*, sin saber si funcionaría. Y efectivamente, funcionó. Por ejemplo, el siguiente código es válido:

~~~julia
x_train = [reshape(x_train[:,:, i], :) for i in 1:size(x_test)[3]]
~~~

donde estamos usando un constructo común en *Python* para formatear un conjunto de datos.

## El uso de tipos

En *Python* podemos (y creo que es una buena costumbre) usar anotación de tipos. Por ejemplo, podemos escribir el siguiente código *Python*:

~~~python
def f(x: int = 2)
    return x * x
~~~

Estamos indicando que a la función deberíamos pasarle un entero. Sin embargo, nada nos impide que usemos cualquier otro tipo de parámetro. Esta anotación de tipos no es más que eso, una anotación como cualquier otro tipo de documentación. *Python* no va a comprobar nada sobre dichos tipos. Existen herramientas como [mypy](http://mypy-lang.org/) para asegurar el buen uso de los tipos, pero por lo que tengo entendido, no funciona con cualquier código de *Python*.

Sin embargo, en *Julia*, si anotamos los tipos (cosa que no es necesaria, como ya hemos mostrado previamente), tendremos comprobaciones y recibiremos errores si no usamos correctamente los tipos:

~~~julia
function f(x::Int64)
    return x*x
end

result = f(3.14)
~~~

Este código devuelve un error, aunque podríamos no haber anotado el tipo y el código funcionaría.

El objetivo del uso de tipos no es directamente este, sino el de permitir *multiple dispatch*. Sin embargo, es una efecto colateral que personalmente me gusta. Considero que es positivo poder controlar los tipos de las funciones, aunque no sea necesario, para evitar problemas en el futuro, y para forzar diseños más adecuados.

## Multiple Dispatch

Ya lo hemos comentado previamente, pero podemos escribir código del siguiente modo:

~~~julia
function f(x::Int64)
    return x*x
end

function f(x::Float64)
    return x + x
end

value = f(3)   # Value es 9
value = f(3.0) # Value es 6.0
~~~

Esto es algo común en otros lenguajes, como puede ser el caso de *Java*. Sin embargo, en *Julia*, al no disponer de programación orientada a objetos *"out of the box"*, usaremos mucho más estas caraterísticas para lograr ciertas funcionalidades deseadas. Por ejemplo, supongamos que tenemos una estructura `Persona`:

~~~julia
struct Persona
    name::String
    age::Int64
end
~~~

De momento, solo disponemos del constructor por defecto, que toma los argumentos en orden. Por ejemplo, `sergio = Persona("Sergio", 22)`. Sin embargo, usando el *multiple dispatch* podemos definir una función con el mismo nombre pero con argumentos distintos. Por ejemplo:

~~~julia
function Persona(name::String) ::Persona
    return Persona(name, 18)
end
~~~

Sobre este tema, podríamos hablar largo y tendido, pero si quieres informarte más, te aconsejo que veas la parte del directo en la que exploro esto, y que consultes el *notebook* previamente citado (lo puedes encontrar [aquí](https://colab.research.google.com/github/ageron/julia_notebooks/blob/master/Julia_for_Pythonistas.ipynb))

## El lenguaje no se va a interponer en tu camino

Seré breve pues ya lo hemos comentado previamente. En *Python*, si en tu proyecto de *machine learning* te encuentras con un problema que tu librería (ya sea *tensorflow* o *pytorch*) no resuelve, tienes dos opciones:

1. Escribir el algoritmo (potencialmente pesado a nivel computacional) en *Python*
    - Si lo escribes de forma clara y fácil de leer, probablemente sea demasiado lento
    - Si lo intentas optimizar con pequeños *trucos* o *hacks* para que no sea excesivamente lento, terminarás con un código críptico y difícil de leer. Con esto, pierde el sentido escribirlo en *Python*
2. Escribirlo en un lenguaje rápido (ie. *C / C++*) y llamar a este código desde *Python*

En *Julia* esto no pasa. El lenguaje es lo suficientemente rápido como para poder correr algoritmos pesados, gracias a la compilación *Just in Time*. Esto, teóricamente (recalco aquí que no he trabajado lo suficiente con el lenguaje) evitará el ciclo "escribo la idea en *Python*, veo que funciona, así que lo re-escribo en un lenguaje rápido para tener una versión final que llamaré desde otro lenguaje como el mismo *Python*"

Gracias a esto muchas librerías como *Flux.jl* están escritas completamente en *Julia*. Si quieres hacer un pequeño *"hack"* en tu proyecto, o si quieres contribuir a la librería, no necesitarás usar otro lenguaje.

## Puedes llamar fácilmente a código de *Python*

Algo que no cubro en el directo, y que realmente me parece positivo, es la facilidad con la que podemos llamar a código de *Python*. Por ejemplo:

~~~julia
using PyCall
os = pyimport("os")
path = os.path.join("pruebas", "mas_pruebas")
println(path) # "pruebas/mas_pruebas"
~~~

Por tanto, si necesitas usar partes específicas de *Python*, en teoría deberías poder sin demasiados problemas.

## El gestor de paquetes

Para acceder al gestor de paquetes basta con lanzar la *shell* de *Julia* `julia` y pulsar la tecla `]`, entrando en modo paquetes. Una vez hecho esto, podemos añadir un paquete con la orden `add Flux`, por ejemplo.

Si queremos crear un entorno virtual, dentro del modo paquete podemos usar la orden `activate .`. Creará un entorno si no existe previamente, y si existe lo cargará. A partir de este momento podremos usar ordenes como la de instalación de paquetes para gestionar el entorno. Además, se crearán dos archivos `.toml` que reflejarán el estado del proyecto. Estos ficheros los podemos colocar en `git`, haciendo que nuestro entorno sea fácilmente reproducible.

Me gustaría poder hacer esto sin tener que entrar en la *shell* de *Julia*, por ejemplo hacer algo como `julia --add_pkg Flux`. Sin embargo, esto no debe ser difícil de programar, pues podemos realizar todas las órdenes de paquetes desde un *script* de *Julia*, por ejemplo:

~~~julia
import Pkg
Pkg.add("Flux")
~~~

Y con esto debería ser sencillo crear una herramienta para realizar lo anteriormente descrito. El hecho de poder gestionar los paquetes desde código *Julia* me parece algo muy positivo.

# Lo malo de Julia

## Lentitud

¿Cómo digo esto, si llevo todo el *blog* hablando de la rapidez de *Julia*? Pues lo fundamental aquí es comprender cómo *Julia* consigue ser tan rápido a la vez que dinámico.

Antes desarrollar nada, quiero recalcar que no conozco en detalle las técnicas de las que voy a hablar, solamente las ideas generales de dichas técnicas. Por tanto, puedo cometer errores al explicar dichas técnicas, aunque las ideas generales deberían ser correctas.

El truco es el uso de una técnica conocida como *Just in Time (JIT) compilation*. Antes de explicar en qué consiste, veamos las dos alternativas a dicha técnica:

1. Lenguaje dinámico, como es el caso de *Python*. En estos lenguajes, las órdenes de alto nivel van llegando de una en una (o en bloques). Se traducen a lenguaje máquina y se ejecutan
2. Lenguaje compilado, como puede ser *C++*. En este caso, todo el código se traduce a lenguaje máquina antes de poder ejecutarse. Una vez disponemos de todo el programa en lenguaje máquina (el binario), ejecutamos dicho lenguaje máquina

En el caso de *JIT*, las instrucciones van llegando una a una o en bloques. Antes de ser ejecutadas, se compilan y normalmente se almacena el resultado de la compilación. Con esto se ejecutan. Si se puede re-aprovechar la compilación de un bloque de código (ie. el código que se ejecuta en un bloque `for`), no se repite la compilación, sino que se aprovecha.

Esto provoca los siguientes efectos:

1. La primera vez que llega una instrucción o bloque, tardaremos más en ejecutarlo que en un lenguaje dinámico, pues realizamos el proceso de compilación
2. Sin embargo, las siguientes veces que se repita el código, la ejecución será más rápida. Prácticamente a la misma velocidad que en lenguajes compilados

Por ejemplo en un bucle `for`:

- La primera iteración será más lenta que en un lenguaje dinámico
- Sin embargo, las posteriores ejecuciones serán muchísimo más rápidas que en un lenguaje dinámico

Hasta aquí todo bien. El pequeño *overhead* inicial debería ser compensado por las veces que repetimos ciertos cómputos pesados. El **problema** que me he encontrado principalmente es a la hora de **importar una librería**. Esto puede verse claramente en el directo resubido.

Esto que digo puede ser incierto, pues no he investigado lo suficiente. Pero a mi entender, el problema es que a la hora de importar una librería, pre-compilamos dicha librería (esto lo pienso por los mensajes que obtenemos al hacer `add` de las librerías).

Esto que digo se ve respaldado en esta pregunta en [*StackOverFlow*](https://stackoverflow.com/questions/49635221/speeding-up-package-load-in-julia) y en el [foro oficial de Julia](https://discourse.julialang.org/t/extremely-slow-execution-time/11095). Así que no parece ser un problema que solamente yo tenga. En ambos casos se proponen algunas soluciones:

1. Mantener las sesiones vivas el máximo tiempo posible. Ya sea que estemos usando la *shell* interactiva o un *notebook* como *Jupyter*
2. Usar algún paquete que se encargue de evitar recompilar las librerías una y otra vez. Por ejemplo, [Revise.jl](https://github.com/timholy/Revise.jl)

La primera alternativa no me gusta, pues no es factible a la hora de escribir código en un editor de texto. Estaríamos obligados a escribir código en un *notebook* como *Jupyter* (cosa que hago en el directo, identificando correctamente el problema con los tiempos de ejecución) o en una *shell*.

Estoy seguro de que el equipo de desarrolladores estará trabajando en solucionar este problema.

## Documentación insuficiente

Este es un problema prácticamente inevitable, al ser *Julia* un lenguaje tan nuevo. En el directo se puede ver cómo hago búsquedas sobre ejemplos para resolver el conjunto de datos *MNIST*, y los resultados que obtengo no son de muy buena calidad. Sin embargo, realizar la misma búsqueda para alguna librería de *Python* seguramente arrojará más resultados, de mayor calidad. Simplemente por disponer de una comunidad mucho más grande que ha generado contenido durante más tiempo.

No es algo de lo que pueda culpar a *Julia*. Como ya he dicho, es inevitable. Además, la solución pasa por esperar cierto tiempo a que la comunidad crezca y genere más y mejor contenido sobre el lenguaje.

Sin embargo, la documentación oficial si que me parece en cierta medida insuficiente. En el mismo directo, realizo una búsqueda sobre el tipo de datos *diccionario* en la documentación oficial. Lo encuentro pero no es fácilmente indexable, pues aparece mezclado con otros tipos de datos. Además, no tengo un índice con los métodos del tipo de dato, pues el índice muestra el resto de tipos de dato que aparecen junto al diccionario. Compruébalo tu mismo en la [documentación oficial](https://docs.julialang.org/en/v1/base/collections/), que es lo que a día de hoy me aparece al realizar la búsqueda *julia dictionary*.

Esto sí que puede mejorarse a día de hoy. Un buen ejemplo a seguir es la magnífica documentación de *Rust*. Por ejemplo, la documentación oficial sobre el tipo de dato *HashMap* se puede encontrar [aquí](https://doc.rust-lang.org/std/collections/struct.HashMap.html), bien indexada y accesible.

## El compilador no es muy claro

De nuevo tomaremos como referente el compilador de *Rust*, que es magnífico. Los errores son claros, bien documentados e incluso proponiendo buenas soluciones. En [este post](https://dmerej.info/blog/post/letting-the-compiler-tell-you-what-to-do/) se puede apreciar a lo que me refiero.

Por parte de *Julia*, los errores con los que me he encontrado no me han parecido tan claros de leer (como puede verse a lo largo del directo). Por ejemplo, si accedemos a una estructura de datos usando el índice 0 (en *Julia* tenemos *1-indexing*) obtenemos el siguiente error:

~~~julia
ERROR: KeyError: key 0 not found
Stacktrace:
 [1] getindex(h::Dict{Any, Any}, key::Int64)
   @ Base ./dict.jl:481
 [2] top-level scope
   @ REPL[5]:1
~~~

En este caso, el error es muy sencillo y leyéndolo seguramente sepa identificar el problema. Sin embargo, y siguiendo este simple ejemplo, observemos:

1. No propone una solución al problema, como hace *Rust* en múltiples ocasiones. En este caso, sería fácil que el compilador, a sabiendas de que estamos usando *0-indexing* en un lenguaje *1-indexing*, podría informarnos de esto de forma clara y en un lenguaje sencillo
2. El *StackTrace* es algo ilegible

Hacia el final del directo puedes ver que me encuentro con un problema con las dimensiones de las matrices con las que estoy trabajando (un problema no tan trivial como el que he presentado previamente). Puedes comprobar que el error apenas me ayuda a identificar su fuente. Y además, el *StackTrace* es tan largo e irrelevante que oculta lo realmente útil en el error. Creo que, en ese caso en concreto, el problema se ve agravado al mostrar el *stacktrace* de la macro que estaba usando.

Sin embargo, todo lo que he dicho hay que cogerlo con pinzas. Estoy comparando un lenguaje compilado, estrictamente tipado y no dinámico con un lenguaje dinámico, no estrictamente tipado y con *JIT*. Puede ser (no estoy seguro de esto pues no conozco en detalle los procesos de compilación) que *Rust*, en su compilación, tenga más información global con la que detectar e informar de problemas. Mientras que *Julia*, al compilar bloque a bloque, puede que no tenga tanta información y que muestre lo mejor que puede detectar.

# Conclusiones
