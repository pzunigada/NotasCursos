# ***Analisis de NOSQL (Not Only SQL)***

Base de Datos Documental
Los Documentos


Informacion Adicional
XML
YAML
JSON



# Base de Datos Documental
Una base de datos documental está constituida por un conjunto de programas que almacenan, recuperan y gestionan datos de documentos o datos de algún modo estructurados. Este tipo de bases de datos constituyen una de las principales subcategorías dentro de las denominadas bases de datos NoSQL. A diferencia de las bases de datos relacionales, estas bases de datos están diseñadas alrededor de una noción abstracta de "Documento". 

## **Los Documentos**
El concepto central de una base de datos orientada a documentos es el concepto mismo de Documento. Mientras cada implementación de base de datos orientada a documentos difiere en los detalles, en general todas ellas comparten el principio de que los documentos encapsulan y codifican datos o información siguiendo algún formato estándar. Entre las codificaciones usadas en la actualidad se encuentran XML, YAML y JSON, así como formatos binarios como BSON.

Los documentos dentro de una base de datos orientada a documentos son similar, de algún modo, a registros, tuplas o filas en una base de datos relacional pero menos rígidos. No se les requiere ajustarse a un esquema estándar ni tener todos las mismas secciones, atributos, claves o cosas por el estilo. Por ejemplo un documento puede ser: 
``` JS
 {
    Nombre:Miguel Ignacio Barboteo Piñero
    Dirección:Málaga
    Profesión:"Bancario"
 }
```
Mientras que otro:
``` JS
 {
     Nombre:Miguel Ignacio Barboteo Piñero
     Dirección:Málaga
     Hijos:[
        {Nombre:"Iñaki"},
        {Nombre:"Nando"},
        {Nombre:"Maria"},
    Esposa:[
        {Nombre:"Maria Begoña"},
``` 
Estos documentos contienen alguna información similar y otra diferente. Al contrario que una base de datos relacional en la que todos los registros deben tener los mismos atributos -que pueden quedar vacíos- , en un documento no quedan 'campos' vacíos. De este modo es posible añadir nueva información sin necesidad de establecer qué información queda excluida.

### ***Claves***
Se direccionan los documentos mediante una clave única que identifica el documento. Generalmente esta clave se compone de una simple cadena. En algunos casos puede tratarse de un URI o un camino, que sirve para rescatar el documento de la base de datos. Generalmente la base de datos mantiene un índice de dichas claves, por lo que la recuperación es rápida.

### ***Recuperación***
Otra de las características que definen una base de datos orientada a documentos es que, más allá de la sencilla correspondencia clave-documento (o clave-valor) usada para recuperar un documento, la base de datos ofrece un API o un lenguaje de interrogación para recuperar documentos según su contenido. Por ejemplo, para preguntar por todos los documentos que tienen un valor dado en un campo. El conjunto de características del API o del lenguaje de interrogación, así como lo que se obtiene, varía significativamente entre distintas implementaciones.

### ***Organización***
Las distintas implementaciones de bases de datos documentales que podemos organizan los documentos de muy distintas formas, entre las que se encuentran:

* Colecciones
* Etiquetas
* Metadatos ocultos
* Jerarquías de directorios

## **Bases de datos XML**
La mayoría de las bases de datos XML están orientadas a documentos. 

# Base de Datos Orientada a Grafos

Una base de datos orientada a grafos (BDOG) representa la información como nodos de un grafo y sus relaciones con las aristas del mismo, de manera que se pueda usar teoría de grafos para recorrer la base de datos ya que esta puede describir atributos de los nodos (entidades) y las aristas (relaciones).

![Graph DataBase](./GraphDatabase_PropertyGraph.png "Base Datos Grafo")

Una BDOG debe estar absolutamente normalizada, esto quiere decir que cada tabla tendría una sola columna y cada relación tan solo dos, con esto se consigue que cualquier cambio en la estructura de la información tenga un efecto solamente local.
Investigadores han demostrado que las bases de datos de grafos no presentan ningún beneficio sobre las bases de datos tradicionales cuando se simulan sobre un motor de bases de datos RDBMS. Sin embargo son bastante eficientes cuando son nativas.

### Reseña historica
Aunque pareciera ser una novedad en el área de las bases de datos, el modelo orientado a grafos ya lleva un buen tiempo de haber sido inventado; sin embargo, debido a la aparición de otros modelos como el de orientación a objetos y el más conocido de todos, el relacional, las BDOG pasaron a un segundo plano, debido principalmente por la simplicidad y fácil manejo del último mencionado, el modelo relacional.

