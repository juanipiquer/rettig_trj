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




La fecha en Italicas.
    Después de la fecha en Italicas, se procede a describir una situación en algun lugar geográfico más o menos consistentes.
    En ese lugar puede haber uno o mas de un nombre mencionado. Los nombres no se repiten. 

    
