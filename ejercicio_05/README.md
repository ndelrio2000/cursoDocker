Investigar que hacen y para que se usan los siguientes comandos dentro de un Dockerfile:

* HEALTHCHECK: Dentro de un Dockerfile, esta opción permite indicarle a Docker como debe testear la saludo de un contenedor para verificar su el mismo está o no funcionando. Puede detectar por ejemplo la salud de un servidor web que no esté atendiendo nuevas conexiones, independientemente de si el proceso se encuentra vivo o no. Cuando un contenedor es lanzado con el HEALDTHCHECK, tendrá un helth status adicional a su status normal. Este statos figurará inicialmente como starting. Cuando se realiza el chequeo al menos una vez, luego pasará a un estado de healthy (en caso de estar ok) o inhealthy (en caso de que el chequeo arroje error). Esta opción puede acompañarse con las siguientes opciones:
      --interval=DURATION (default: 30s)
      --timeout=DURATION (default: 30s)
      --start-period=DURATION (default: 0s)
      --retries=N (default: 3)
Solo puede existir una única instrucción HEALTHCHECK en un Dockerfile. En caso de haber mas de una, solo la última se tomará en consideración. CUalquier chequeo implementado deberá devolver alguno de los siguientes valores:
        0: success - the container is healthy and ready for use
        1: unhealthy - the container is not working correctly
        2: reserved - do not use this exit code
Un ejemplo de HEALTHCKECK en Dockerfile puede ser el siguiente:

        HEALTHCHECK --interval=5m --timeout=3s \
          CMD curl -f http://localhost/ || exit 1

* ONBUILD: Esta instrucción permite definir un disparador (trigger) que será ejecutado posteriormente. Por ejemplo una aplicación crea un entorno o dispara un proceso que debe ser customizado con alguna configuración específica. 
La forma de utilizarlo es:
      ONBUILD ADD . /app/src
      ONBUILD RUN /usr/local/bin/python-build --dir /app/src
Esta instrucción montará en /app/src el contenido del directorio actual desde donde es disparado el contenedor es ejecutado. Posteriormente elecutará el comando /usr/local/bin/python-build --dir /app/src. Todo esto, una vez que la imagen original (FROM) haya sido iniciada.

* VOLUME: Esta instrución crea un punto de montaje con el nombre especificado en el contenedor. Permite hacer un mapeo persistente de un volumen montado desde el host nativo u otro contenedor. Se le puede especificar un valor o bien un arreglo escrito en formato json. 
