---
title: Aplicar la lógica de negocios usando scripting de cliente en aplicaciones basadas en modelos que usan JavaScript | Microsoft Docs
description: Aprenda cómo los desarrolladores pueden usar JavaScript en scripts del lado cliente para aplicar lógica de negocios personalizada en aplicaciones basadas en modelos y aplicaciones Dynamics 365 for Customer Engagement
services: ''
suite: powerapps
author: KumarVivek
ms.service: powerapps
ms.topic: article
ms.date: 06/27/2019
ms.author: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="apply-business-logic-using-client-scripting-in-model-driven-apps-using-javascript"></a>Aplicar la lógica de negocios usando scripting de cliente en aplicaciones basadas en modelos que usan JavaScript

El scripting del cliente mediante JavaScript es una de las distintas formas de aplicar la lógica personalizada de procesos de negocios para mostrar los datos en un formulario en una aplicación basada en modelos.

> [!IMPORTANT]
> Todos los conceptos y API de script del cliente que se explican en esta documentación también se aplican a aplicaciones Dynamics 365 for Customer Engagement porque las aplicaciones Customer Engagement son en realidad aplicaciones basadas en modelos basadas en la plataforma Common Data Service.

Los scripts de cliente no deben ser su primera opción sin embargo para aplicar lógica de proceso de negocio personalizada en formularios de aplicación basados en modelos. Las *reglas de negocio* permiten a alguien que no conozca JavaScript y no sea programador aplicar la lógica de los procesos de negocio en un formulario. Más información: [Crear reglas de negocio para aplicar lógica](/powerapps/maker/model-driven-apps/create-business-rules-recommendations-apply-logic-form). Encontrará al diseñador de reglas de negocio dentro del área **Common Data Service** en [powerapps.com](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc). Cuando vea una entidad, busque la pestaña **Reglas de negocio**.

Sin embargo, si el requisito empresarial no se puede conseguir con una regla de negocio, descubrirá que el scripting de cliente que usa el modelo de objetos API de cliente proporciona una forma eficaz de ampliar el comportamiento de la aplicación y habilitar la automatización en el cliente.

## <a name="use-client-scripting-in-model-driven-apps"></a>Usar el scripting de cliente en aplicaciones basadas en modelos

Los formularios en las aplicaciones basadas en modelos son útiles para mostrar los datos al usuario. Un formulario en aplicaciones basadas en modelos puede contener elementos como campos, un formulario rápido o una cuadrícula. Un [evento](clientapi/events-forms-grids.md) se produce en formularios de aplicaciones basadas en modelos cuando:
- Se carga un formulario
- Se cambian los datos en un campo o un elemento dentro del formulario
- Se guardan datos en un formulario

Puede adjuntar el código de JavaScript para que "reaccione" a estos eventos de forma que se ejecute el código cuando se produzca el evento en el formulario. Adjunte el código de JavaScript (scripts) a estos eventos usando un [recurso web de script](script-jscript-web-resources.md) en aplicaciones basadas en modelos. 

Las aplicaciones basadas en modelos proporcionan un amplio conjunto de **API de cliente** para interactuar con objetos de formulario y eventos para controlar qué y cuándo se debe mostrar en un formulario.

> [!NOTE]
> Algunas API de cliente son obsoletas en la versión actual de aplicaciones basadas en modelos. Asegúrese de tener en cuenta estas API al escribir el código del lado cliente para las aplicaciones basadas en modelos. Más información: [API de cliente obsoletas](/dynamics365/get-started/whats-new/customer-engagement/important-changes-coming#some-client-apis-are-deprecated)

## <a name="get-started-here"></a>Empecemos aquí

[Eventos de formularios y cuadrículas](clientapi/events-forms-grids.md)<br/>
[Comprender el modelo de objetos de la API de cliente](clientapi/understand-clientapi-object-model.md)<br/>
[Tutorial: Escribir el primer script de cliente](clientapi/walkthrough-write-your-first-client-script.md)

## <a name="reference"></a>Referencia

[Referencia de API de cliente](clientapi/reference.md)


### <a name="related-topics"></a>Temas relacionados

[Recursos web para aplicaciones basadas en modelos](web-resources.md)<br/>
[Personalización de comandos y la cinta de opciones](customize-commands-ribbon.md)<br/>
[Guía para desarrolladores de aplicaciones Dynamics 365 for Customer Engagement](/dynamics365/customer-engagement/developer/developer-guide)