El uso de las BDOG es escaso aunque actualmente hay muchas herramientas para su desarrollo (Ver abajo el 'Listado de bases de datos orientadas a grafos'). 




# Informacion Adicional

## XML eXtensible MArkup Language
***es un metalenguaje que permite definir lenguajes de marcas desarrollado por el World Wide Web Consortium (W3C)*** utilizado para almacenar datos en forma legible. Proviene del lenguaje SGML y permite definir la gramática de lenguajes específicos (de la misma manera que HTML es a su vez un lenguaje definido por SGML) para estructurar documentos grandes. A diferencia de otros lenguajes, XML da soporte a bases de datos, siendo útil cuando varias aplicaciones deben comunicarse entre sí o integrar información.1​

XML no ha nacido únicamente para su aplicación en Internet, sino que ***se propone como un estándar para el intercambio de información estructurada entre diferentes plataformas***. Se puede usar en bases de datos, editores de texto, hojas de cálculo y casi cualquier cosa imaginable.

XML es una tecnología sencilla que tiene a su alrededor otras que la complementan y la hacen mucho más grande, con unas posibilidades mucho mayores. Tiene un papel muy importante en la actualidad ya que ***permite la compatibilidad entre sistemas para compartir la información de una manera segura, fiable y fácil.*** 

### Ventajas del XML
* ***Es extensible:*** Después de diseñado y puesto en producción, ***es posible extender XML con la adición de nuevas etiquetas,*** de modo que se pueda continuar utilizando sin complicación alguna.
* ***El analizador es un componente estándar***, no es necesario crear un analizador específico para cada versión de lenguaje XML. Esto ***posibilita el empleo de cualquiera de los analizadores disponibles***. De esta manera se evitan bugs y se acelera el desarrollo de aplicaciones.
* Si un tercero decide usar un documento creado en XML, ***es sencillo entender su estructura y procesarla***. Mejora la compatibilidad entre aplicaciones. Podemos comunicar aplicaciones de distintas plataformas, sin que importe el origen de los datos, es decir, podríamos tener una aplicación en Linux con una base de datos Postgres y comunicarla con otra aplicación en Windows y base de datos MS-SQL Server.
* Transformamos datos en información, pues ***se les añade un significado concreto y los asociamos a un contexto***, con lo cual tenemos flexibilidad para estructurar documentos.
Estructura de un documento XML

La tecnología XML busca dar solución al problema de expresar información estructurada de la manera más abstracta y reutilizable posible. Que la información sea estructurada quiere decir que se compone de partes bien definidas, y que esas partes se componen a su vez de otras partes. Entonces se tiene un árbol de trozos de información. Ejemplos son un tema musical, que se compone de compases, que están formados a su vez por notas. Estas partes se llaman elementos, y se las señala mediante etiquetas.

Una etiqueta consiste en una marca hecha en el documento, que señala una porción de este como un elemento. Un pedazo de información con un sentido claro y definido. Las etiquetas tienen la forma <nombre>, donde nombre es el nombre del elemento que se está señalando.

A continuación se muestra un ejemplo para entender la estructura de un documento XML:
``` XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE Edit_Mensaje SYSTEM "Edit_Mensaje.dtd">

<Edit_Mensaje>
     <Mensaje>
          <Remitente>
               <Nombre>Nombre del remitente</Nombre>
               <Mail> Correo del remitente </Mail>
          </Remitente>
          <Destinatario>
               <Nombre>Nombre del destinatario</Nombre>
               <Mail>Correo del destinatario</Mail>
          </Destinatario>
          <Texto>
               <Asunto>
                    Este es mi documento con una estructura muy sencilla 
                    no contiene atributos ni entidades...
               </Asunto>
               <Parrafo>
                    Este es mi documento con una estructura muy sencilla 
                    no contiene atributos ni entidades...
               </Parrafo>
          </Texto>
     </Mensaje>
</Edit_Mensaje>
```
Aquí está el ejemplo de código del DTD del documento «Edit_Mensaje.dtd»:
``` XML
<?xml version="1.0" encoding="ISO-8859-1" ?>
<!-- Este es el DTD de Edit_Mensaje -->

<!ELEMENT Mensaje (Remitente, Destinatario, Texto)*>
<!ELEMENT Remitente (Nombre, Mail)>
<!ELEMENT Nombre (#PCDATA)>
<!ELEMENT Mail (#PCDATA)>
<!ELEMENT Destinatario (Nombre, Mail)>
<!ELEMENT Nombre (#PCDATA)>
<!ELEMENT Mail (#PCDATA)>
<!ELEMENT Texto (Asunto, Parrafo)>
<!ELEMENT Asunto (#PCDATA)>
<!ELEMENT Parrafo (#PCDATA)>
```  
## YAML Ain't Markup Languaje
es un formato de serialización de datos legible por humanos inspirado en lenguajes como XML, C, Python, Perl, así como en el formato de los correos electrónicos (RFC 2822). YAML fue propuesto por Clark Evans en 2001, quien lo diseñó junto a Ingy döt Net y Oren Ben-Kiki.

