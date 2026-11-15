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


