# Variables de Entorno
### ¿Qué son las variables de entorno?
Son valores almacenados en el sistema operativo que programas y scripts pueden usar para obtener información importante, como rutas de archivos, configuraciones o credenciales.

### Para crear un contenedor con variables de entorno?

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.

```
docker run -d --name nginx -e username=rodrigo -e role=admin nginx:alpine
```

![Imagen](img/dockerVariables.png)
![Imagen](img/dockerRole.png)

### Crear un contenedor con mysql:8 , mapear todos los puertos
```
docker run -P -d --name mysql mysql:8
```

### ¿El contenedor se está ejecutando?
El contenedor intenta arrancar pero inmediante detiene su ejecución.

### Identificar el problema
En la creación del contenedor no se especificó la variable de entorno ```MYSQL_ROOT_PASSWORD```, por tanto al intentar ejecutar el contenedor resulta en un error.

### Eliminar el contenedor creado con mysql:8 
```
docker rm -f mysql
```


### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

Previo a esto es necesario crear el archivo y colocar las variables en un archivo, **.env** se ha convertido en una convención estándar, pero también es posible usar cualquier extensión como **.txt**.
```
docker run -d --name <nombre contenedor> --env-file=<nombreArchivo>.<extensión> <nombre imagen>
```
**Considerar**
Es necesario especificar la ruta absoluta del archivo si este se encuentra en una ubicación diferente a la que estás ejecutando el comando docker run.

### Crear un contenedor con mysql:8 , mapear todos los puertos y configurar las variables de entorno mediante un archivo
```
docker run -P -d --name mysql --env-file=variablesEntorno.txt mysql:8
```

![Imagen](img/dockerMysql.png)

### ¿Qué bases de datos existen en el contenedor creado?
El contenedor posee las siguientes bases de datos: information_schema, mysql, performance_schema, sys.

![Imagen](img/dockerDB.png)

