---

copyright:
  years: 2016,2018
lastupdated: "2017-06-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conexión de una aplicación {{site.data.keyword.cloud_notm}}

Para conectar una aplicación {{site.data.keyword.cloud}} al servicio, utilice las credenciales de servicio que se crean cuando se suministra el servicio. La app de ejemplo muestra cómo utilizar Node.js para conectar utilizando las credenciales y cómo crear una base de datos y leer y escribir en la base de datos.

## Conexión mediante la app de ejemplo 'Hello World'

La app de ejemplo [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) muestra cómo utilizar Node.js para conectar con el servicio mediante las credenciales proporcionadas. La aplicación crea, lee y escribe en una base de datos.

Descargue la app de ejemplo y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación de {{site.data.keyword.cloud_notm}}, pulse **Ver APP** para ver el contenido de la tabla *ejemplos*.

## Credenciales disponibles

Nombre de campo|Descripción
----------|-----------
`db_type`|El tipo de base de datos que ofrece el servicio, en este caso `mysql`.
`name`|El nombre del despliegue de la base de datos.
`uri_cli`|Una línea de mandatos de `mysql` que se conecta a la instancia de la base de datos.
`ca_certificate_base64`|Un certificado firmado automáticamente que se utiliza para confirmar que una aplicación se está conectando al servidor apropiado. El certificado está codificado como base64.
`deployment_id`|Un identificador interno para el servicio, tal como se ha creado en Compose.
`uri`|El URI que se utiliza al conectarse al servicio, que incluye el esquema (`mysql:`), el nombre de usuario y la contraseña del administrador, el nombre de host del servidor, el número de puerto al que se conecta y el nombre de vhost.
`uri_direct_1`|Un URI secundario que se puede utilizar al conectarse al servicio. Formateado en cuanto a `uri`.
`uri_cli_1`|Una línea de mandatos de shell de `mysql` secundaria que se conecta a la instancia de la base de datos.
{: caption="Tabla 1. Credenciales de Compose for MySQL" caption-side="top"}

**Nota:** Dos portales `haproxy` proporcionan acceso al servicio MySQL. Tanto `uri` como `uri_direct_1` pueden utilizarse para conectarse. En las aplicaciones, conmute entre `uri` y `uri_direct_1` para gestionar respuestas a fallos de conexión.
