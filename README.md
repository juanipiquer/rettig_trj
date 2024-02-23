# unholster_prj
 
## Informe rettig repo

Este es un análisis explorativo para traspasar los casos documentados del informe Rettig desde un formato de texto a una base de datos estructurada analizable y con las trayectorias individuales sintetizadas en alguna forma.

El informe rettig consta de 500 paginas. Tiene toda un 

### Estructura de un caso en el texto

Los datos de personas-trayectorias tienen dos unidades de identifiación que no se repiten: Las personas, y los eventos. 
Las personas tienen como atributo su nombre y caracteristicas generales como edad, 

Los eventos tienen como atributo una fecha, un lugar y un cojunto de acciones de violencia cometidas contra las personas identificadas. 

La unidad identiicadora de los datos son los "eventos". Un evento son hechos localizados en una fecha en un lugar, que pueden afectar a más de una persona. 
Varios eventos contienen más de una víctima involucrada. 

Los datos están presentados por párrafos secuenciales, ordenados por zona geográfica primero y después cronológicamente. 

Las expresiones regulares que permiten particionar el texto son:
    - Un evento siempre inicia con la fecha en itálicas
    - todos los nombres están en negritas.

Esto permite hacer dos listas vinculadas de todos los nombres y de todos los eventos.

### Estructura del proyecto. 

El proyecto tiene dos partes distintas, cada una con su propio script. 

    - Parsing de los datos con expresiones regulares en HTML. 
    - Procesamiento de los con spaCy para detectar entidades, hacer resuménes y procesamiento de lenguaje natural en general.

#### Lo que hice: Parsing
    En primer lugar para probar los script más rápido pero igual ver los prolemas mas comunes, trabajé sólo Santiago. Son mas o menos la mitad de los casos.
    
    En el script de parsing pasé el PDF a HTML para recuperar la data del formato, y después trabajé sobre eso para separar los nombres por un lado y los eventos por otro.
    

#### Lo que falta: Parsing
 Seguir trabajando la extracción. Dada la regularidad del  formato, es lógico hacer está parte bien y a mano, y asegurarse de tener todos los nombres y todos los casos bien identificados.


#### Lo que hice: spaCy

    Sobre el estado del arte de procesamientos con modelos de lenguaje natural en Python, y en spaCy es fácil integrar todo y está enfocada en proyectos aplicados.
    En cualquier caso una vez que el procesamiento esté más afinado con los parámetros includios de spaCy como stop words o los modelos de lenguaje subyacentes, se puede probar con otras bibliotecas de esos elementos. 

    En términos de programación, lo que alcancé a hacer es la estructura básica de que haga un summary de cada evento, sin input de qué buscar. El resultado es bastante decente dado lo malo de los datos (no logré hacer bien el stop de cada caso ni incluir el párrafo donde está la fecha). El output es un excel con el caso original y el caso resumido. 

### Lo que falta spaCy

    Con más trabajo sobre el regex no es difícil llegar a una base de datos más perfecta con la que alimentar el pipeline de spacy. Hay que decirle que busque en los casos las caracteristicas individuales de los nombres como nombre, edad, empleo y militancia.
    El procesamiento con LLM y prompt tipo query requiere que los inputs no sean tan masivos, por lo que esta estrutura de datos me parece optima. 

    Yo haría un pipeline semi superversiado, y spaCy tiene buena implimentación de eso. Haría una pasada, corregir a mano un set de los outpus, y desupés le das como training esas observaciones.

## Post tener una base rica:

    Interno; se puede hacer una mejor vinculación con el resto del informe rettig y aprovechar parte del contenido que sale ahí. 

    Visualizaciones 
    Mapas de los lugares
    Cronología de las fechas 
    Estadística sumaria de género, edad, 

    Externo: 
    Después, una vez que se llega a una base de datos más o menos limpia, esta es relatiavamente fácil de cruzar con los RUT para hacer un mejor matching con otra ppotencial data del estado, porque la estructura de nombres es nombre - nombre - APELLIDO APELLIDO.

    



