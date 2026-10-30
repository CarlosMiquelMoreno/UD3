# Práctica: Configuración de ACL en LINUX - Caso Torrent S.L.

## TAREAS A REALIZAR

Tarea 1 - Preparar el entorno
1. Comprueba que el soporte de ACL está disponible en tu sistema:
<img width="695" height="376" alt="image" src="https://github.com/user-attachments/assets/45d4f42a-308e-4cff-9794-2cc1188312d8" />

2. Crea los tres grupos y los nueve usuarios del enunciado, asignando a cada usuario su grupo correspondiente.
<img width="518" height="117" alt="image" src="https://github.com/user-attachments/assets/b552762c-68a7-46f4-aa0d-d15cc9be2bf4" />
<img width="773" height="210" alt="image" src="https://github.com/user-attachments/assets/35b2ca06-401c-443e-bd85-1bd43eefab85" />

3. Crea la estructura de ficheros: un fichero (o script) ejecutable llamado hmi_planta, y una carpeta planos/ con los ficheros autoclave.dwg, caldera.dwg y destilacion.dwg.
<img width="747" height="115" alt="image" src="https://github.com/user-attachments/assets/7630ce13-e691-4f1a-a12a-f069884dbaed" />

Tarea 2 - Permisos base (propietario/grupo/resto)
4. Decide qué usuario y qué grupo deben ser propietarios de hmi_planta y de planos/ (por ejemplo, un usuario de sistemas o de ingeniería).
5. Aplica con chmod unos permisos de partida restrictivos (por ejemplo 750 o 700), de forma que el resto del acceso tenga que concederse explícitamente mediante ACL.
<img width="790" height="178" alt="image" src="https://github.com/user-attachments/assets/8a98bcd7-7667-4659-aa6b-2221fb6bf0ff" />

Tarea 3 - Configurar las ACL con setfacl
6. Aplica las ACL necesarias sobre hmi_planta.
<img width="852" height="75" alt="image" src="https://github.com/user-attachments/assets/8aabe3bb-df52-4749-8989-94d3df885298" />

7. Aplica las ACL necesarias sobre la carpeta planos/ y, si procede, sobre los ficheros que ya contiene.
<img width="847" height="74" alt="image" src="https://github.com/user-attachments/assets/841dc215-ba54-410e-88d0-5cdde1721745" />

8. Valora si alguno de los permisos del diagrama debería aplicarse también como ACL por defecto (setfacl -d), para que los ficheros nuevos que se creen en planos/ hereden automáticamente esos permisos.
<img width="857" height="74" alt="image" src="https://github.com/user-attachments/assets/5a0a78ba-1d22-4d99-89ab-3edbbcb1e2c6" />

Tarea 4 - Verificación

Antes de la verificación, viendo las imagenes he visto que he escrito algunos comandos mal, aqui están bien.
<img width="873" height="93" alt="image" src="https://github.com/user-attachments/assets/ce343d71-26e8-41ce-ba10-630718f46fb0" />

9. Comprueba el resultado con getfacl sobre cada recurso
<img width="613" height="754" alt="image" src="https://github.com/user-attachments/assets/c7d99539-daaf-4eb3-ac51-7e71511da374" />

## Preguntas de reflexión

1. ¿Por qué no bastan los permisos clásicos de Unix (usuario / grupo / resto) para implementar el esquema del diagrama? Pon un ejemplo concreto de este caso.

Los permisos clásicos de Unix solo asignan a un propietario y a un grupo, si un archivo o directorio necesita que 3 o mas de sus colectivos tenga diferentes permisos, es sistema petaría.

Imagina que la propiedad de la carpeta al administrador osea la (root:root) usára los permisos clásicos.

-Solo podemos elegir un grupo propietario para el recurso. A ingenieria le daremos los permisos de lectura y escritura (rw-).

-Al ya no tener mas casillas de "grupo", los otros 2, operarios y supervisores, caen si o si en la categoría de otros.

-Como operarios y supervisores estan en el mismo, no se pueden diferenciar, si a otros les damos los permisos de lectura (r--), cualquiera podría leer.


2. ¿Qué es la máscara (mask) de una ACL y cómo afecta a los permisos efectivos de un usuario o grupo, aunque su entrada de ACL indique más permisos?

La máscara de una ACL es la que define que permisos pueden tener los usuarios y grupos nombrados y funciona como un filtro lógico (AND). Si a un grupo le asignas los permisos de (rwx) y la mascara del ACL esta puesta como (r-x), mandara ella por encima de la otr configuración.

3. ¿Qué diferencia hay entre una ACL de acceso y una ACL por defecto? ¿Cuándo se aplica cada una?

La ACL de acceso es la que se aplica al instante a un archivo o directorio y se aplica cada vez que un usuario intenta interactuar con un recurso.

La ACL por defecto es una plantilla de permisos que solo esta para lso directorios y se aplica automáticamente a cualquier archivo o subcarpeta que crea.

4. Si mañana se incorpora un nuevo operario, ¿qué pasos tendrías que repetir para darle exactamente el mismo acceso que al resto de operarios?

Ninguno que tenga que ver con las ACL, ya que ya las hemos hecho.

Solo tendria que añadirlo como usuario en operarios 'sudo useradd -m -g operarios -s /bin/bash nuevo_operario'.
