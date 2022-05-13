Instalacion de PostgreSQL


# Instalacion de PostgreSQL

## Paso 1: Instalar PostgreSQL
Los repositorios predeterminados de Ubuntu contienen paquetes de Postgres, para que pueda instalarlos utilizando el sistema de empaquetado apt.

Si no lo hizo recientemente, actualice el índice del paquete local de su servidor:
```shell
    sudo apt update
``` 
Luego, instale el paquete de Postgres junto con un paquete -contrib, que agrega algunas utilidades y funcionalidades adicionales:
```shell
    sudo apt install postgresql postgresql-contrib
```
Ahora que el software está instalado, podemos analizar su funcionamiento y la forma en que puede diferenciarse de otros sistemas de administración de bases de datos relacionales que pueda haber utilizado.

## Paso 2: Utilizar roles y bases de datos de PostgreSQL
Por defecto, **Postgres utiliza un concepto llamado “roles” para gestionar la autenticación y la autorización**. Estos son, en algunos aspectos, parecidos a las cuentas normales de estilo Unix, pero Postgres no distingue entre los usuarios y los grupos, y en su lugar prefiere el término más flexible de “rol”.

Tras la instalación, **Postgres se configura para usar la autenticación ident.** Esto significa que asocia los roles de Postgres con una cuenta de sistema Unix o Linux correspondiente. Si existe un rol dentro de Postgres, un nombre de usuario de Unix o Linux con el mismo nombre puede iniciar sesión ocupando ese rol.

**El procedimiento de instalación creó una cuenta de usuario llamada postgres, que se asocia con el rol predeterminado de Postgres.** Para usar Postgres, puede iniciar sesión en esa cuenta.

Existen algunas maneras de usar esta cuenta para acceder a Postgres.
### ***Cambiar a la cuenta de postgres***
Cambie a la cuenta de postgres en su servidor escribiendo lo siguiente:
```shell
    sudo -i -u postgres
```
Ahora, puede acceder de inmediato a una línea de comandos de PostgresSQL al escribir lo siguiente:
```shell
    psql
```
Allí, puede interactuar con el sistema de administración de bases de datos como sea necesario.

Salga de la línea de comandos de PostgreSQL escribiendo lo siguiente:
```shell
    \q
```
Con esto, regresará a la línea de comandos de Linux de postgres.
### ***Acceder a una línea de comandos de Postgres sin cambiar de cuenta***
También puede ejecutar el comando que desee con la cuenta de postgres de forma directa a través de sudo.

Por ejemplo, en el último caso se le indicó acceder a la línea de comandos de Postgres pasando primero al usuario de postgres y luego ejecutando psql para abrir la línea de comandos de Postgres. Puede realizarlo en un solo paso ejecutando el comando único psql como usuario de postgres con sudo, como se muestra:
```shell
    sudo -u postgres psql
```
Esto le permitirá iniciar sesión de forma directa en Postgres sin el shell bash intermediario entre ellos.

De nuevo, puede salir de la sesión interactiva de Postgres escribiendo lo siguiente:
```shell
    \q
```
Para muchos casos de uso se requiere más de un rol de postgres. Continúe leyendo para saber cómo configurar estos roles.

## Paso 3: Crear un nuevo rol
En este momento, solo tiene el rol de postgres configurado dentro de la base de datos. Puede crear nuevos roles desde la línea de comandos con el comando `createrole`. El indicador --interactive le solicitará el nombre del nuevo rol y también le preguntará si debería tener permisos de superusuario.

Si inició sesión a través de la cuenta de postgres, puede crear un nuevo usuario escribiendo lo siguiente:
```shell
    createuser --interactive
```
Si, como alternativa, prefiere usar sudo para cada comando sin dejar de usar su cuenta normal, escriba lo siguiente:
```shell
    sudo -u postgres createuser --interactive
```
La secuencia de comandos le mostrará algunas opciones y, según sus respuestas, ejecutará los comandos correctos de Postgres para crear un usuario conforme a sus especificaciones.
```shell
Output
Enter name of role to add: sammy
Shall the new role be a superuser? (y/n) y
```
Puede obtener un mayor control pasando algunos indicadores adicionales. Consulte las opciones visitando la página de man:
```shell
    man createuser
```
Ahora su instalación de Postgres tiene un usuario nuevo, pero aún no agregó bases de datos. En la sección siguiente se describe este proceso.

