# Práctica: Certificados y HTTPS: de nuestra propia CA a Let’s Encrypt

## Tareas a realizar

PARTE 1 Nuestra propia autoridad de certificación

Paso 0 — Instalar Apache y comprobar que funciona (todavía sin cifrar)
<img width="892" height="282" alt="image" src="https://github.com/user-attachments/assets/78d3dda5-16cb-4936-ba63-5c3bc68e7ac7" />
<img width="577" height="92" alt="image" src="https://github.com/user-attachments/assets/1740d845-0720-429b-88ad-f5a7c892229f" />
<img width="820" height="262" alt="image" src="https://github.com/user-attachments/assets/c0d46004-c29a-43de-998a-c01bbec2789a" />
Dice que la conexion no es seguro debido a que estamos usando HTTP.

Paso 1 — Crear una carpeta de trabajo para la CA
<img width="537" height="65" alt="image" src="https://github.com/user-attachments/assets/3ed42592-27b7-43d7-af7a-d174875d6eaa" />

Paso 2 — Generar la clave privada de la CA
<img width="726" height="67" alt="image" src="https://github.com/user-attachments/assets/03f6fd90-a190-47eb-84af-9e070209a686" />
Conviene porque si algun atacante consigue entrar en cuenta root los permisos ya no sirven

Paso 3 — Crear el certificado raíz de la CA (autofirmado)
<img width="880" height="111" alt="image" src="https://github.com/user-attachments/assets/6668f60d-f9db-4c40-a420-34f369d35eaf" />
<img width="877" height="95" alt="image" src="https://github.com/user-attachments/assets/e97e6eb6-2a54-4001-a646-a8d5b12f7de4" />

Paso 4 — Inspeccionar el certificado que acabas de crear
<img width="883" height="162" alt="image" src="https://github.com/user-attachments/assets/78666147-0967-4967-80e6-651dcc789bef" />
Es el mismo por que se autofirma la CA y el certificado dura 10 años, osea 2036.

Paso 5 — Clave privada del servidor y petición de certificado (CSR)
<img width="765" height="68" alt="image" src="https://github.com/user-attachments/assets/e6c1e019-7d47-49d8-aa49-8e720c2407e8" />

Paso 6 — Indicar para qué nombres e IP es válido el certificado (SAN)
<img width="617" height="121" alt="image" src="https://github.com/user-attachments/assets/29973d0e-eeac-4866-b913-124d9b04e967" />

Paso 7 — La CA firma el certificado del servidor
<img width="875" height="111" alt="image" src="https://github.com/user-attachments/assets/9b643ec5-48fc-45ad-b33f-e70bbb4888b5" />
Es por si alguien roba la clave privada del certificado del servidor.

Paso 8 — Verificar la cadena de confianza
<img width="877" height="180" alt="image" src="https://github.com/user-attachments/assets/08c838c0-f230-405c-b8f1-240d6a32e89f" />

Paso 9 — Instalar el certificado en Apache
<img width="890" height="355" alt="image" src="https://github.com/user-attachments/assets/f77041a5-29db-4fa6-8090-4b23b54d2113" />
<img width="707" height="86" alt="image" src="https://github.com/user-attachments/assets/f52d6171-7e10-4b2d-b063-9563e91c092d" />
<img width="881" height="243" alt="image" src="https://github.com/user-attachments/assets/3a06849f-b168-4bf9-98db-b7ace528812d" />

Paso 10 — Probar HTTPS desde la propia VM, antes de confiar en la CA
<img width="768" height="161" alt="image" src="https://github.com/user-attachments/assets/ba32488b-216c-453e-b878-0380476c4db0" />
<img width="797" height="215" alt="image" src="https://github.com/user-attachments/assets/7dd7fdeb-0e45-438d-b3fb-962db943bd13" />
El primero falla por que no conoce la CA de torrent S.L. cosa que en el segundo si

Paso 11 — El navegador: advertencia, huella e importación de la CA
<img width="873" height="95" alt="image" src="https://github.com/user-attachments/assets/6bf15b27-dee4-4c51-82fc-6716e212a984" />
<img width="892" height="822" alt="image" src="https://github.com/user-attachments/assets/00bfc81f-8dab-44e4-8824-4c27408f74e0" />
<img width="656" height="280" alt="image" src="https://github.com/user-attachments/assets/5189db4e-6855-43b3-a36b-543593086cb5" />

Paso 12 — Mirar la conexión TLS por dentro
<img width="872" height="247" alt="image" src="https://github.com/user-attachments/assets/5daa1740-887b-4e14-b132-2bf7c257e1da" />
Si quitas la opcion CAfile, openssl rechaza porque busca al emisor en el almacen del SO

Paso 13 — Guardar lo hecho para la Fase 2
<img width="662" height="25" alt="image" src="https://github.com/user-attachments/assets/9d7be5af-3308-46a7-9c57-c4eb347e918c" />
1. Explica con tus palabras la diferencia entre ca.key, ca.crt, srv.key y srv.crt: ¿cuáles son secretos y cuáles públicos?

La ca.key y la srv.key son las claves privadas y nunca salen ni se comparten y los crt son los certificados publicos que se van enviando navegadores y clientes.

2. Alguien roba ca.key (sin contraseña). ¿Qué puede hacer con ella? ¿Qué tendría que hacer Torrent S.L. para recuperar la confianza?

El atacante puede firmar certificados falsos para suplantar paginas web de empleados, tendrian que borrar el certificado de raiz y de todos los dispositivos de la empresa y crear una nueva CA desde cero.

3. ¿Por qué descargar ca.crt por HTTP y no verificar la huella es un riesgo? ¿Quién podría aprovecharlo?

Al ir sin cifrar, un atacante que este en la red podria acceder y cambiar el archivo por su CA

4. ¿Es una buena idea que la CA y el servidor web estén en la misma máquina? ¿Qué problema de seguridad crea?

Es muy malo, si alguien hackea la web, tiene acceso a toda la empresa.



