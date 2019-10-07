---
title: ¿Qué es Common Data Service? | Microsoft Docs
description: 'Introducción a Common Data Service, entidades, lógica de servidor, seguridad, y capacidades de desarrollador.'
author: clwesene
manager: kvivek
ms.service: powerapps
ms.topic: overview
ms.component: cds
ms.date: 06/21/2019
ms.reviewer: matp
ms.author: matp
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="what-is-common-data-service"></a>¿Qué es Common Data Service?
Common Data Service, le permite almacenar y administrar de forma segura los datos que usan las aplicaciones empresariales. Los datos de Common Data Service se almacenan en un conjunto de entidades. Una *entidad* es un conjunto de registros que se usa para almacenar datos, similar a cómo una tabla almacena los datos en una base de datos. Common Data Service incluye un conjunto base de entidades estándar que cubren escenarios típicos, pero también puede crear entidades personalizadas específicas para su organización y rellenarlas con datos usando Power Query. Los creadores de aplicaciones pueden usar PowerApps para crear aplicaciones completas usando estos datos.

![Captura de pantalla que muestra información general de la plataforma de aplicaciones empresariales.](./media/data-platform-cds-intro/platform.png "Información general de la plataforma")

Para obtener información sobre cómo comprar un plan para usar Common Data Service, consulte [Información de precios](../../administrator/pricing-billing-skus.md).

## <a name="why-use-common-data-service"></a>¿Por qué usar Common Data Service?
Las entidades estándar y personalizadas de Common Data Service, proporcionan una opción de almacenamiento de datos segura y basada en la nube. Las entidades le permiten crear una definición orientada al negocio de los datos de su organización para su uso en aplicaciones. Si no está seguro de si las entidades son la mejor opción para usted, considere estas ventajas:

* **Fácil de administrar** &ndash; Los metadatos y los datos se almacenan en la nube. No tiene que preocuparse de los detalles de cómo se almacenan.
* **Fácil de proteger** &ndash; Los datos se almacenan de forma segura de forma que los usuarios solo podrán verlos si les concede acceso a ellos. La seguridad basada en roles le permite controlar el acceso a las entidades para diferentes usuarios en la organización.
* **Acceso a sus datos de Dynamics 365** &ndash; Los datos de las aplicaciones de Dynamics 365 también se almacenan en Common Data Service, lo que le permite crear rápidamente aplicaciones que aprovechan los datos de Dynamics 365 y ampliar sus aplicaciones usando PowerApps.
* **Metadatos enriquecidos** &ndash; Los tipos de datos y las relaciones se aprovechan directamente en PowerApps.
* **Lógica y validación** &ndash; Defina campos calculados, reglas de negocio, flujos de trabajo y flujos de proceso de negocio para garantizar la calidad de los datos e impulsar los procesos de negocio.
* **Herramientas de productividad** &ndash; Las entidades están disponibles en los complementos de Microsoft Excel para aumentar la productividad y garantizar la accesibilidad de los datos.

## <a name="dynamics-365-and-the-common-data-service"></a>Dynamics 365 y Common Data Service

Las aplicaciones de Dynamics 365, como Dynamics 365 for Sales, Service o Talent también usan Common Data Service para almacenar y proteger los datos que usan las aplicaciones. Esto le permite crear aplicaciones mediante PowerApps y Common Data Service directamente con sus datos de negocio clave ya usados en Dynamics 365 sin necesidad de integrarlos.

* **Crear aplicaciones con sus datos de Dynamics 365** &ndash; Cree aplicaciones rápidamente con sus datos profesionales en PowerApps o usando el SDK Pro Developer.
* **Administrar reglas y lógica de negocios reutilizables** &ndash; Las reglas y lógica de negocio ya definidas en sus entidades de Dynamics 365 se aplican a las entidades de PowerApps para garantizar la coherencia de datos independientemente del modo en que los usuarios accedan a los datos o con qué aplicación.
* **Habilidades reutilizables en Dynamics 365 y PowerApps** &ndash; Los usuarios con habilidades anteriores en PowerApps o Dynamics 365 ahora pueden aprovecharlas en la nueva plataforma de Common Data Service. La creación de entidades, formularios, gráficos, etcétera ahora son funciones comunes en sus aplicaciones.

    > [!NOTE]
    > Dynamics 365 for Finance and Operations requiere actualmente la configuración del integrador de datos para que los datos profesionales de Finance and Operations estén disponibles en Common Data Service.

## <a name="integrating-data-into-the-common-data-service"></a>Integrar datos en Common Data Service

La creación de una aplicación implica normalmente datos de más de un origen y, aunque a veces esto se puede hacer en el nivel de aplicación, también hay casos en los que al integrar estos datos en un almacén común permite una experiencia de creación de aplicaciones más sencilla y un único conjunto de lógica para mantener y operar con los datos. Common Data Service permite integrar los datos de varios orígenes en un único almacén que luego se pueden usar en PowerApps, Flow y Power BI, junto con los datos que ya estén disponibles en las aplicaciones de Dynamics 365.

* **Integración programada con otros sistemas** &ndash; Los datos que se mantienen en otra aplicación se pueden sincronizarse periódicamente con Common Data Service para poder aprovechar los datos de otras aplicaciones en PowerApps.
* **Transformar e importar datos con PowerQuery** &ndash; La transformación de datos al importar en Common Data Service puede realizarse mediante PowerQuery desde muchos orígenes de datos en línea, una herramienta común que se usa en Excel y Power BI.
* **Importación única de datos** &ndash; Se puede usar una importación y exportación simples de archivos de Excel y CSV para una importación única o poco frecuente de datos en Common Data Service.

