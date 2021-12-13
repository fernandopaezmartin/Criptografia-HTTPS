
![hhtp-https](https://github.com/fernandopaezmartin/Criptografia-HTTPS/blob/main/imagenes/hhtp-https.png)


# Criptografia HTTPS

Cada vez más las páginas web están protegidos por HTTPS. Con ésto indican que es segura. Esa diferencia con el protocolo tradicional de http quiere decir que es una navegación navegación web cifrada para comunicarse con otros servidores web.

Con "http" ocurre que todo se transmite en texto plano, sin cifrar por lo tanto, cualquiera que se conecte o que tenga acceso a la misma red donde nos encontramos, puede ver todos los datos que se reciben y se envían, por ejemplo, contraseñas de correo, o cuando se navega por la web de un banco.

# ¿Qué es HTTPS?

En el protocolo HTTP las URLs comienzan con "http://" y utilizan por omisión el puerto 80, las URLs de HTTPS comienzan con "https://" y utilizan el puerto 443 por omisión (También comúnmente usado el 4433). HTTP es inseguro y está sujeto a ataques man-in-the-middle.

SSL/TLS (Secure Sockets Layer/Transmission Layer Security) son dos protocolos o también algoritmo de cifrado híbrido, para enviar paquetes cifrados a través de Internet. Sirven igual para HTTP que para cualquier otro protocolo de comunicación.

Usa TLS para crear un canal cifrado (cuyo nivel de cifrado depende del servidor remoto y del navegador utilizado por el cliente) más apropiado para el tráfico de información sensible que el protocolo HTTP. De este modo se consigue que la información sensible (usuario y claves de paso normalmente) no pueda ser usada por un atacante que haya conseguido interceptar la transferencia de datos de la conexión, ya que lo único que obtendrá será un flujo de datos cifrados que le resultará imposible de descifrar.

# Servidor web HTTPS

Para que funcione, el protocolo HTTPS necesita una forma de poder proporcionar privacidad, integridad e identificación en los sitios web. La manera de poder proporcionar esto se llama cifrado o encriptación.

Para preparar un servidor web que acepte conexiones HTTPS, el administrador del sitio debe crear un certificado de clave pública para el propio servidor. Este certificado debe estar firmado por una autoridad de certificación (CA) para que el navegador web lo acepte. La autoridad certifica que el titular del certificado es quien dice ser. Los navegadores web generalmente son distribuidos con los certificados raíz firmados por la mayoría de las autoridades de certificación (CA) por lo que estos pueden verificar certificados firmados por ellos.

# ¿Cómo funciona?

El servidor web envía una lista de versiones de SSL / TLS compatibles que hayan configurado, y un conjunto de algoritmos de cifrado con los que puede trabajar con el navegador web. Por otra parte, el navegador web también envía su lista también. Entonces, se elige la mejor versión de los protocolos SSL / TLS y el algoritmo de cifrado según las preferencias del servidor.

El servidor responderá al navegador web enviando su certificado, que incluye su clave pública para que pueda verificar la identidad del servidor web. El navegador comprueba que el certificado enviado por el servidor sea auténtico, y, entonces, el navegador genera una clave maestra para que tanto navegador como servidor puedan usarla más tarde cuando generen una clave única. Esta clave maestra previa es enviada al servidor usando la clave pública del servidor para cifrarla, y luego, es descifrada por el servidor usando su clave privada.

Todo hasta ahora ha sido mediante una comunicación abierta y no cifrada, excepto el envío de la clave maestra previa que fue cifrada usando claves asimétricas. Una vez recibido por el servidor la clave maestra previa, ambos generan un “secreto compartido” que es la clave simétrica que usarán, y es entonces cuando todos los datos que van y vienen entre el navegador y servidor están asegurados para el resto de la sesión.

SSL/TLS funciona de forma transparente para el usuario.


# Seguridad

La seguridad de HTTPS depende de la del TLS, que normalmente utiliza claves públicas y privadas a largo plazo para generar una clave de sesión a corto plazo, que luego se utiliza para cifrar el flujo de datos entre el cliente y el servidor. Los certificados X.509 se utilizan para autenticar el servidor (y en ocasiones también el cliente). 
Por tanto, las autoridades certificadoras y los certificados de clave pública son necesarios para verificar la relación entre el certificado y su propietario, así como para generar, firmar y administrar la validez de los certificados. Si bien esto puede ser más beneficioso que verificar las identidades a través de una red de confianza.
Para que HTTPS sea efectivo, el sitio web debe estar completamente alojado en HTTPS. Si algunos de los contenidos del sitio se cargan a través de HTTP (scripts o imágenes, por ejemplo), o si solo una determinada página que contiene información confidencial, como una página de inicio de sesión, se carga a través de HTTPS mientras se carga el resto del sitio a través de HTTP simple, el usuario será vulnerable a ataques. Además, las cookies en un sitio servido a través de HTTPS deben tener habilitado el atributo seguro. En un sitio que tiene información confidencial, el usuario y la sesión quedarán expuestos cada vez que se acceda a ese sitio con HTTP en lugar de HTTPS.


# Ejemplo de comunicación segura

Cuando el navegador hace una petición al sitio seguro de Facebook por ejemplo, éste envía un mensaje donde indica que quiere establecer una conexión segura y envía datos sobre la versión del protocolo SSL/TLS que soporta y otros parámetros necesarios para la conexión.

En base a esta información enviada por el navegador, el servidor web de Facebook responde con un mensaje informando que está de acuerdo en establecer la conexión segura con los datos de SSL/TLS proporcionados.

Una vez que ambos conocen los parámetros de conexión, el sitio de Facebook presenta su certificado digital al navegador web para identificarse como un sitio confiable.

![fcbook](https://github.com/fernandopaezmartin/Criptografia-HTTPS/blob/main/imagenes/fcbook.png)

# Validez del Certificado

Una vez que el navegador tiene el certificado del sitio web de Facebook, realiza algunas verificaciones antes de confiar en el sitio:

- Integridad del certificado: Verifica que el certificado se encuentre íntegro, esto lo hace descifrando la firma digital incluida en él mediante la llave pública de la AC y comparándola con una firma del certificado generada en ese momento, si ambas son iguales entonces el certificado es válido.
- Vigencia del certificado: Revisa el periodo de validez del certificado, es decir,  la fecha de emisión y la fecha de expiración incluidos en él.

## Certificado de Facebook

![Certifcbook](https://github.com/fernandopaezmartin/Criptografia-HTTPS/blob/main/imagenes/Certifcbook.png)

## Certificado raiz en el navegador, emitido por CA DigiCert Inc

![CA_Facebook](https://github.com/fernandopaezmartin/Criptografia-HTTPS/blob/main/imagenes/CA_Facebook.png)


## Certificado NO SEGURO

La mayoría de los navegadores web alertan al usuario cuando visita sitios que tienen certificados de seguridad no válidos. 


![Cert no val](https://github.com/fernandopaezmartin/Criptografia-HTTPS/blob/main/imagenes/Cert%20no%20val.png)


## Algunas diferencias entre HTTPS, SSL y TLS

HTTPS es la versión segura de HTTP: "Protocolo de transferencia de hipertexto". El protocolo HTTP es el utilizado por el navegador y servidores web para comunicarse e intercambiar información. Pero cuando el intercambio de datos se cifra con SSL / TLS, entonces se llama HTTPS.

SSL (Secure Sockets Layer) significa "Capa de sockets seguros". Es un protocolo creado por Netscape. Su versión 2 se lanzó en el año 1995 con el navegador Netscape 1.1. En 1996 se lanzó la versión SSL 3,0 que solucionaba grandes fallos de seguridad de su versión anterior. 
Antes de desaparecer Netscape, éste cedió el control del protocolo SSL a la IETF, "Internet Engineering Task Force". Este organismo, antes de finales de 1999 lanzó la versión de TLS 1.0 que en realidad era SSL 3.1. Es decir, SSL cambio su nombre a TLS "Transport Layer Security", creando confusión que sigue aún hoy para diferenciar a los protocolos. Actualmente la última versión de TLS es la 1.3, e incorpora muchas mejoras en seguridad, pero, sobre todo, en rendimiento.

## Versiones de navegadores que soportan la última versión de TLS 1.3

![tls](https://github.com/fernandopaezmartin/Criptografia-HTTPS/blob/main/imagenes/tls.png)


## Comprobación de que el navegador cliente soporta SSL

![Navegador_SSL](https://github.com/fernandopaezmartin/Criptografia-HTTPS/blob/main/imagenes/Navegador_SSL.png)



### Webgrafía (Último acceso Diciembre 2021)
https://en.wikipedia.org/wiki/HTTPS
https://www.howsmyssl.com/
https://developers.google.com/search/docs/advanced/security/https?hl=es
https://caniuse.com/?search=tls%201.3
