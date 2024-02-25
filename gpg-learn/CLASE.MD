# GPG

**Tabla de contenidos**

<!-- vscode-markdown-toc -->

-   [Teoría](#Teora)
    -   [¿Qué significa GPG y cuál es su función principal?](#QusignificaGPGyculessufuncinprincipal)
    -   [¿Cuál es la diferencia entre criptografía simétrica y asimétrica? ¿Qué tipo de criptografía utiliza GPG?](#CulesladiferenciaentrecriptografasimtricayasimtricaQutipodecriptografautilizaGPG)
    -   [¿Cuál es el propósito de tener un par de claves en GPG? ¿Cómo se genera un par de claves?](#CuleselpropsitodetenerunpardeclavesenGPGCmosegeneraunpardeclaves)
    -   [¿Cómo se importan y exportan claves en GPG? Proporciona los comandos básicos para realizar estas operaciones.](#CmoseimportanyexportanclavesenGPGProporcionaloscomandosbsicospararealizarestasoperaciones.)
    -   [¿Cómo se el nombre de usuario?](#Cmoseelnombredeusuario)
    -   [¿Qué comandos se utilizan en GPG para cifrar y descifrar mensajes?](#QucomandosseutilizanenGPGparacifrarydescifrarmensajes)
    -   [¿Qué clave privada usa **`gpg --decrypt`**? ¿Cómo se el identificador del destinatario?](#Quclaveprivadausagpg--decryptCmoseelidentificadordeldestinatario)
    -   [¿Cuál es la diferencia entre firmar y cifrar un mensaje en GPG?](#CulesladiferenciaentrefirmarycifrarunmensajeenGPG)
    -   [¿Cómo se firma y verifica un mensaje con GPG?](#CmosefirmayverificaunmensajeconGPG)
    -   [¿Qué son las subclaves en GPG y cuál es su propósito?](#QusonlassubclavesenGPGyculessupropsito)
    -   [¿Todos los algoritmos pueden generar subclaves a partir de la principal?](#Todoslosalgoritmospuedengenerarsubclavesapartirdelaprincipal)
    -   [¿Cuál es el método por el cual se generan subclaves a partir de la principal?](#Culeselmtodoporelcualsegeneransubclavesapartirdelaprincipal)
    -   [¿Se puede desencriptar con la clave principal un archivo encriptado con una subclave? ¿Cómo es que la subclave conserva esta capacidad?](#SepuededesencriptarconlaclaveprincipalunarchivoencriptadoconunasubclaveCmoesquelasubclaveconservaestacapacidad)
    -   [¿Cómo se revoca una clave en GPG? ¿Por qué es importante hacerlo correctamente?](#CmoserevocaunaclaveenGPGPorquesimportantehacerlocorrectamente)
-   [Ejercicios](#Ejercicios)
    -   [Generación de claves](#Generacindeclaves)
    -   [Exportación e importación de claves](#Exportacineimportacindeclaves)
    -   [Cifrado y descifrado de mensajes](#Cifradoydescifradodemensajes)
    -   [Firma y verificación de mensajes](#Firmayverificacindemensajes)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='Teora'></a>Teoría

### <a name='QusignificaGPGyculessufuncinprincipal'></a>¿Qué significa GPG y cuál es su función principal?

GPG, que significa _GNU Privacy Guard_, tiene como función principal proporcionar un sistema de cifrado de datos que garantiza la privacidad y autenticidad de la comunicación electrónica. Se utiliza para cifrar, descifrar, firmar y verificar mensajes, archivos y correos electrónicos, utilizando criptografía de clave pública (asimétrica).

### <a name='CulesladiferenciaentrecriptografasimtricayasimtricaQutipodecriptografautilizaGPG'></a>¿Cuál es la diferencia entre criptografía simétrica y asimétrica? ¿Qué tipo de criptografía utiliza GPG?

La criptografía simétrica utiliza una sola clave para cifrar y descifrar datos, lo que significa que ambas partes deben compartir la misma clave de antemano. Por otro lado, la criptografía asimétrica utiliza un par de claves: una clave pública para cifrar los datos y una clave privada correspondiente para descifrarlos. GPG utiliza criptografía asimétrica para proporcionar seguridad en la comunicación.

### <a name='CuleselpropsitodetenerunpardeclavesenGPGCmosegeneraunpardeclaves'></a>¿Cuál es el propósito de tener un par de claves en GPG? ¿Cómo se genera un par de claves?

El propósito de tener un par de claves en GPG es permitir la encriptación y la firma digital de mensajes de forma segura. El par de claves consta de una clave pública, que se comparte con otros usuarios para encriptar mensajes dirigidos a ti, y una clave privada, que se mantiene en secreto y se utiliza para descifrar los mensajes encriptados y firmar mensajes. Se genera un par de claves utilizando el comando `gpg --gen-key` y siguiendo las instrucciones para especificar el tipo de clave, la longitud y otros parámetros.

### <a name='CmoseimportanyexportanclavesenGPGProporcionaloscomandosbsicospararealizarestasoperaciones.'></a>¿Cómo se importan y exportan claves en GPG? Proporciona los comandos básicos para realizar estas operaciones.

Para importar una clave en GPG, se utiliza el comando `gpg --import` seguido del nombre del archivo que contiene la clave a importar. Por ejemplo: `gpg --import clave_publica.asc`. Para exportar una clave pública, se utiliza el comando `gpg --export -a "Nombre del usuario" > clave_publica.asc`, donde "Nombre del usuario" es el identificador del usuario asociado a la clave que se quiere exportar. Esto guardará la clave pública en un archivo de texto llamado `clave_publica.asc`.

### <a name='Cmoseelnombredeusuario'></a>¿Cómo se el nombre de usuario?

Para determinar el nombre de usuario asociado a una clave en GPG, puedes utilizar el comando `gpg --list-keys`. Este comando te mostrará una lista de todas las claves públicas que tienes en tu llavero GPG, junto con su ID de clave y el nombre del usuario asociado a cada clave. Por ejemplo:

```
/Users/tuusuario/.gnupg/pubring.kbx
----------------------------------
pub  rsa2048 2022-01-01 [SC]
      A1B2C3D4E5F6G7H8  [Clave pública]
uid          [completa] Nombre de Usuario <correo@ejemplo.com>


```

En este ejemplo, "Nombre de Usuario" es el nombre asociado a la clave pública.

### <a name='QucomandosseutilizanenGPGparacifrarydescifrarmensajes'></a>¿Qué comandos se utilizan en GPG para cifrar y descifrar mensajes?

Para cifrar un mensaje en GPG, se utiliza el comando `gpg --encrypt -r destinatario mensaje.txt`, donde "destinatario" es el identificador del destinatario y "mensaje.txt" es el archivo que se desea cifrar. Para descifrar un mensaje cifrado, se utiliza el comando `gpg --decrypt mensaje_cifrado.gpg`, donde "mensaje_cifrado.gpg" es el archivo que contiene el mensaje cifrado.

### <a name='Quclaveprivadausagpg--decryptCmoseelidentificadordeldestinatario'></a>¿Qué clave privada usa **`gpg --decrypt`**? ¿Cómo se el identificador del destinatario?

Cuando se utiliza el comando `gpg --decrypt`, GPG utiliza la clave privada asociada al destinatario del mensaje cifrado para descifrarlo. En el contexto de descifrar un mensaje, GPG busca automáticamente la clave privada correspondiente en su llavero para el destinatario del mensaje.
El identificador del destinatario se refiere al identificador único asociado a la clave pública del destinatario en el llavero GPG. Este identificador puede ser el nombre de usuario, la dirección de correo electrónico u otro identificador único asignado a la clave pública durante su creación. Puedes encontrar el identificador del destinatario utilizando el comando `gpg --list-keys`.

### <a name='CulesladiferenciaentrefirmarycifrarunmensajeenGPG'></a>¿Cuál es la diferencia entre firmar y cifrar un mensaje en GPG?

Firmar un mensaje en GPG implica agregar una firma digital al mensaje utilizando la clave privada de la persona que envía el mensaje, lo que garantiza la autenticidad y la integridad del mensaje. Cifrar un mensaje, por otro lado, implica codificar el contenido del mensaje de manera que solo el destinatario designado, que posee la clave privada correspondiente, pueda descifrarlo y leerlo. Mientras que firmar un mensaje no lo hace confidencial, cifrarlo sí lo hace.

### <a name='CmosefirmayverificaunmensajeconGPG'></a>¿Cómo se firma y verifica un mensaje con GPG?

Para firmar un mensaje con GPG, la persona que envía el mensaje utiliza su clave privada para generar una firma digital del mensaje. Esto se hace con el comando `gpg --sign mensaje.txt`, donde "mensaje.txt" es el archivo del mensaje que se quiere firmar. Para verificar la firma de un mensaje, el destinatario utiliza la clave pública de la persona que envió el mensaje con el comando `gpg --verify mensaje_firmado.txt`, donde "mensaje_firmado.txt" es el archivo del mensaje firmado. Si la firma se verifica correctamente, significa que el mensaje no ha sido modificado y proviene de la persona que afirma ser.

### <a name='QusonlassubclavesenGPGyculessupropsito'></a>¿Qué son las subclaves en GPG y cuál es su propósito?

Las subclaves en GPG son claves secundarias generadas a partir de la clave principal. Su propósito principal es proporcionar una capa adicional de seguridad y flexibilidad al permitir la delegación de ciertas funciones, como la capacidad de firmar o cifrar, sin exponer la clave principal. Esto significa que si una subclave se ve comprometida, la clave principal aún permanece segura y se puede revocar la subclave comprometida sin afectar la seguridad de la clave principal. Las subclaves también permiten gestionar de manera más eficiente las funciones y los permisos asociados a una clave principal.

### <a name='Todoslosalgoritmospuedengenerarsubclavesapartirdelaprincipal'></a>¿Todos los algoritmos pueden generar subclaves a partir de la principal?

No todos los algoritmos de clave pública admiten la generación de subclaves. Los algoritmos que actualmente admiten subclaves en GPG son RSA y ElGamal.

### <a name='Culeselmtodoporelcualsegeneransubclavesapartirdelaprincipal'></a>¿Cuál es el método por el cual se generan subclaves a partir de la principal?

El método utilizado para generar subclaves a partir de la clave principal implica el uso de la clave principal como base para generar nuevas claves secundarias. Esto implica que las subclaves heredan ciertas propiedades de la clave principal, como su identificador único y su relación jerárquica con la clave principal.

### <a name='SepuededesencriptarconlaclaveprincipalunarchivoencriptadoconunasubclaveCmoesquelasubclaveconservaestacapacidad'></a>¿Se puede desencriptar con la clave principal un archivo encriptado con una subclave? ¿Cómo es que la subclave conserva esta capacidad?

Sí, se puede desencriptar un archivo encriptado con una subclave utilizando la clave principal. Esto se debe a que la clave principal posee la capacidad de descifrar cualquier archivo que haya sido cifrado con sus subclaves. La subclave conserva esta capacidad porque, aunque delega ciertas funciones, sigue siendo una derivación de la clave principal y, por lo tanto, puede ser utilizada para descifrar archivos encriptados con ella.

### <a name='CmoserevocaunaclaveenGPGPorquesimportantehacerlocorrectamente'></a>¿Cómo se revoca una clave en GPG? ¿Por qué es importante hacerlo correctamente?

Para revocar una clave en GPG, se utiliza el comando `gpg --gen-revoke [ID de la clave]`. Este comando generará un certificado de revocación que deberá ser enviado a los servidores de claves públicos y distribuido a las personas con las que se haya compartido la clave. También es importante asegurarse de que el certificado de revocación esté disponible en caso de que alguien intente verificar la validez de la clave en el futuro.
Es importante revocar una clave correctamente porque permite informar a otros usuarios y sistemas de que la clave ya no es válida y no debe ser utilizada para cifrar mensajes o verificar la autenticidad de la firma. Si no se revoca una clave comprometida o no utilizada, existe el riesgo de que alguien la utilice de manera maliciosa, lo que podría comprometer la seguridad de la comunicación.

## <a name='Ejercicios'></a>Ejercicios

### <a name='Generacindeclaves'></a>Generación de claves

Para generar un par de claves (pública y privada) en GPG, se utiliza el comando `gpg --gen-key` y se siguen las instrucciones para proporcionar la información del usuario durante el proceso de generación.

**Paso 1: Generación del par de claves**
Para generar un par de claves (pública y privada) en GPG, sigue estos pasos:

1. Abre una terminal en tu sistema operativo.
2. Ejecuta el comando `gpg --gen-key` y presiona Enter.
3. Se te pedirá que ingreses información sobre el usuario asociado a la clave, como nombre, dirección de correo electrónico y una frase de contraseña.
4. Sigue las instrucciones y proporciona la información requerida.
5. Elige el tipo de clave y la longitud deseada cuando se te solicite. Por ejemplo, puedes elegir RSA y 2048 bits.
6. Confirma la generación de la clave cuando se te solicite.

**Ejemplo:**

```
$ gpg --gen-key
gpg (GnuPG) 2.2.27; Copyright (C) 2021 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

gpg: directory '/home/user/.gnupg' created
gpg: keybox '/home/user/.gnupg/pubring.kbx' created
Please select what kind of key you want:
  (1) RSA and RSA (default)
  (2) DSA and Elgamal
  (3) DSA (sign only)
  (4) RSA (sign only)
Your selection?
```

**Nota:** Los pasos pueden variar ligeramente dependiendo de tu sistema operativo y de la versión de GPG que estés utilizando. Es importante seguir las instrucciones que se muestran en la terminal.
Una vez completado este proceso, el par de claves (pública y privada) estará generado y listo para su uso.

### <a name='Exportacineimportacindeclaves'></a>Exportación e importación de claves

La clave pública se exporta utilizando el comando `gpg --export -a "Tu Nombre" > clave_publica.asc`. Para importar una clave pública de otro usuario, se utiliza el comando `gpg --import clave_publica.asc`.

**Paso 1: Exportación de la clave pública**
Para exportar la clave pública en GPG, sigue estos pasos:

1. Abre una terminal en tu sistema operativo.
2. Ejecuta el comando `gpg --export -a "Tu Nombre" > clave_publica.asc` y presiona Enter.
3. Reemplaza `"Tu Nombre"` con el nombre asociado a la clave pública que deseas exportar.
4. Esto guardará la clave pública en un archivo de texto llamado `clave_publica.asc`.

**Ejemplo:**

```
$ gpg --export -a "John Doe" > clave_publica.asc
```

**Paso 2: Importación de la clave pública**
Para importar una clave pública en GPG, sigue estos pasos:

1. Asegúrate de tener el archivo que contiene la clave pública en un formato compatible, como ASCII armor (.asc).
2. Abre una terminal en tu sistema operativo.
3. Ejecuta el comando `gpg --import clave_publica.asc` y presiona Enter.
4. Esto importará la clave pública al llavero GPG y estará disponible para su uso.

**Ejemplo:**

```
$ gpg --import clave_publica.asc
```

Una vez completados estos pasos, la clave pública estará disponible en tu llavero GPG y podrás utilizarla para cifrar mensajes destinados al propietario de esa clave pública.

### <a name='Cifradoydescifradodemensajes'></a>Cifrado y descifrado de mensajes

Se cifra un mensaje con el comando `gpg --encrypt -r "Nombre del destinatario" mensaje.txt`. Para descifrar un mensaje cifrado, se utiliza el comando `gpg --decrypt mensaje_cifrado.gpg`.

**Paso 1: Cifrado de un mensaje**
Para cifrar un mensaje en GPG utilizando la clave pública de un destinatario, sigue estos pasos:

1. Asegúrate de tener el archivo del mensaje que deseas cifrar.
2. Abre una terminal en tu sistema operativo.
3. Ejecuta el comando `gpg --encrypt -r "Nombre del destinatario" mensaje.txt` y presiona Enter.
4. Reemplaza `"Nombre del destinatario"` con el nombre o identificador del destinatario de la clave pública que utilizarás para cifrar el mensaje.
5. Esto cifrará el mensaje y generará un archivo cifrado con extensión ".gpg".

**Ejemplo:**

```
$ gpg --encrypt -r "John Doe" mensaje.txt
```

**Paso 2: Descifrado de un mensaje cifrado**
Para descifrar un mensaje cifrado en GPG, sigue estos pasos:

1. Asegúrate de tener el archivo del mensaje cifrado que deseas descifrar.
2. Abre una terminal en tu sistema operativo.
3. Ejecuta el comando `gpg --decrypt mensaje_cifrado.gpg` y presiona Enter.
4. Esto descifrará el mensaje cifrado y mostrará el mensaje original en la terminal o lo guardará en un archivo de texto, dependiendo de cómo se haya cifrado originalmente.

**Ejemplo:**

```
$ gpg --decrypt mensaje_cifrado.gpg
```

Una vez completados estos pasos, habrás cifrado y descifrado un mensaje utilizando GPG.

### <a name='Firmayverificacindemensajes'></a>Firma y verificación de mensajes

Para firmar un mensaje, se utiliza el comando `gpg --sign mensaje.txt`. La firma de un mensaje firmado por otro usuario se verifica utilizando el comando `gpg --verify mensaje_firmado.txt`.

**Paso 1: Firma de un mensaje**
Para firmar un mensaje en GPG, sigue estos pasos:

1. Asegúrate de tener el archivo del mensaje que deseas firmar.
2. Abre una terminal en tu sistema operativo.
3. Ejecuta el comando `gpg --sign mensaje.txt` y presiona Enter.
4. Esto firmará el mensaje utilizando tu clave privada y generará una firma digital del mensaje.

**Ejemplo:**

```
$ gpg --sign mensaje.txt
```

**Paso 2: Verificación de la firma de un mensaje firmado**
Para verificar la firma de un mensaje firmado por otro usuario en GPG, sigue estos pasos:

1. Asegúrate de tener el archivo del mensaje firmado que deseas verificar.
2. Abre una terminal en tu sistema operativo.
3. Ejecuta el comando `gpg --verify mensaje_firmado.txt` y presiona Enter.
4. Esto verificará la firma digital del mensaje utilizando la clave pública del firmante y mostrará el resultado de la verificación en la terminal.

**Ejemplo:**

```
$ gpg --verify mensaje_firmado.txt
```

Una vez completados estos pasos, habrás firmado y verificado un mensaje utilizando GPG.
