# Patrones Arquitecturales

# S3 Tutorial
## 1. Desplegar un sitio estático usando S3

Nos dirigimos a la consola de AWS como se ilustra en la siguinete imagen:

![Cosola de administración](/images/1.png)

En la consola buscamos el servicio de S3, entramos a S3 y no aparecera la siguente pantalla.

![Cosola de administración](/images/2.png)

Damos click en el boton azul de create bucket que nos aparece en la pantalla, una vez le demos al boton nos aparecera una ventana emergente como la siguiente.


En esta ventana escojemos el nombre que tendra el bucket y su regino, para este caso el nombre del bucket es "patronesarquitecturales" y su region US East(N. Virginia)


**Nota:** el nombre del bucket tiene que ser unico con todos los buckets que existan en AWS.
Una vez llenado estos datos le damos en el boton de next.


![Cosola de administración](/images/3.png)

Esta ventana es para realizar la configuracion del bucket, le damos en el boton de Next.

![Cosola de administración](/images/4.png)

En este apartado podemos configurar el accesos externo hacia el bucket, por el momento no tocamos nada y le damos al boton Next.

![Cosola de administración](/images/5.png)

En este apartado revisaremos que toda las opciones esten como las modificamos, una vez confirmemos que todo este bien le damos en el boton "Create bucket".

![Cosola de administración](/images/6.png)

Una vez le dimos en **"Create bucket"**, cerramos la ventana y tendremos nuestro bucket creado como se muestra en la siguiente imagen.

![Cosola de administración](/images/7.png)

Entramos al bucket y aparecela la siguiente ventana.

![Cosola de administración](/images/8.png)

Dentro del bucket le damos el boton de Upload para montar nuestro sitio estatico con todo sus recursos.

![Cosola de administración](/images/9.png)

Arrastramos todo los archivos del sitio, en este caso el index.html y la carpeta de las imagenes donde se encuentran todas las imagenes de este sitio.


Le damos en el boton Upload para cargar los archivos.

![Cosola de administración](/images/10.png)

Cuando termine de montar todos los archivos al bucket, veremos la siguente ventana.

![Cosola de administración](/images/17.png)

Nos vamos a dirigir a la pestaña que dice "Properties" para realizar la configuracion del hosting.

![Cosola de administración](/images/16.png)

Entre las opciones que nos da esta pestaña, vamos a usar el que dice "Static website hosting" como se muestra en la siguiente imagen.


Cuando le demos click se despliegara un menu como la imagen de la derecha.


En este formulario escojemos la opcion "Use this bucket to host a website" y en el campo de Index document pondremos el nombre de nuestro archivo html, para nuestro caso es index.html

![Cosola de administración](/images/12.png)

![Cosola de administración](/images/11.png)

Ahora nos dirigimos a la pestaña de Permissions, donde encontraremos 4 sub-ventanas, en la primera encontramos la siguiente ventana


En esta pestraña de "Block Public Access" la damos al boton de editar y desmarcamos todas las opciones, guardamos y nos tiene que quedar de la suiguiente forma.

![Cosola de administración](/images/18.png)

Luego nos vamos a la sub-pestaña de "Bucket Policy"


Tendremos que generar una politica de lectura para que nos permita entrar al sitio web.

![Cosola de administración](/images/19.png)

