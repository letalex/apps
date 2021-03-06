---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-25"

---

# ¿Qué hace que una app sea buena?
{: #best-practice}

Cree su app en {{site.data.keyword.Bluemix_notm}} para aprovechar todas las posibilidades que ofrece la nube. Estas mejores prácticas pueden ayudarle a asegurarse de que sus apps estén preparadas para la nube.
{:shortdesc}

## Cree su app de forma que sea independiente de la topología

En un entorno que no sea en la nube, su app podría utilizar una topología de despliegue concreta. No obstante, su topología de app podría cambiar en apps en la nube porque las apps y servicios listos para la nube permiten cambios de escalabilidad inmediata. Los cambios de escalabilidad incluyen escalado dinámico y cambio manual del tamaño del número de instancias de una app.

Construya su app de forma que sea lo más genérica e independiente posible de estado, para evitar que se vea afectada por cambios de escalabilidad.

## Presuponga que el sistema de archivos local no es permanente

No se base en archivos que se graben en el sistema de archivos, porque una instancia de app en la nube se puede mover, suprimir o duplicar. Si una app utiliza el sistema de archivos local como memoria caché de información usada con frecuencia incluyendo los registros de app, la información se pierde cuando se cierra la instancia y se reinicia en una ubicación distinta o en otra MV.

En lugar del sistema de archivos local, puede almacenar información en un servicio, como una base de datos SQL o NoSQL. En un entorno de nube dinámico, también es fundamental tener sus registros disponibles en un servicio que sobreviva a la instancia de la app desde la que se generan los registros.

## Almacene el estado de sesión fuera de la app

El estado de su sistema lo definen sus bases de datos y almacenamientos compartidos, y no cada instancia individual de app en ejecución. El uso de estados de cualquier tipo limita la escalabilidad de su app. Intente minimizar el impacto del estado de sesión almacenándolo en una ubicación centralizada en el servidor.

Si no puede eliminar el estado de sesión por completo, colóquelo en un almacén de alta disponibilidad externo a su servidor de apps. Los almacenes pueden ser IBM WebSphere eXtreme Scale, Redis o Memcached, o bien una base de datos externa.

## Utilice un registro de servicio externo para resolver puntos finales de servicio

No presuponga que los servicios que utiliza su app están en nombres de host o direcciones IP concretas. Los servicios podrían cambiar de lugar o volverse a generar en su entorno de nube y los nombres de host y las direcciones IP también podrían cambiar.

La extracción de las dependencias específicas del entorno a un conjunto de archivos de propiedades mejora la situación, pero sigue sin ser adecuado. Lo recomendable es utilizar un registro de servicio externo para resolver puntos finales de servicio, o delegar la función de direccionamiento completa en un bus de servicio o un equilibrador de carga con un nombre virtual.

## Cree la app mediante una arquitectura de varias regiones
{: #multiregion}

Ejecute varias instancias para evitar el tiempo de inactividad en una sola región, sin embargo, para ofrecer una aplicación más sólida tenga en cuenta una arquitectura de varias regiones.

## Asegúrese de supervisar sus apps
{: #monitoring}

{{site.data.keyword.Bluemix_notm}} facilita la supervisión de su aplicación con servicios como, por ejemplo, [New Relic ![Icono de enlace externo](../icons/launch-glyph.svg)](http://newrelic.com/){: new_window}. Consulte [supervisión y registro](../monitor_log/logging.html#logging) para obtener más información.

## Saque partido a las opciones de soporte
{: #support}

El plan de precios de pago de {{site.data.keyword.Bluemix_notm}} ofrece un número de tipos de cuenta distintos con soporte de pago opcional. Sin importar el tipo de cuenta, si piensa en llevar una aplicación a producción en {{site.data.keyword.Bluemix_notm}}, considere la posibilidad de inscribirse en esta opción.

Con o sin soporte de pago, puede obtener ayuda como se describe en [soporte](../get-support/howtogetsupport.html), que ofrece seguro contra problemas imprevistos.

## Evite API de infraestructura en su app

Si se basa en una API de infraestructura específica en su app, al cambiar la infraestructura podría haber problemas, ya que la API de la infraestructura puede hacer referencia a distintas capas en su pila de software.

En su lugar, puede basarse en código abierto existente o productos comerciales, y dejar las soluciones PaaS en la capa PaaS para mantenerlas fuera de su código de app.

## Utilice protocolos estándar

No utilice protocolos complejos que necesiten de configuración adicional para su capacidad de resistencia.

Las apps basadas en protocolos estándar son más resistentes con los elementos de configuración que están delegados a la plataforma. Los protocolos estándar principales son HTTP, SSL, base de datos estándar, consultas y conexiones de servicio web.

## Utilice bibliotecas de compatibilidad en lugar de funciones de específicas de SO

Si ya ha utilizado características específicas del sistema operativo, puede solucionarlo mediante el uso de bibliotecas de compatibilidad, como Cygwin y Mono. Cygwin es una biblioteca de compatibilidad que proporciona un conjunto de herramientas Linux en un entorno Windows. Mono es una biblioteca de compatibilidad que proporciona capacidades de Windows .NET en Linux.

Evite las dependencias de un sistema operativo específico; en su lugar, utilice servicios proporcionados por la infraestructura middleware o proveedores de servicios.

## Cree scripts del proceso de instalación

Su app se podría instalar con frecuencia a demanda en el entorno de nube dinámico. El proceso de instalación debe ser mediante script y fiable, y los datos de configuración se deben externalizar de los scripts.

Capture la instalación de la app como un conjunto uniforme de scripts independientes del sistema operativo. Mantenga la instalación de su app en un tamaño reducido y portátil para adaptarse a distintas técnicas de automatización. Además, minimice las dependencias necesarias para la instalación de apps.

Para obtener más información sobre apps listas para la nube, consulte [The 12-factor app ![icono de enlace externo](../icons/launch-glyph.svg)](http://12factor.net/){: new_window}.


