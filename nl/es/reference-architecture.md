---
copyright:
  years: 2016,2018
lastupdated: "2018-06-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Arquitectura 
{: #architecture}

## Réplica

Un despliegue de {{site.data.keyword.composeForMySQL_full}} empieza con tres nodos de datos en un clúster, distribuidos entre las zonas de disponibilidad de la región. Los datos se replican en los tres nodos; si un miembro de datos del clúster pasa a no ser accesible, el clúster continúa operando con normalidad. El clúster está configurado de modo que si falla el miembro del líder en el clúster, el esclavo actual se promociona a un líder en un plazo de 60 segundos del líder que deja de responder. 

## Cifrado de disco

Todos los servicios de {{site.data.keyword.composeForMySQL}} tienen cifrado en reposo. Los datos residen en servidores que tienen el cifrado de nivel de volumen habilitado. 

Puesto que {{site.data.keyword.composeForMySQL}} es un servicio gestionado, es posible que los operadores de {{site.data.keyword.cloud}} Compose vean los datos. Además del cifrado de disco, le recomendamos que cifre la información personal antes de almacenarla en la base de datos o que utilice extensiones o funciones para habilitar el cifrado en la propia base de datos. Si bien estos métodos pueden afectar a la usabilidad o al rendimiento, es una buena práctica asegurarse de que la información personal esté protegida con cifrado.

## Escalado automático

Los recursos se escalan automáticamente en función del uso de almacenamiento en disco total de las bases de datos MySQL. El uso de memoria se basa en una proporción de almacenamiento suministrado en una proporción de 1:10. Estos recursos se empaquetan como unidades.

El escalado automático está diseñado para responder a las tendencias a corto y medio plazo de la base de datos. Cada hora, el servicio está marcado y si se está quedando corto en el espacio de disco, se asignan más unidades al despliegue.

El escalado automático no reduce los despliegues en los que el uso de disco/memoria se ha reducido. Los recursos suministrados a las bases de datos permanecerán para sus necesidades futuras, o hasta que reduzca el despliegue manualmente.
{: .tip}