Para obtener más información sobre cómo integrar datos en Common Data Service, consulte [Agregar datos a una entidad en Common Data Service usando Power Query](data-platform-cds-newentity-pq.md).

## <a name="interacting-with-entities"></a>Interactuar con entidades
Cuando desarrolla una aplicación, puede usar entidades estándar, entidades personalizadas o ambas. Common Data Service proporciona entidades estándar de forma predeterminada. Estas están diseñadas, de acuerdo con prácticas recomendadas, para capturar los conceptos y escenarios más comunes en una organización.

![Captura de pantalla que muestra una lista de entidades.](./media/data-platform-cds-intro/entitylist.png "Lista de entidades")

Para ver una lista completa de entidades, consulte [Referencia de entidad](https://docs.microsoft.com/powerapps/developer/common-data-service/reference/about-entity-reference).

Puede ampliar la funcionalidad de entidades estándar creando una o varias entidades personalizadas para almacenar la información que es única para su organización. Para obtener más información, consulte [Cómo crear una entidad personalizada](create-custom-entity.md).

## <a name="logic-and-validation"></a>Lógica y validación
Las entidades de Common Data Service pueden aprovechar la lógica y validación enriquecidas de servidor para garantizar la calidad de los datos y reducir código repetitivo en cada aplicación que crea y usa datos en una entidad.

* Las **reglas de negocio** validan los datos de varios campos y entidades, y proporcionan advertencias y mensajes de error, independientemente de la aplicación usada para crear los datos. Para obtener más información, consulte [Crear una regla de negocio](./data-platform-create-business-rule.md).
* Los **flujos de proceso de negocio** guían a los usuarios para asegurarse de que introducen los datos de forma coherente y de que siguen los mismos pasos cada vez. Actualmente, los flujos de proceso de negocio solo se admiten para aplicaciones controladas por modelos. Para obtener más información, consulte [Información general sobre flujos de proceso de negocio](/dynamics365/customer-engagement/customize/business-process-flows-overview).
* Los **flujos de trabajo** le permiten automatizar los procesos de negocio sin interacción del usuario. Para obtener más información, consulte [Información general de flujos de trabajo](/dynamics365/customer-engagement/customize/workflow-processes).
* La **lógica de negocios con código** admite escenarios avanzados de desarrollador para ampliar la aplicación directamente con código. Para obtener más información, consulte [Aplicar lógica de negocios con código](../../developer/common-data-service/apply-business-logic-with-code.md).

## <a name="security"></a>Seguridad
Common Data Service tiene un rico modelo de seguridad que protege la integridad de los datos y privacidad de los usuarios al tiempo que promueve una colaboración y un acceso a los datos eficaces. Puede combinar unidades de negocio, la seguridad basada en roles, la seguridad de registros y la seguridad basada en campos para definir el acceso generala la información que los usuarios tienen en un entorno de Common Data Service. Más información: [Seguridad en Common Data Service](/power-platform/admin/wp-security) 

## <a name="developer-capabilities"></a>Capacidades de desarrollador
Además de las características disponibles mediante el portal de [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc), Common Data Service también incluye características para que los desarrolladores puedan acceder de forma programática a los metadatos y datos para crear entidades y lógica de negocios, así como para interactuar con datos. Para obtener más información, consulte [Información general para desarrolladores de Common Data Service](../../developer/common-data-service/overview.md)

## <a name="next-steps"></a>Pasos siguientes
Para empezar a utilizar Common Data Service:
- [Crear una aplicación de lienzo mediante una base de datos Common Data Service](../canvas-apps/data-platform-create-app-scratch.md).
- [Crear una entidad personalizada](create-custom-entity.md) y, a continuación, [crear una aplicación de lienzo que use la entidad](../canvas-apps/data-platform-create-app.md).
- [Crear una aplicación basada en modelos](/powerapps/maker/model-driven-apps/build-first-model-driven-app) con Common Data Service.
- [Usar Power Query](./data-platform-cds-newentity-pq.md) para conectarse a un origen de datos en línea o local e importar los datos directamente en Common Data Service.

## <a name="privacy-notice"></a>Aviso de privacidad
Con el modelo común de datos de Microsoft PowerApps, Microsoft recopila y almacena la entidad personalizada y los nombres de campo en nuestros sistemas de diagnóstico. Usamos esta información para mejorar el modelo común de datos para los clientes. La entidad y los nombres de campo que los creadores de la aplicación crean nos ayudan a comprender los escenarios que son comunes en la comunidad de Microsoft PowerApps y a determinar los huecos en la cobertura de las entidades estándar del servicio, como los esquemas relacionados con las organizaciones. Microsoft no accede a los datos de las tablas de base de datos asociadas a estas entidades ni los usa o replica fuera de la región en la que se proporciona la base de datos. No obstante, tenga en cuenta que la entidad personalizada y los nombres de campo se pueden replicar en las regiones y que se eliminan de acuerdo con nuestras directivas de retención de datos. Microsoft se compromete a proteger su privacidad, como se describe con más detalle en nuestro [Centro de confianza](https://www.microsoft.com/trustcenter/Privacy/default.aspx).