## Paso 4: Crear una nueva base de datos
Otra **suposición que el sistema de autenticación de Postgres realiza por defecto es que para cualquier rol utilizado en el inicio de sesión habrá una base de datos con el mismo nombre al que este podrá acceder**.

Esto significa que, si el usuario que creó en la última sección se llama sammy, ese rol intentará conectarse con una base de datos que, por defecto, también se llama “sammy”. Puede crear la base de datos apropiada con el comando `createdb`.

Si inició sesión a través de la cuenta de postgres, escribiría algo similar a lo siguiente:
```shell
    createdb sammy
```
Si, como alternativa, prefiere utilizar sudo para cada comando sin dejar de emplear su cuenta normal, escribiría lo siguiente:
```shell
    sudo -u postgres createdb sammy
```
Esta flexibilidad ofrece varias vías para crear bases de datos cuando sea necesario.

## Paso 5: Abrir una línea de comandos de Postgres con el nuevo rol
Para iniciar sesión con la autenticación basada en ident, necesitará un usuario de Linux con el mismo nombre de su rol y su base de datos de Postgres.

Si no tiene un usuario disponible de Linux que coincida, puede crear uno con el comando `adduser`. Deberá hacerlo desde su cuenta `non-root` con privilegios sudo (es decir, sin iniciar sesión como usuario de postgres):
```shell
    sudo adduser sammy
```
Una vez que esté disponible esta cuenta nueva, podrá cambiar y conectarse a la base de datos escribiendo lo siguiente:
```shell
    sudo -i -u sammy
    psql
```
También podrá hacerlo de forma directa:
```shell
    sudo -u sammy psql
```
Este comando le permitirá iniciar sesión de forma automática, suponiendo que todos los componentes se hayan configurado de forma correcta.

Si desea que su usuario se conecte a una base de datos diferente, puede lograrlo especificando la base de datos de esta manera:
```shell
    psql -d postgres
```
Ya que inició sesión, puede verificar la información de su conexión actual escribiendo lo siguiente:
```shell
    \conninfo

Output
You are connected to database "sammy" as user "sammy" via socket in "/var/run/postgresql" at port "5432".
```
Esto resultará útil si se conecta a bases de datos no predeterminadas o con usuarios no predeterminados.

## Paso 6: Crear y eliminar tablas
Ahora que sabe cómo conectarse al sistema de bases de datos de PostgreSQL, puede aprender algunas tareas básicas de administración de Postgres.

La sintaxis básica para la creación de tablas es la siguiente:
```shell
CREATE TABLE table_name (
    column_name1 col_type (field_length) column_constraints,
    column_name2 col_type (field_length),
    column_name3 col_type (field_length)
);
```
Como puede observar, estos comandos otorgan un nombre a la tabla y luego definen las columnas, el tipo de columna y la extensión máxima de los datos de campo. De manera opcional, también puede añadir restricciones de tabla para cada columna.

Para fines de demostración, cree la siguiente tabla:
```shell
    CREATE TABLE playground (
        equip_id serial PRIMARY KEY,
        type varchar (50) NOT NULL,
        color varchar (25) NOT NULL,
        location varchar(25) check (location in ('north', 'south', 'west', 'east', 'northeast', 'southeast', 'southwest', 'northwest')),
        install_date date
    );
```
Este comando creará una tabla que realiza un inventario de equipos para áreas recreativas. La primera columna de la tabla contendrá números de ID de equipos de tipo serial, que es un entero que se incrementa de forma automática. Esta columna también tiene la limitación de PRIMARY KEY, lo que significa que los valores en su interior deben ser únicos y no pueden ser nulos.

Las siguientes dos líneas crean columnas para type y color de los equipos respectivamente, que no pueden estar vacías. La siguiente línea crea una columna location y una restricción que requiere que el valor sea uno de los ocho valores posibles. La última línea crea una columna de fecha en la cual se registra la fecha en la que usted instaló el equipo.

Para dos de las columnas (equip_id e install_date), el comando no especifica una longitud de campo. Esto se debe a que algunos tipos de datos no requieren una longitud establecida, dado que la extensión o el formato están implícitos.

Puede ver su tabla nueva escribiendo lo siguiente:
```shell
    \d

Output
                  List of relations
 Schema |          Name           |   Type   | Owner
--------+-------------------------+----------+-------
 public | playground              | table    | sammy
 public | playground_equip_id_seq | sequence | sammy
(2 rows)
```
Su tabla de áreas de recreación se encuentra aquí, pero también existe algo llamado playground_equip_id_seq que responde al tipo sequence. Esto es una representación del tipo serial que usted atribuyó a su columna de equip_id. Esto realiza un seguimiento del número que sigue en la secuencia y se genera de forma automática para columnas de este tipo.

