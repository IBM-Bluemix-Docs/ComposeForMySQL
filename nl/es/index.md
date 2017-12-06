---

copyright:
  years: 2016,2017
lastupdated: "2017-10-23"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Con un subconjunto amplio de ANSI SQL 99 y un gran conjunto de sus propias extensiones, incluido el documento de JSON, la búsqueda de texto completo y las vistas actualizables, MySQL ofrece una paleta rica para que los desarrolladores exploten sus aplicaciones. Los administradores también pueden encontrar una amplia selección de herramientas de gestión de bases de datos que pueden funcionar con MySQL. {{site.data.keyword.composeForMySQL_full}} hace que MySQL amplíe las capacidades de MySQL gestionándolo para los usuarios, ofreciendo un sistema de despliegue sencillo y de escalado automático que proporcione alta disponibilidad y redundancia, y copias de seguridad automatizadas.
{:shortdesc}

## Creación de una instancia del servicio Compose for MySQL

[Cree una instancia de {{site.data.keyword.composeForMySQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

Al crear una instancia del servicio, seleccione un nombre para el servicio y un nombre de credencial. Deje el servicio desenlazado; puede conectar una aplicación al servicio más adelante utilizando las credenciales proporcionadas cuando se proporcione el servicio.  Los distintos valores de credenciales se listan en la sección "Credenciales disponibles".

Cuando suministre la instancia de {{site.data.keyword.composeForMySQL}}, puede elegir los planes *Estándar* o *Empresa*. Con el plan *Empresa*, puede suministrar la instancia de {{site.data.keyword.composeForMySQL}} en un clúster disponible de {{site.data.keyword.composeEnterprise}}. {{site.data.keyword.composeEnterprise}} proporciona la seguridad y nivel de aislamiento necesarios para el cumplimiento de las reglas empresariales y utiliza redes dedicadas para garantizar el rendimiento de las bases de datos desplegadas. Consulte la [documentación de Compose Enterprise](../ComposeEnterprise/index.html) para ver más detalles.

## Gestión de Compose for MySQL

Puede gestionar el servicio desde el panel de control del servicio. Aquí encontrará información sobre su base de datos de {{site.data.keyword.cloud}} Compose y cómo conectarse a la misma. También puede:
- gestionar copias de seguridad
- asignar más recursos para el servicio
- cambiar la contraseña del servicio
- utilizar listas blancas para restringir el acceso a las bases de datos. 
Para obtener más información, consulte [Valores](./dashboard-settings.html).


## Conexión a Compose for MySQL

Puede conectarse a su servicio utilizando las credenciales que se crean junto con el servicio, o con las series de conexión y la línea de mandatos que se proporcionan en el separador *Visión general* del panel de control del servicio.

## Conexión de una aplicación {{site.data.keyword.cloud_notm}} a Compose for MySQL

Para conectar una aplicación {{site.data.keyword.cloud_notm}} al servicio, utilice las credenciales que se crean junto con el servicio. Encontrará información sobre cómo conectar una aplicación {{site.data.keyword.cloud_notm}} a su servicio en el apartado [Conexión de una aplicación {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Conexión a Compose for MySQL desde fuera de {{site.data.keyword.cloud_notm}}

Si desea conectar el servicio desde fuera de {{site.data.keyword.cloud_notm}}, puede utilizar las series de conexión proporcionadas o la línea de mandatos. Encontrará información sobre cómo conectar en el apartado [Conexión de una aplicación externa](./connecting-external.html).
