---
title: Propiedades disponibles en el diseñador de formularios | MicrosoftDocs
ms.custom: ''
ms.date: 02/19/2019
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - PowerApps
author: Aneesmsft
ms.author: matp
manager: kvivek
tags:
  - PowerApps maker portal impact
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="properties-available-in-the-form-designer"></a>Propiedades disponibles en el diseñador de formularios

Ubicado en el panel derecho del diseñador de formularios basados en modelos, el panel de propiedades le permite rápidamente ver y actualizar las propiedades de cualquier elemento seleccionado de vista previa o de los paneles de navegación. 

> [!div class="mx-imgBorder"] 
> ![](media/form-designer-property-pane.png "Panel de propiedades del diseñador de formularios")

## <a name="form-properties"></a>Propiedades del formulario


|Nombre  |Descripción  |
|---------|---------|
|**Título**     | Escriba un nombre descriptivo para las personas. Este nombre se mostrará a las personas cuando usen el formulario. Si pueden usar formularios múltiples configurados para la entidad, usarán este nombre para diferenciar los formularios disponibles. <br /> Se requiere esta propiedad.        |
|**Descripción**     |  Escriba una descripción que explique las diferencias de este formulario respecto de otros formularios principales. Esta descripción se muestra solo en la lista de formularios de una entidad en el explorador de soluciones.        |
|**Ancho máx.**     | Establezca el ancho máximo (en píxeles) para limitar el ancho del formulario. El valor predeterminado es 1900. <br /> Se requiere esta propiedad.       |
|**Mostrar imagen**      | Mostrar la **Imagen principal** de la entidad si tiene una establecida. Este valor permitirá mostrar el campo de imagen en el encabezado de este formulario. <br /> Consulte Habilitar o deshabilitar opciones de entidad para obtener más información acerca de las opciones de la entidad.         |


## <a name="tab-properties"></a>Propiedades de las pestañas

|Área   |Nombre  |Descripción  |
|---------|---------|---------|
|**Opciones de visualización**      | **Etiqueta de pestaña**      | Etiqueta localizable de la pestaña visible para los usuarios. <br /> Se requiere esta propiedad.         |
| **Opciones de visualización**      |  **Nombre**     |  El nombre único de la pestaña que se usa al hacerle referencia en los scripts. El nombre solo puede contener caracteres alfanuméricos y de subrayado. <br />Se requiere esta propiedad.      |
| **Opciones de visualización**      |  **Expandir esta ficha de forma predeterminada**      |  El estado de la ficha puede alternar entre expandida o contraída usando scripts de formulario o cuando los usuarios seleccionan la etiqueta. Elija el estado predeterminado para la pestaña.       |
| **Opciones de visualización**      | **Ocultar pestaña**     | Cuando se selecciona, la pestaña está oculta de forma predeterminada y se puede mostrar con código.       |
| **Opciones de visualización**      | **Ocultar en teléfono**     |  Para una versión condensada de este formulario en pantallas de teléfono, las pestañas se pueden ocultar.     |
| **Formato**   | **Diseño**     |  Las pestañas pueden tener hasta tres columnas. Use las opciones para establecer el número de pestañas y qué porcentaje del ancho total deben ocupar.      |

## <a name="section-properties"></a>Propiedades de las secciones


|Área   |Nombre  |Descripción  |
|---------|---------|---------|
|**Opciones de visualización**      | **Etiqueta de sección**    | Etiqueta localizable de la sección visible para los usuarios. <br /> Se requiere esta propiedad.      |
|**Opciones de visualización**      | **Nombre**    | El nombre único de la sección que se usa al hacerle referencia en los scripts. El nombre solo puede contener caracteres alfanuméricos y de subrayado. <br /> Se requiere esta propiedad.        |
|**Opciones de visualización**      | **Ocultar etiqueta**   |  Cuando se selecciona, la etiqueta de la sección está oculta.  |
|**Opciones de visualización**      | **Bloquear sección**    | Bloquee esta sección para evitar que se elimine.      |
|**Opciones de visualización**      | **Ocultar sección**     | Cuando se selecciona, la sección está oculta de forma predeterminada y se puede mostrar con código.      |
|**Opciones de visualización**      | **Ocultar en teléfono**     |  Para una versión condensada de este formulario en pantallas de teléfono, las secciones se pueden ocultar.     |
|**Formato**     |  **Columnas**    |  Especifique hasta cuatro columnas para incluir en la sección.      |

## <a name="field-properties"></a>Propiedades de campo


|Área  |Nombre  |Descripción  |
|---------|---------|---------|
|**Opciones de visualización**     | **Etiqueta de campo**    | De forma predeterminada, la etiqueta se corresponderá con el nombre para mostrar del campo. Puede reemplazar ese nombre para el formulario proporcionando otra etiqueta aquí.       |
|**Opciones de visualización**     |  **Nombre del campo**    | Nombre del campo. Esto procede de las propiedades de campo de la entidad y es de solo lectura.     |
|**Opciones de visualización**     | **Ocultar etiqueta**     | Cuando se selecciona, la etiqueta del campo está oculta.      |
|**Opciones de visualización**     | **Campo de solo lectura**    | Cuando se selecciona, el valor del campo no es editable.      |
|**Opciones de visualización**     |  **Bloquear campo**   |  Bloquee este campo para evitar que se elimine.     |
|**Opciones de visualización**     |  **Ocultar campo**     | Cuando se selecciona, el campo está oculto de forma predeterminada y se puede mostrar con código.      |
|**Opciones de visualización**     |  **Ocultar en teléfono**    | Para una versión condensada de este formulario en pantallas de teléfono, los campos se pueden ocultar.         |
|**Opciones de visualización**     | **Ancho de campo**      |  Cuando la sección que contiene los campos tiene más de una columna puede establecer el campo para ocupar hasta el número de columnas que tiene la sección.       |


## <a name="see-also"></a>Vea también
[Información general del diseñador de formularios controlado por modelos](form-designer-overview.md)  
[Crear o editar formularios usando el diseñador de formularios](create-and-edit-forms.md)  
[Agregar, mover o eliminar campos en un formulario usando el diseñador de formularios](add-move-or-delete-fields-on-form.md)  
[Agregar, mover o eliminar secciones en un formulario usando el diseñador de formularios](add-move-or-delete-sections-on-form.md)  
[Agregar, mover o eliminar pestañas en un formulario usando el diseñador de formularios](add-move-or-delete-tabs-on-form.md)  
[Configurar propiedades de encabezado en el diseñador de formularios](form-designer-header-properties.md)  
[Use la vista de árbol del diseñador de formularios](using-tree-view-on-form.md)  
[Crear y editar campos](../common-data-service/create-edit-field-portal.md)