Si desea ver solo la tabla sin la secuencia, puede escribir lo siguiente:
```shell
    \dt

Output
          List of relations
 Schema |    Name    | Type  | Owner
--------+------------+-------+-------
 public | playground | table | sammy
(1 row)
```
Ahora que tenemos una tabla lista, la usaremos para practicar la administración de datos.

## Paso 7: Agregar, consultar y eliminar datos en una tabla
Ahora que tiene una tabla, puede insertar algunos datos en ella. Como ejemplo, añada un tobogán y un columpio al invocar la tabla en la que los desea agregar, nombrar las columnas y, luego, proporcionar datos para cada una de ellas de la siguiente forma:
```shell
INSERT INTO playground (type, color, location, install_date) VALUES ('slide', 'blue', 'south', '2017-04-28');

INSERT INTO playground (type, color, location, install_date) VALUES ('swing', 'yellow', 'northwest', '2018-08-16');
```
Debe tener cuidado al ingresar los datos para evitar algunos errores comunes. Para empezar, no escriba los nombres de las columnas entre comillas. Estás sí se necesitarán para los valores de la columna que ingresó.

Otro aspecto que debe tener en cuenta es no ingresar un valor para la columna equip_id. Esto se debe a que se genera de forma automática siempre que se añade una fila nueva a la tabla.

Recupere la información que agregó escribiendo lo siguiente:
```shell
    SELECT * FROM playground;

Output
 equip_id | type  | color  | location  | install_date
----------+-------+--------+-----------+--------------
        1 | slide | blue   | south     | 2017-04-28
        2 | swing | yellow | northwest | 2018-08-16
(2 rows)
```
Aquí, puede ver que su equip_id se completó con éxito y que todos sus otros datos se organizaron de forma correcta.

Si el tobogán del área de recreación se daña y tiene que eliminarlo, también puede eliminar la fila de su tabla escribiendo lo siguiente:
```shell
DELETE FROM playground WHERE type = 'slide';
```
Consulte la tabla de nuevo:
```shell
SELECT * FROM playground;

Output
 equip_id | type  | color  | location  | install_date
----------+-------+--------+-----------+--------------
        2 | swing | yellow | northwest | 2018-08-16
(1 row)
```
Observará que la fila de slide ya no se encuentra en la tabla.

## Paso 8: Agregar y eliminar columnas en una tabla

Después de crear una tabla, puede modificarla añadiendo o eliminando columnas. Agregue una columna para mostrar la última visita de mantenimiento por cada equipo escribiendo lo siguiente:
```shell
    ALTER TABLE playground ADD last_maint date;
```
Si vuelve a ver la información de su tabla, observará que se agregó la columna nueva, pero no se ingresaron datos:
```shell
SELECT * FROM playground;

Output
 equip_id | type  | color  | location  | install_date | last_maint
----------+-------+--------+-----------+--------------+------------
        2 | swing | yellow | northwest | 2018-08-16   |
(1 row)
```
Si determina que su equipo de trabajo utiliza una herramienta separada para dar seguimiento al historial de mantenimiento, puede eliminar la columna escribiendo lo siguiente:
```shell
ALTER TABLE playground DROP last_maint;
```
Con esto, se eliminan la columna last_maint y los valores que se encuentren en ella, pero deja intactos todos los demás datos.
Paso 9: Actualizar datos de una tabla

Hasta ahora, a través de este tutorial aprendió a agregar registros a una tabla y a eliminarlos de ella, pero aún no se abordó la forma de modificar los registros existentes.

Puede actualizar los valores de una entrada existente buscando el registro que desee y fijando el valor que prefiera utilizar para la columna. Puede consultar el registro de swing (se incluirán todos los columpios de su tabla) y cambiar su color a red. Esto puede ser útil si asignó una tarea de pintura al columpio:
```shell
    UPDATE playground SET color = 'red' WHERE type = 'swing';
```
Puede verificar la eficacia de la operación consultando los datos de nuevo:
```shell
SELECT * FROM playground;

Output
 equip_id | type  | color | location  | install_date
----------+-------+-------+-----------+--------------
        2 | swing | red   | northwest | 2018-08-16
(1 row)
```
Como puede ver, ahora, el columpio está registrado como rojo.