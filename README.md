# Trayectorias informe Rettig
 
### Informe rettig repo

Este es un análisis explorativo para traspasar los casos documentados del informe Rettig desde formato de texto a una base de datos estructurada analizable y con las trayectorias individuales sintetizadas.  
El informe rettig consta de tres tomos de 1700 páginas en total.

La pretensión de recopilación de casos es de exhaustividad respecto a los de violencia política grave, especialmente asesinatos y desapariciones forzadas. La tortura quedó fuera y se abordó después en la comisión Valech. A su vez, muchos casos no fueron presentados por las víctimas o sus familiares, o se consideró que no habían pruebas suficientes para poder ser incluidos.

El informe tiene tres tomos. El primero tiene los casos de septiembre de 1973 a diciembre de 1973, que es el período con más casos en general y con mayor cantidad de personas no vinculadas a la izquierda política. 
El tomo 2 se divide en dos períodos. 74-78, que es de más ataques sistemáticos a personas de izquierda política y oposición. Y 78-90, donde se mantiene la persecución política y se agrega casos en contexto de represión de protestas.

Tomos 1 y 2 tienen información descritpiva de los contextos y formas de operación.

El tomo 3 es auxiliar de los otros dos y tiene una lista de todos los individuos mencionados en los casos, con el resumen biográfico y descripción breve del evento.

## Estructura de un caso en tomos 1 y 2.
Los datos tienen dos unidades de identifiación que no se repiten: Las personas, y los eventos. 

- Las **personas** tienen como atributo su nombre y caracteristicas generales como edad, empleo y militancia, y las circunstancias de su caso.
- Los **eventos** tienen como atributo una fecha, un lugar, un cojunto de acciones de violencia cometidas y la individualización de las víctimas de esas acciones.

La información está presentada por párrafos secuenciales, ordenados por región y dentro de ellas cronológicamente. 

Las regularidades que permiten particionar el texto de los tomo I y II son:
- Un evento siempre inicia con la fecha en itálicas
- Todos los nombres están en negritas.

Esto permite hacer dos listas vinculadas de todos los nombres y de todos los eventos.

En el tomo tres se repiten todos los nombres individuales, también en negritas, y con breves descripciones de muerto o desaparecido, edad, empleo, actividad política, y  circunstancias del evento. Contienen un poco mas de información personal que la expuesta en los Tomo I y II, y menos información respecto a los eventos.

## Estructura del procesamiento. 

El proyecto tiene dos partes distintas, cada una con su propio script. 

- Parsing de los datos con regularidades en HTML. 
- Procesamiento con spaCy para detectar entidades, hacer resúmenes y procesamiento de lenguaje natural en general.
### Parsing
#### Lo que hice
En primer lugar para probar los script más rápido pero igual ver los prolemas más comunes, trabajé sólo RM. Son mas o menos la mitad de los casos.

En el script de parsing pasé el PDF a HTML para recuperar la data del formato (Italics=event; Bold=name), y después trabajé sobre eso para destilar los nombres por un lado y los eventos por otro.

#### Lo que falta
Seguir trabajando la extracción. Dada la regularidad del  formato, es lógico hacer está parte sin modelos predictivos, pues es posible asegurarse tener todos los nombres y todos los casos bien individualizados.

También hay q hacer la extracción de datos del tomo 3, para hacer la tabla de todas las personas con sus atributos de forma precisa. Esta se debería cotejar con la lista de nombres obtenidas del tomo I y II. Toda persona debería ser asignable a un caso. 

### spaCy 
#### Lo que hice

Sobre el estado del arte de procesamientos con modelos de lenguaje natural en Python, en spaCy es fácil integrar todo (NER, LLM) y está enfocada en proyectos aplicados.
En cualquier caso una vez que el procesamiento esté más afinado con las herramientas incluidas de spaCy como stop words o los modelos de lenguaje subyacentes, se puede probar con otras bibliotecas de esos elementos. 

En términos de programación, lo que tengo es la estructura básica de que haga un summary de cada evento, sin input de qué buscar. El resultado no es tan malo dado lo malo de los datos (para cada caso falta hacer bien el límite entre c/u e incluir el primer párrafo). El output es un excel con las parejas de texto original y caso resumido.
#### Lo que falta
Con más trabajo sobre el regex de sparcing no es difícil llegar a una base de datos más perfecta con la que alimentar el pipeline de spacy. Hay que enfocarlo en que busque en los casos las descripciones de contexto y detalles del evento, pues las identificaciones personales están asignadas con precisión y más detalle en el tomo 3.

El procesamiento con LLM y prompt tipo query requiere que los inputs no sean tan masivos, por lo que esta estructura de datos me parece óptima. 

Yo haría un pipeline semi superversiado, y spaCy tiene buena implimentación de eso. Haría una pasada, corregir a mano un set de los outpus, y desupés le das como training esas observaciones.

## Post tener una base rica:

**Interno**: se puede hacer una vinculación con el resto del informe rettig y aprovechar parte del contenido que sale ahí, en la medida de que hayan elementos vinculables a los eventos.

*Visualizaciones*  
Mapas de los lugares  
Cronología de las fechas   
Estadística sumaria de género, edad, etc.

**Externo**: 
Después, una vez que se llega a una base de datos más o menos limpia, esta es relatiavamente fácil de cruzar con los RUT para hacer un mejor matching con otra potencial data del estado, porque la estructura de nombres es nombre - nombre - APELLIDO APELLIDO.

Dado que el lenguaje del informe es parecido al legal penal chileno y habla sistemáticamente sobre casos de violaciones de DDHH y el contexto de la dictadura, agregaría todo el documento como training de un modelo para resumir casos provenientes de otras fuentes.


### *librerías*

spaCy https://spacy.io/usage 

Beautiful soup https://www.crummy.com/software/BeautifulSoup/bs4/doc/

PDFminer https://github.com/pdfminer/pdfminer.six

