# Práctica: Contraseñas, MFA y privilegios justos - Caso Torrent S.L.

## TAREAS A REALIZAR

PARTE 1 CONTRASEÑAS ROBUSTAS CON PAM


1.2 Instalar y activar pwquality
<img width="887" height="307" alt="image" src="https://github.com/user-attachments/assets/e399ff6a-f91d-4427-bbe1-d2c10ba27b64" />


1.3 Práctica guiada — aplicar la política
<img width="660" height="230" alt="image" src="https://github.com/user-attachments/assets/2ccacb3a-2dfd-43cc-afac-be86359c9bd0" />
<img width="736" height="23" alt="image" src="https://github.com/user-attachments/assets/e8606969-457e-4717-bf9a-35ea512807bd" />

<img width="662" height="70" alt="image" src="https://github.com/user-attachments/assets/aea5a4bd-bb26-460c-955c-480718de7fe8" />
<img width="385" height="90" alt="image" src="https://github.com/user-attachments/assets/eacd377a-dc19-4c49-abce-502d63a340d6" />
<img width="661" height="136" alt="image" src="https://github.com/user-attachments/assets/2a800009-8ab7-4c72-a395-ad767bde682a" />


1.4 Caducidad y aviso con chage
<img width="875" height="115" alt="image" src="https://github.com/user-attachments/assets/4cca0b39-8317-45a0-a2ee-7773fdac0e07" />


PARTE 2 MFA en SSH con Google Authenticator


2.2 Instalar el módulo PAM
<img width="732" height="200" alt="image" src="https://github.com/user-attachments/assets/92707f27-c315-45b9-b7ce-1554aced594d" />

2.3 Generar el secreto (lo hace cada usuario, con su propia cuenta)
<img width="877" height="107" alt="image" src="https://github.com/user-attachments/assets/eed61c97-937b-4aae-afe4-12c0765f420a" />

<img width="290" height="67" alt="image" src="https://github.com/user-attachments/assets/a8fa31b8-c3c2-4df1-a2a3-24e928a8c546" />


2.4 Conectar Google Authenticator con sshd
<img width="673" height="65" alt="image" src="https://github.com/user-attachments/assets/fbf32fca-4fcd-4d1e-a731-ffdd1a4be6c2" />
<img width="272" height="25" alt="image" src="https://github.com/user-attachments/assets/457e7e63-8400-4bbd-9e98-10cb8f43bb9a" />
<img width="340" height="27" alt="image" src="https://github.com/user-attachments/assets/0978a973-1ad0-4982-b4a2-5f8d28e0c0be" />
<img width="118" height="25" alt="image" src="https://github.com/user-attachments/assets/8e1e8f17-6a70-46c0-bcb3-8f5e30fb55eb" />

2.5 Verificación
1. Desde otra terminal (o desde el móvil con un cliente SSH), conéctate como el usuario que configuró el MFA.
Se abre una terminal y se inicia por SSH, el sistema solicita la contraseña, tras ponerla solicita el codigo de verificacion y los 6 digitos y el acceso se completa.

2. Comprueba que primero pide la contraseña y después el código de 6 dígitos de la app.

3. Prueba a escribir un código incorrecto y comprueba que la conexión se rechaza.
Si pasa esto, cuando pones un codigo que no es, el sistema rechaza y deniega el acceso.


2.6 ¿A quién se lo exigimos?
<img width="607" height="50" alt="image" src="https://github.com/user-attachments/assets/0417e3fd-541d-4de6-acd8-3202cb2c0069" />
<img width="877" height="53" alt="image" src="https://github.com/user-attachments/assets/7005f80a-7962-4cf3-a356-4b41bd077640" />
<img width="286" height="26" alt="image" src="https://github.com/user-attachments/assets/91f55438-b910-4699-8b42-d8578f170c77" />

PARTE 3 Privilegios justos con sudo

3.3 Práctica guiada
<img width="706" height="88" alt="image" src="https://github.com/user-attachments/assets/b6ff074c-31c8-4630-9151-53ce100f9e6e" />
<img width="876" height="72" alt="image" src="https://github.com/user-attachments/assets/943131a7-cd72-4e78-87bb-7bb72a73fad0" />


3.4 Verificación
<img width="875" height="637" alt="image" src="https://github.com/user-attachments/assets/9b155278-5af1-4fa8-bd8f-3a9962d3b9eb" />
<img width="567" height="87" alt="image" src="https://github.com/user-attachments/assets/9332c11c-e742-4767-8c94-0033baf61ccd" />
<img width="1852" height="461" alt="image" src="https://github.com/user-attachments/assets/2347bff1-618e-4cc1-bdfc-ee8545ccde95" />
<img width="742" height="45" alt="image" src="https://github.com/user-attachments/assets/5079ad8a-da04-44d5-b868-c4baae75e096" />

Preguntas de reflexión
1. Una contraseña de 20 caracteres aleatorios es, en teoría, casi imposible de reventar por fuerza bruta. ¿Qué riesgo concreto cubre el MFA que una contraseña así, por fuerte que sea, no cubre?

El MFA lo que cubre es el "algo que tienes", por el código en el movil de 30 segundos.

2. Buscad brevemente la postura actual del NIST sobre la caducidad obligatoria de contraseñas. ¿Por qué forzar el cambio cada pocos días puede llegar a ser contraproducente para la seguridad real?

Cambiar las contraseñas cada pocos dias, quiere decir que los usuarios cambian las contraseñas y como nunca se quedan con ninguna, las apuntan, afectando a su seguridad.

3. Aunque sudo esté perfectamente configurado, seguís necesitando las ACL de la sesión anterior. Explicad con un ejemplo por qué una capa no sustituye a la otra.

Si un usuario de ingenieria tiene permisos sudo para reiniciar el hmi_planta, pero no esta configurado el ACL, cualquier usuario sin sudo puedo entrar directo a la carpeta y borrarlos o copiarlos.

4. Un alumno pierde el móvil con Google Authenticator y no guardó los scratch codes. ¿Qué tendría que hacer el administrador del sistema para devolverle el acceso sin comprometer la seguridad del resto de cuentas?

Deberia el admin conectarse con root y eliminar o renombrar el archivo de  google_autheticator en la carpeta de el usuario que ha perdido el movil.


