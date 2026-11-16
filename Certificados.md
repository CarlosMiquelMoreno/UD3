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

 PARTE 2 Un certificado real y gratuito con Let’s Encrypt

 Paso 1 — Crear tu subdominio en DuckDNS
 <img width="842" height="105" alt="image" src="https://github.com/user-attachments/assets/17ffdeb1-b320-4a51-b289-14fd77335dea" />
 <img width="726" height="52" alt="image" src="https://github.com/user-attachments/assets/cd05a757-416a-4843-bbfb-952a93ebe24e" />

 Paso 2 — Instalar acme.sh (leyendo antes lo que se va a ejecutar)
<img width="806" height="177" alt="image" src="https://github.com/user-attachments/assets/768d7237-913d-42be-ac30-b190479a8a60" />
Al revisar el script de instalación se ve que crea el directorio oculto ~/.acme.sh donde copia sus archivos y scripts DNS, añade un alias en ~/.bashrc para facilitar la ejecución y programa una tarea automática diaria en cron para renovar los certificados antes de que caduquen.

Paso 3 — Elegir Let’s Encrypt como autoridad
<img width="802" height="62" alt="image" src="https://github.com/user-attachments/assets/2ec78aef-d5a5-4566-9469-307964233625" />
Si, sigue siendo el valido y necesario desde la version 3.0 de acme.sh, la herramienta que usa es ZeroSSL como autoridad, otras autoridares como google trust services, buypass Go SSL, SSL.com, etc.

Paso 4 — Pedir el certificado (desafío DNS-01)
<img width="880" height="557" alt="image" src="https://github.com/user-attachments/assets/36871090-cbe5-46f5-873f-f812b29f8af2" />
<img width="881" height="528" alt="image" src="https://github.com/user-attachments/assets/c224e7d5-8180-4fa7-95e1-859d70eb96c8" />

Paso 5 — Instalar el certificado donde Apache pueda usarlo
<img width="872" height="307" alt="image" src="https://github.com/user-attachments/assets/f67d29fc-0a29-4036-b881-fdbefed64b3d" />

Paso 6 — Cambiar Apache al certificado de Let’s Encrypt
<img width="887" height="128" alt="image" src="https://github.com/user-attachments/assets/64046e21-1eb7-48bc-a9c5-3bf77dc9cc47" />
<img width="871" height="128" alt="image" src="https://github.com/user-attachments/assets/4b3453fc-5e9f-446e-91d9-68254178f99b" />

Paso 7 — Comprobar el resultado
<img width="818" height="308" alt="image" src="https://github.com/user-attachments/assets/bd175162-dcd7-46fd-8d46-f4ce7e4633d5" />

Paso 8 — Mirar la cadena y la lista de CA de confianza
<img width="877" height="325" alt="image" src="https://github.com/user-attachments/assets/f75672b7-94e9-472c-b272-4656cd764e1a" />
No, no esta, solo lo he importado dentro del almacen del navegador, pero no lo he instalado.

Lo decide los proveedores de SO y navegadores, a traves de los programas de certificados raiz.

Paso 9 — La renovación automática
<img width="882" height="153" alt="image" src="https://github.com/user-attachments/assets/0f32bf04-c6d9-47bd-9ace-a3fe39fff29e" />

Completa la tabla con lo que has visto en la práctica (no con lo que crees saber):

|   | CA propia de Torrent S.L. | Let’s Encrypt |
| - | ------------------------- | ------------- |
| ¿Quien firma el certificado | Nuestra propia CA creada de raiz por nosotros. | Una autoridad publica (Let´s Encrypt). |
| ¿El navegador lo acepta sin hacer nada? | No, da una advertencia de seguridad. | Si, esta el icono de candado cerrado desde el principio. | 
| ¿Que tuviste que hacer para que confiara? | Descargar el certificado de torrent-ca.crt, comprobar la huella sha256 y impartarlo a los ajustes de firefox | Nada, ya viene asi de base. |
| Validez del certificado del servidor | Se le pone en la propia configuracion, en nuestro caso 1 año. | 90, basado en las politicas de Let´s Encrypt. |
| Coste y esfuerzo de renovarlo | Es gratis, pero hay que hacerlo por ti mismo. | Es gratis y automatico. |
| ¿Que se comprueba antes de firmar? | Nada, nosotros mismo las firmamos. | La propiedad de verdad del dominio, mediante DNS. |
| Valdria para un servidor sin internet? | Si porque funciona en red local. | No, necesitas accesso a internet. |

3. Preguntas finales
1. ¿Por qué el navegador confía en Let’s Encrypt y no en la CA de Torrent S.L.? ¿Quién decide en qué entidades confía un navegador?

El certificado de Let´s Encrypt viene ya instalado de base en el alamacen de confianza del navegador y del SO. Lo que pasa en el CA de Torrent S.L. es algo creado por nosotros, por lo que ningun navegador externo lo conoce.

Lo deciden los fabricantes de los navegadores(google, firefox, mozilla) a traves de programas de certificados raiz.

2. ¿Por qué los certificados de Let’s Encrypt duran solo 90 días? Piensa en qué pasa si alguien roba la clave privada del servidor.

Dura 90 dias por su politica de reducir el tiempo en el que si un atacante consigue de alguna manera obtener la clave privada, tenga un tiempo no tan duradero

3. La página interna de la planta de Torrent S.L. no tiene salida a Internet. ¿Qué CA usarías, la propia o Let’s Encrypt? ¿Y para la web pública de un cliente?

Para la interna la CA, al no estar conectada a internet el servidor no puede comunicarse con el Let´s Encrypt, donde si la usaria seria en la web publica, a gente externa no le podemos pedir que instalen siempre certificados.

4. HTTPS protege la confidencialidad y la integridad de lo que viaja. Pon dos ejemplos de ataques que HTTPS no impide.

El phising, osea, mostrara candado cerrado y trafico viajara cifrado pero sera una estafa.

Ataques de aplicacion web, como fuerza bruta o malware, HTTPS hace que nadie pueda entrar ni interferir en la comunicacion, pero pueden por medio de fallos de programacion,

5. Una empresa de 3 personas, ¿montaría una CA propia? ¿Cuándo sí tiene sentido? Relaciónalo con lo que haremos en la Fase 2 (VPN).

 No saldria comveniente, seria gasto de tiempo y mantenimiento innecesarios, es mejor el Let´s Encrypt.

 Tiene sentido en organizaciones mas grandes, ya que hay mas dispositivos.

 En una VPN, necesitamos autenticar al servidor y al cliente/empleado que este fuera. En este caso una CA propia es muy buena opcion para emitir y revocar los certificados de cada trabajador que pueda meterse por la VPN.
