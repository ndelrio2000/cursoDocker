# cursoDocker

Ejercicio_04 https://hub.docker.com/r/ndelrio/passwordapi-ndelrio

Creado a través del siguiente Dockerfile:
FROM anapsix/alpine-java
MAINTAINER ndelrio
COPY passwordapi.jar /home/passwordapi.jar
EXPOSE 8080
CMD ["java","-jar","/home/passwordapi.jar"]