**Nota:** estas son ayudas para generar las politicas necesarias.
1. [Generador de politicas de AWS](https://awspolicygen.s3.amazonaws.com/policygen.html)
2. [Documentacion sobre las politicas](https://docs.aws.amazon.com/AmazonS3/latest/dev/example-bucket-policies.html)

Cuando le damos en el enlace de "Generador de politicas de AWS" que se encuentra en la parte de arriba nos sale la siguinete ventana.


En esta ventana selecionamos S3 Bucket Policy como tipo de politica.


En el apartado de primcipal ponemos **"*"** para que permita todos los archivos.


En el apartado Actions buscamos el que dice **"GetObject"**.


Y en el apartado Amazon Resource Name (ARN) ponemos el Arn que aparece en la consola de AWS, justo al lado **"Bucket policy editor"**.


En este caso es **"arn:aws:s3:::patronesarquitecturales"** y le agregamos al final **"/*"**.


Le damos al boton de "Add Statement".

![Cosola de administración](/images/15.png)

se generara una politica en la parte de abajo, al final de la pagina hay un boton que dice "Generate Policy"


Cuando le damos nos sale la siguiente ventana.

![Cosola de administración](/images/20.png)

```
{
	"Id": "Policy1569790985535",
	"Version": "2012-10-17",
	"Statement": [
		{
		"Sid": "Stmt1569790984088",
		"Action": [
			"s3:GetObject"
		],
		"Effect": "Allow",
		"Resource": "arn:aws:s3:::patronesarquitecturales/*",
		"Principal": "*"
		}
	]
}
```

![Cosola de administración](/images/14.png)

Para terminar nos vamos a la pestaña de Cors configuracion


Copiamos el siguiente codigo y lo pegamos en la recuadro de texto.

```
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
	<CORSRule>
		<AllowedOrigin>*</AllowedOrigin>
		<AllowedMethod>GET</AllowedMethod>
		<MaxAgeSeconds>3000</MaxAgeSeconds>
		<AllowedHeader>*</AllowedHeader>
	</CORSRule>
</CORSConfiguration>
```
Nos tiene que quedar de la siguente forma


Una vez tengamos eso realizado guardamos

![Cosola de administración](/images/13.png)

**Nota:** para mayor informacion de la configuracion de cors entra al enlace que esta aqui abajo.
 - [Documentacion sobre los Cors](https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html)



Hemos terminado la configuracion del bucket para probar nuestro sitio web escribimos la siguinete ruta.

```
https://<Nombre del bucket>.s3.amazonaws.com/<index>.html
```

Para nuestro caso la direccion ULR es la siguiente:
[https://patronesarquitecturales.s3.amazonaws.com/index.html](https://patronesarquitecturales.s3.amazonaws.com/index.html)

# EC2
## 2. Desplegar un formulario dinámico usando EC2

1. Acceda a la consola de administración de AWS

Buscamos el servicio de EC2.

![Cosola de administración](/images/1.png)

2. Cree una maquina virtual linux siguiendo los pasos en:

Despues de darle click en EC2 de la consola de AWS veremos esta pantalla.

![Cosola de EC2](/images/EC2.png)

Una ves en esta pantalla nos desplazamos para la parte inferior y veremos la siguiente pantalla.

![Cosola de EC2](/images/EC2Create.png)

realizamos Click en la opcion de Launch instance.

Una ves realizado el click nos redirigira a la siguiente ventana.

![Cosola de EC2](/images/SelectInstace.png)

Seleccionamos la segunda opcion. (Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type)

![Cosola de EC2](/images/SelectType.png)

Dejamos seleccionada la opcion por defecto y hacemos click en el boton de "**Review and Launch**".

![Seleccion de Maquina](/images/ReviewInstance.png)

En esta ventana solo nos muestra un pequeño resumen de los elementos de nuestra instancia; Le daremos en el boton **Launch**.

![Seleccion de tipo de instancia](/images/key.png)

Se nos abrira la ventana anterior, en esta ventana escojemos en el primer campo la opcion **"Create a new key pair"**.
En la segundo campo ponemos el nombre de como queremos que se llame la llave.

Se debe ver de la siguiente forma: 

![Seleccion de Maquina](/images/key2.png)

Le damos en el boton de **"Download Key Pair"**.

Una ves descargada la llave de acceso para la maquina realizamos click en el boton de **Launch**.

![Resumen del recurso a crear](/images/Launch.png)

Nos aparecera la anterior ventana, mostrando que se a creado exitosamente la maquina virtual.

Bajamos hasta el final de la pagina y presionamos el boton **View Launch**
![Creacion de credenciales ssh](/images/Launch2.png)

Nos redirigira a la siguinete pagina donde veremos las instancias creadas. En este caso solo tendremos la que creamos.

![Cosola de administración instancias EC2](/images/InstanceLaunch.png)

Para mas referencias visite el siguiente enlace: 
- [Aws getting started tutorial](https://aws.amazon.com/es/getting-started/tutorials/launch-a-virtual-machine/)

# 3. Nos conectamos a la maquina con el siguiente commando:

Nos dirigimos a la parte superior al boton que dice **Connect**, esto nos desplegara la siguiente ventana:

![Cliente ssh](/images/connect.png)

En esta ventana nos aparecen diferentes metodos de conexion con nuestra instancia EC2.

nos connectaremos por SSH.

Para esto nos dirigiremos por consola a la ubicacion de archivo **.PEM** anteriormente descargado y realizaremos el paso 3 que nos indica la ventana.

```
> chmod 400 key.pem
```
Despues de esto realizaremos el paso 4.

En este caso a mi me muesta el siguiente comando que usare para realizar la conexion:

```
> ssh -i "key.pem" ec2-user@ec2-3-83-11-201.compute-1.amazonaws.com
```

La siguiente imagen ilustra la ejecucion de los dos pasos anteriores, **Note** que cuando ejecutamos el comando ssh nos pregunta que si deseamos continuar con la conexion, esto solo aparecera la primera ves que realicemos el proceso.

![Ejecucion el comando](/images/ssh.png)

Una ves dentro de la maquina terminaremos la conexion.
**Nota:** Salimos del ssh usando "exit".

# 4. Conexion Spring Boot + MongoDB.

Utilizando un proyecto maven con el plugin de spring boot para el manejo mongodb.

El proyecto utilizado esta a [aqui](https://github.com/Arep-Nico/Patrones-Arquitecturales)

Formulario web [aqui](https://github.com/Arep-Nico/arep-app)

Ingresaremos al cluster de MongoDB [aqui](https://account.mongodb.com/account/login?signedOut=true)

Con una cuenta previamente creada ingresaremos.

![Login Mongo](/images/loginMongo.png)

Una vez autenticados nos aparecera la siguiente ventana:

![Project](/images/projects.png)

Realizaremos click en el boton **New Project**, a continuacion nos redirigira a la siguiente ventana, donde pondremos el nombre de nuestro projecto, en mi caso el ponder **Arep-Project**

![New Project](/images/newProject.png)

Realizaremos click en el boton **New**, nos redirigira a la siguiente ventana.

![Create Project](/images/CreateProject.png)

Realizaremos click en **Create Project**, al finalizar la creacion del proyecto nos mandara a la siguiente pantall:

![Cluster](/images/cluster.png)

Para crear un cluster daremos click en el boton **Build a Cluster**.

![Cluster plan](/images/clusterBuild.png)

En la anterior imagen nos muestra los diferentes planes que ofrece Mongo, en mi caso seleccionare le plan **Shared Cluster**.

En la siguiente ventana nos aparecen las diferentes opciones para desplegar el cluster que se generara.

![Select deploy](/images/clusterBuildAws.png)

Seleccionaremos Aws y en la region de Virginia US, de damos click e **Create Cluster**

![Deploy](/images/deployCluster.png)

Una vez finalizado el despliegue de las 3 instancias del cluster, se nos habilitara el boton de **CONNECT**, al realizar click sobre el nos aparecera la siguiente ventana.

![Connect](/images/connectMongo.png)

para el primer paso de damos en el boton de **Add Your Current IP Address** y en el segundo punto escribiremos el nombre de usuario y la contraseña del usuario que crearemos para acceder a la coleccion de mongo.

Nos debe quedar de la siguiente manera:

![Connect](/images/connectMongo2.png)

Daremos click en el boton de **Add IP Address** y en de **Create MongoDB User**, se nos mostrara lo siguiente:

![Connect](/images/connectMongo3.png)

Realizamos click en **Choose a connect method**, nos saldra lo siguiente:

![Method](/images/method.png)

Seleccionamos **Connect your application**, y nos mostrara lo siguiente:

![Method](/images/method2.png)

En driver buscamos **Java** y en **Version** seleccionamos la mas reciente.

En el paso dos nos aparecera la linea para la coneccion a mongo, la copiaremos y la pegaremos en el archivo **application.properties** de nuestro proyecto maven.

Nos debe quedar de la siguiente forma:

![Configure](/images/config.png)

**Nota**: debemos cambiar el texto \<password> por nuestra contraseña y adicional mente podemos cambiar **test** por el nombre de la Base de Datos que querramos usar.

Ya podemos ejecutar el proyecto y ver en la terminal como realiza la conexion a mongo.

Para poder ejecutar nuestro proyecto desde otra maquina y que el cluster de mongo nos permita la conexion deberemos agregar la ip de la maquina desde la cual nos conectaremos.

En este caso nos iremos a la consola de Aws y en la intancia en la parte inferior nos aparecera la ip publica que tiene la maquina.

![Ip EC2](/images/ip.png)

En la consola de Mongo nos dirigimos al apartado de Network Access que aparece en el menu de la parte izquierda.

![Ip EC2](/images/ipMongo.png)

Una vez dentro nos aparecera al ip que agregamos anterior mente.

Le damos en el boton de **Add Ip Address** y nos desplegara la siguiente ventana:

![Ip EC2](/images/appIp.png)

En esta ventana escribiremos la ip de la instancia EC2.

![Ip EC2](/images/ipAdd.png)

Nos debe quedar como ilustra la anterior imagen.

# 5. Usamos sftp para tranferir el archivo .jar de nuestro proyecto.

## Methodo 1
Para realizar la transderencia de archivos a la maquina EC2 usaremos el comando **sftp** de la terminal.

En este caso a mi se muesta el siguiente comando que usare para realizar la conexion por **sftp**:

```
> sftp -i "key.pem" ec2-user@ec2-3-83-11-201.compute-1.amazonaws.com
```

Buscamos de manera local el archivo para tranferirlo y con el siguiente comando lo pasamos a la maquina virtual.

**Nota**: para desplazarce por los directorios locales se utiliza lcd y para listar los directorios es lls.

```
put <nombre del archivo>.jar
```

**Nota**: para esto previamente debimos empaquetar el proyecto.

En la siguiente imagen se ilustra la ejecucion de los pasos anteriores.

![Cosola de salida](/images/put.png)

## Metodo 2

Si deseamos descargar el proyecto desde un repositorio git tendremos que instalar git, para eso ejecuta el siguiente comando:

```
> sudo yum install git -y
```

Si deseas ejecurata y/o empaquetar un proyecto maven tendras que instalar maven en la instancia para eso sigue el siguiente tutorial: [aqui](https://docs.aws.amazon.com/neptune/latest/userguide/iam-auth-connect-prerq.html)

# 6. Arrancamos el servicion del archivo jar

Para configurar java 1.8 utiliza estos comandos:

```
sudo yum install java-1.8.0 -y
sudo yum install java-1.8.0-openjdk-devel -y
sudo yum remove java-1.7.0-openjdk -y
```

Este es el comando que tenemos que ejecutar en la terminal:

```
java -jar <nombre del archivo>.jar
```

![Cosola de salida](/images/spring.png)

## 7. Configurar un VPC para gestionar la seguridad y los permisos de acceso a sus servidores.

En las opciones de la parte inferior nos muestra varios datos de la instancia, en que nos importa por el momento es el que dice **Security groups**.

![Cosola EC2](/images/EC22.png)

Damos click en el enlace que dice **launch-wizard-1**

![Secure Group](/images/secure.png)

En la ventana anterior realizamos click en el grupo, nos redirigira a la siguiente pagina:

![Secure Group](/images/secure2.png)

Le damos en el boton de **edit inbound rules**, y nos aparecera la siguiente ventana:

![Inbound](/images/inbound.png)

Le damos en el boton de **add rule** y escojemos la opcion de Custom TCP, en el port range ponemos el puerto por el que esta corriendo nuestra aplicacion.

Ejemplo: 

> ![Ibound rules](/images/inbound2.png)

Guardamos los cambios.

![Cosola de salida](/images/save.png)

A continucion visitamos nuestra pagina para comprobar que la regla fue correctamente configurada.

Para esto tenemos dos formas de ingresar, la primera es por el DNS que provee AWS, la segunda forma es por la ip publica que brinda Aws.

```
> ec2-3-83-11-201.compute-1.amazonaws.com:8080
> 3.83.11.201:8080
```

![Cosola de salida](/images/webDns.png)


![Cosola de salida](/images/webIp.png)