A comienzos de su desarrollo, YAML significaba Yet Another Markup Language (‘otro lenguaje de marcado más’) para distinguir su propósito centrado en los datos en lugar del marcado de documentos. Sin embargo, dado que se usa frecuentemente XML para serializar datos y XML es un auténtico lenguaje de marcado de documentos, es razonable considerar YAML como un lenguaje de marcado ligero. 

### Caracteristicas
fue creado bajo la creencia de que todos los datos pueden ser representados adecuadamente como combinaciones de listas, hashes (mapeos) y datos escalares (valores simples). La sintaxis es relativamente sencilla y fue diseñada teniendo en cuenta que fuera muy legible pero que a la vez fuese fácilmente mapeable a los tipos de datos más comunes en la mayoría de los lenguajes de alto nivel. Además, YAML utiliza una notación basada en la sangría y/o un conjunto de caracteres Sigil distintos de los que se usan en XML, haciendo que sea fácil componer ambos lenguajes.

* Los contenidos en YAML se describen utilizando el conjunto de caracteres imprimibles de Unicode, bien en UTF-8 o UTF-16.
* La estructura del documento se denota indentando con espacios en blanco; sin embargo no se permite el uso de caracteres de tabulación para sangrar.
* Los miembros de las listas se denotan encabezados por un guion ( - ) con un miembro por cada línea, o bien entre corchetes ( [   ] ) y separados por coma espacio ( ,   ).
* Los vectores asociativos se representan usando los dos puntos seguidos por un espacio. en la forma "clave: valor", bien uno por línea o entre llaves ( {   } ) y separados por coma seguida de espacio ( ,   ).
* Un valor de un vector asociativo viene precedido por un signo de interrogación ( ? ), lo que permite que se construyan claves complejas sin ambigüedad.
* Los valores sencillos (o escalares) por lo general aparecen sin entrecomillar, pero pueden incluirse entre comillas dobles ( " ), o comillas simples ( ' ).
* En las comillas dobles, los caracteres especiales se pueden representar con secuencias de escape similares a las del lenguaje de programación C, que comienzan con una barra invertida ( \ ).
* Se pueden incluir múltiples documentos dentro de un único flujo, separándolos por tres guiones ( --- ); los tres puntos ( ... ) indican el fin de un documento dentro de un flujo.
* Los nodos repetidos se pueden denotar con un ampersand ( & ) y ser referidos posteriormente usando el asterisco ( * )
* Los comentarios vienen encabezados por la almohadilla ( # ) y continúan hasta el final de la línea.
* Los nodos pueden etiquetarse con un tipo o etiqueta utilizando el signo de exclamación( ! ) seguido de una cadena que puede ser expandida en una URL.
* Los documentos YAML pueden ser precedidos por directivas compuestas por un signo de porcentaje ( % ) seguidos de un nombre y parámetros delimitados por espacios.. Hay definidas dos directivas en YAML 1.1:
  - La directiva %YAML se utiliza para identificar la versión de YAML en un documento dado.
  - La directiva %TAG se utiliza como atajo para los prefijos de URIs. Estos atajos pueden ser usados en las etiquetas de tipos de nodos.

### Ejemplos
#### ***Listas***
``` YAML
 --- # Películas favoritas, formato de bloque
 - BotijoAzul
 - BotijoVerde
 - Viridiana
 - Psicosis
 ...
 --- # Lista de la compra, formato en línea
 [leche, pan, huevos]
 [chorizo, morcilla, botijo, pollo]
``` 
#### ***Vectores asociativos***
``` YAML
 --- # Bloque
 nombre: Pepe López
 edad: 33
 --- # En  línea
 {nombre: Pepe López, edad: 33}
```
Literales de bloque
Preservando retornos de línea
``` YAML
 --- |
  El texto mantiene su estructura,
  en el sentido que preserva los retornos de línea.
  
  Esto incluye también líneas en blanco.
```
### ***Ignorando retornos de línea***
``` YAML
 --- >
  El texto rodeado 
  será formateado 
  como un único
  párrafo
  
  Las líneas en blanco
  denotan saltos de párrafo.
```
#### ***Listas de vectores asociativos***
``` YAML
 - {nombre: Pepe López, edad: 33}
 - nombre: Maria Garcia
   edad: 27
```
#### ***Vectores asociativos de listas***
``` YAML
 hombres: [Pepe Lopez, Guillermo Garcia]
 mujeres:
  - María García
  - Susana Márquez
```
## JSON JavaScript Object Notation
es un formato de texto sencillo para el intercambio de datos. Se trata de un subconjunto de la notación literal de objetos de JavaScript, aunque, debido a su amplia adopción como alternativa a XML, se considera (año 2019) un formato independiente del lenguaje.

Una de las supuestas ventajas de JSON es que en el 2022 ya no es desarrollado sobre XML como formato de intercambio de datos es que resulta mucho más sencillo escribir un analizador sintáctico (parser) para él. En JavaScript, un texto JSON se puede analizar fácilmente usando la función eval(), algo que (debido a la ubicuidad de JavaScript en casi cualquier navegador web) ha sido fundamental para que haya sido aceptado por parte de la comunidad de desarrolladores AJAX.

En la práctica, los argumentos a favor de la facilidad de desarrollo de analizadores o de sus rendimientos son poco relevantes, debido a las cuestiones de seguridad que plantea el uso de eval() y el auge del procesamiento nativo de XML incorporado en los navegadores modernos. Por esa razón, JSON se emplea habitualmente en entornos donde el tamaño del flujo de datos entre cliente y servidor es de vital importancia (de aquí su uso por Yahoo!, Google, Mozilla, etc, que atienden a millones de usuarios) cuando la fuente de datos es explícitamente de fiar y donde no es importante el hecho de no disponer de procesamiento XSLT para manipular los datos en el cliente.

Si bien se tiende a considerar JSON como una alternativa a XML, lo cierto es que no es infrecuente el uso de JSON y XML en la misma aplicación; así, una aplicación de cliente que integra datos de Google Maps con datos meteorológicos en SOAP (Simple Object Access Protocol) necesita hacer uso de ambos formatos.

En diciembre de 2005, Yahoo! comenzó a dar soporte opcional de JSON en algunos de sus servicios web.

### Sintaxis

Los tipos de datos disponibles con JSON son:
* **Números:** Se permiten números negativos y opcionalmente pueden contener parte fraccional separada por puntos. Ejemplo: 123.456
* **Cadenas:** Representan secuencias de cero o más caracteres. Se ponen entre doble comilla y se permiten cadenas de escape. Ejemplo: "Hola"
* **Booleanos:** Representan valores booleanos y pueden tener dos valores: true y false
* **null:** Representan el valor nulo.
* **Array:** Representa una lista ordenada de cero o más valores los cuales pueden ser de cualquier tipo. Los valores se separan por comas y el vector se mete entre corchetes. Ejemplo `["juan","pedro","jacinto"]`
* **Objetos:** Son colecciones no ordenadas de pares de la forma `<nombre>:<valor>` separados por comas y puestas entre llaves. El nombre tiene que ser una cadena entre comillas dobles. El valor puede ser de cualquier tipo. Ejemplo:
``` JSON
{
  "departamento":8,
  "nombredepto":"Ventas",
  "director": "Juan Rodríguez",
  "empleados":[
    {
      "nombre":"Pedro",
      "apellido":"Fernández"
    },{
      "nombre":"Jacinto",
      "apellido":"Benavente"
    } 
  ]
}
```
### Modelos de procesamiento

Al ser JSON un formato muy extendido para el intercambio de datos, se han desarrollado API para distintos lenguajes (por ejemplo ActionScript, C, C++, C#, ColdFusion, Common Lisp, Delphi, E, Eiffel, Java, JavaScript, ML, Objective-C, Objective CAML, Perl, PHP, Python, Rebol, Ruby, Lua y Visual FoxPro) que permiten analizar sintácticamente, generar, transformar y procesar este tipo de dato.

Los modelos de programación más utilizados para tratar con JSON en los distintos lenguajes son:

* **Modelo de objeto.-** El JSON completo es almacenado en memoria en un formato de árbol. Este árbol es navegado, analizado y modificado con las API apropiadas. Como lo carga todo en memoria y luego lo procesa este modelo consume muchos recursos. Sin embargo es muy flexible para manipular el contenido. Este modelo es permitido por ejemplo en Java por la JSR 353 y por la biblioteca Jackson.
* **Modelo de flujo:** Los datos son leídos o escritos en bloques. Por ejemplo, cada vez que se lee un bloque, el analizador genera eventos apropiados para indicar el tipo de bloque de que se trata. El cliente puede procesar el contenido escuchando los eventos apropiados. Además es el cliente el que decide como se va leyendo el JSON permitiendo parar o saltar contenidos en mitad del proceso. El proceso de escritura tiene propiedades análogas. Por ejemplo este modelo es permitido en java por la JSR 353.
* **Convirtiendo los objetos JSON en objetos del lenguaje.** En Java esto es realizado por ejemplo por las bibliotecas Jackson y Gson.

### Uso de JSON

En teoría, es trivial analizar JSON en JavaScript usando la función JSON.parse() incorporada en el lenguaje. Por ejemplo:
``` JAVASCRIPT
miObjeto = JSON.parse(json_datos);
```
En la práctica, las consideraciones de seguridad por lo general recomiendan no usar eval sobre datos crudos y debería usarse un analizador JavaScript distinto para garantizar la seguridad. El analizador proporcionado por JSON.org usa eval() en su función de análisis, protegiéndola con una expresión regular de forma que la función sólo ve expresiones seguras.

Un ejemplo de acceso a datos JSON usando XMLHttpRequest es:
``` javascript
var http_request = new XMLHttpRequest();
var url = "http://example.net/jsondata.php"; // Esta URL debería devolver datos JSON
 
// Descarga los datos JSON del servidor.
http_request.onreadystatechange = handle_json;
http_request.open("GET", url, true);
http_request.send(null);
 
function handle_json() {
  if (http_request.readyState == 4) {
    if (http_request.status == 200) {
      var json_data = http_request.responseText; 
      var the_object = eval("(" + json_data + ")");
    } else {
      alert("Ocurrió un problema con la URL.");
    }
    http_request = null;
  }
}
```
Obsérvese que el uso de XMLHttpRequest en este ejemplo no es compatible con todos los navegadores, ya que existen variaciones sintácticas para Internet Explorer, Opera, Safari, y navegadores basados en Mozilla.6​

También es posible usar elementos `<iframe>` ocultos para solicitar los datos de manera asíncrona, o usar peticiones `<form target="url_to_cgi_script" />`. Estos métodos eran los más habituales antes del advenimiento del uso generalizado de XMLHttpRequest.

Hay una biblioteca7​ para el framework .NET que exporta clases .NET con la sintaxis de JSON para la comunicación entre cliente y servidor, en ambos sentidos.
Ejemplo de JSON

A continuación se muestra un ejemplo simple de definición de barra de menús usando JSON y XML.

JSON:
``` JSON
{
    "menu": {
        "id": "file",
        "value": "File",
        "popup": {
            "menuitems": [
                {
                    "value": "New", "onclick": "CreateNewDoc()"
                },{
                    "value": "Open", "onclick": "OpenDoc()"
                },{
                    "value": "Close", "onclick": "CloseDoc()"
                }
            ]
        }
    }
}
```
Es una posible representación JSON del siguiente XML:
``` XML
  <menu id="file" value="File">
    <popup>
      <menuitem value="New" onclick="CreateNewDoc()" />
      <menuitem value="Open" onclick="OpenDoc()" />
      <menuitem value="Close" onclick="CloseDoc()" />
    </popup>
  </menu>
``` 
### Comparación con XML y otros lenguajes de marcado

Hay muchos analizadores JSON en el lado del servidor, existiendo al menos un analizador para la mayoría de los entornos. En algunos lenguajes, como Java o PHP, hay diferentes implementaciones donde escoger. En JavaScript, el análisis es posible de manera nativa con la función `JSON.parse()`. Ambos formatos carecen de un mecanismo para representar grandes objetos binarios.

Con independencia de la comparación con XML, JSON puede ser muy compacto y eficiente si se usa de manera efectiva. Por ejemplo, la aplicación DHTML de búsqueda en «BarracudaDrive» (en inglés). Archivado desde el original el 21 de mayo de 2006. recibe los listados de directorio como JSON desde el servidor. Esta aplicación de búsqueda está permanentemente consultando al servidor por nuevos directorios, y es notablemente rápida, incluso sobre una conexión lenta.

Los entornos en el servidor normalmente requieren que se incorpore una función u objeto analizador de JSON. Algunos programadores, especialmente los familiarizados con el lenguaje C, encuentran JSON más natural que XML, pero otros desarrolladores encuentran su escueta notación algo confusa, especialmente cuando se trata de datos fuertemente jerarquizados o anidados muy profundamente.

### Hay más comparaciones entre JSON y XML en JSON.

YAML es un superconjunto de JSON que trata de superar algunas de las limitaciones de este. Aunque es significativamente más complejo,9​ aún puede considerarse como ligero. El lenguaje de programación Ruby utiliza YAML como el formato de serialización por defecto. Así pues, es posible manejar JSON con bastante sencillez. 