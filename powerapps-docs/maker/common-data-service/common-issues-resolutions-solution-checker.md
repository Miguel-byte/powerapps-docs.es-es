---
title: Problemas y soluciones comunes para el Comprobador de soluciones | Microsoft Docs
description: ' Una lista de problemas y soluciones comunes en Comprobador de soluciones'
keywords: ''
ms.date: 02/11/2019
ms.service: powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: caa4e3f2-9700-49b8-87ed-8a68e8878b02
author: jowells1
ms.author: jowells
manager: austinj
ms.reviewer: null
robots: 'noindex,nofollow'
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="common-issues-and-resolutions-for-solution-checker"></a>Problemas y soluciones comunes para el Comprobador de soluciones

En este artículo se enumeran algunos problemas comunes que puede encontrar mientras usa el Comprobador de soluciones. En los casos que correspondan, se proporcionan las soluciones alternativas.

## <a name="youre-unable-to-use-solution-checker-to-run-analysis-or-download-results"></a>No puede usar el comprobador de soluciones para ejecutar análisis o descargar resultados

Poco después de enviar una solicitud al comprobador de soluciones para ejecutar un análisis o descargar resultados la operación no se completa y se muestra un mensaje de error como:

> *“No pudimos ejecutar la comprobación en la solución **[Nombre de la solución]**. Ejecútela de nuevo."*

Siempre que sea posible, el comprobador de soluciones intenta devolver un mensaje de error específico con un vínculo a los detalles sobre la causa potencial y pasos de resolución. Seleccione **'Más información'** para los detalles.

![Barra de mensajes de error](media/solution-checker-missing-roles-error.png)

Los errores que se producen durante el procesamiento en segundo plano de análisis fallarán con el estado **“No se pudo completar”** y devuelven un mensaje de error en el portal de PowerApps además de enviar una notificación por correo electrónico al solicitante. 

![Estado de error](media/solution-checker-exception-status.png)

La selección de notificación del portal vinculará a esta página de problemas comunes para la solución de problemas adicionales. Si uno de los problemas comunes proporcionados no resuelve el problema, también se devuelve un número de referencia. Proporcione este número de referencia al soporte técnico de Microsoft para su posterior investigación.

![Notificación de error](media/solution-checker-failure-notification.png)

## <a name="solution-checker-fails-due-to-unsupported-version-of-powerapps-checker"></a>El comprobador de soluciones falla debido a una versión no compatible del Comprobador de PowerApps

El Comprobador de soluciones es una característica habilitada por la aplicación Comprobador de PowerApps.  Si ha instalado una versión de la aplicación Comprobador de PowerApps anterior a **1.0.0.47**, las ejecuciones del Comprobador de soluciones pueden no completarse correctamente. Debe actualizar la versión del Comprobador de PowerApps desde [!INCLUDE [pn-dyn-365-admin-center](../../includes/pn-dyn-365-admin-center.md)]. 

Sin embargo, si tiene una versión del Comprobador de PowerApps anterior a **1.0.0.45** instalada, se recomienda eliminar la solución y volver a instalarla. Debido a los cambios recientes de esquema, la actualización del Comprobador de PowerApps de versiones anteriores a **1.0.0.45** puede provocar errores.

Si desea conservar los resultados anteriores del Comprobador de la solución, exporte los resultados de una ejecución anterior o exporte todos los datos del Comprobador de soluciones con [Exportar datos a Excel](../../user/export-data-excel.md) para exportar los datos de las siguientes entidades:

- Componente de análisis
- Trabajo de análisis
- Resultado de análisis
- Detalle de resultado de análisis

### <a name="how-to-uninstall-powerapps-checker"></a>Cómo desinstalar el Comprobador de PowerApps

Para desinstalar la solución Comprobador de PowerApps:

1. Como administrador del sistema o como personalizador del sistema, abra el portal de PowerApps en https://web.powerapps.com/environments.
2. Seleccione **Solución**.
3. Seleccione **Comprobador de PowerApps** y, a continuación, en la barra de herramientas de soluciones seleccione **Eliminar**.

### <a name="how-to-install-powerapps-checker"></a>Cómo instalar el Comprobador de PowerApps

Para instalar el Comprobador de PowerApps en el entorno Common Data Service:

1. Como administrador del sistema o como personalizador del sistema, abra el portal de PowerApps en https://web.powerapps.com/environments.
2. Seleccione **Solución**.
3. En la barra de herramientas de soluciones, seleccione **Comprobador de soluciones** y, a continuación, seleccione **Instalar**.

## <a name="solution-checker-cant-access-organizations-in-administration-mode"></a>El Comprobador de soluciones no puede tener acceso a las organizaciones en modo de administración

Las organizaciones que se han situado en [Modo de administración](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/admin/manage-sandbox-instances#administration-mode) limitan a propósito el acceso solo a los usuarios con roles de Administrador del sistema y Personalizador del sistema. Puesto que la identidad de aplicación Comprobador de PowerApps no tiene ningún de estos roles asignados de forma predeterminada, no tiene acceso a las organizaciones que trabajan en este modo.

Para usar el Comprobador de soluciones en esta organización, el modo de administración debe deshabilitarse.

### <a name="how-to-disable-administration-mode"></a>Cómo deshabilitar el modo de administración

Para deshabilitar el modo de administración en una instancia de organización:

1. Abra al selector de instancias de aplicaciones de Dynamics 365 for Customer Engagement: https://port.crm.dynamics.com/G/Instances/InstancePicker.aspx.
2. Seleccione la instancia de la organización que tiene problemas de ejecución del Comprobador de soluciones.
3. Seleccione **ADMINISTRACIÓN**.<br/>
![Instancia Admin](media/solution-checker-instance-admin.png)

4. Desactive **Habilitar modo de administración** y a continuación, seleccione **Guardar**.<br/>
![Deshabilitar el modo de administración](media/solution-checker-instance-disable-admin-mode.png)

5. Volver a ejecutar el Comprobador de soluciones

## <a name="solution-checker-fails-due-to-missing-security-roles"></a>El Comprobador de soluciones falla porque faltan roles de seguridad

El usuario de la aplicación para el Comprobador de soluciones requiere dos roles de seguridad asignados para proporcionar los privilegios necesarios para comunicarse con la organización de Common Data Service. Si uno de estos roles no se asigna al usuario **'Comprobador de PowerApps'**, se producirá error al intentar ejecutar análisis, descargar resultados y ejecutar cancelación. Esto ocurre con más frecuencia cuando los clientes tienen instalada automatización que quita roles de seguridad de usuarios inesperados. Los roles de seguridad siguientes contienen permisos mínimos necesarios:

- Exportar personalizaciones
- Comprobador de soluciones

### <a name="how-to-assign-missing-security-roles"></a>Cómo asignar roles de seguridad que faltan

Para asignar roles de seguridad que faltan al usuario del Comprobador de PowerApps:

1. Abra la organización de Common Data Service y vaya a **Configuración** > **Seguridad** > **Usuarios**.
2. Seleccione el usuario del **'Comprobador de PowerApps'** de la lista de usuarios.
3. Seleccione **ADMINISTRAR ROLES** en la barra de comandos.
4. Seleccione las casillas de rol **“Exportar personalizaciones** y **“Comprobador de soluciones”** y, a continuación seleccione **Aceptar**.<br/>
![Roles de seguridad obligatorios](media/solution-checker-required-roles.png)

5. Volver a ejecutar el Comprobador de soluciones

## <a name="solution-checker-fails-due-to-restricted-access-mode"></a>El comprobador de soluciones falla debido al modo de acceso restringido

El usuario de la aplicación para el Comprobador de soluciones requiere un modo de acceso de **'No interactivo'** o **'Solo lectura'** para comunicarse con la organización de Common Data Service. Si ha cambiado el modo de acceso a otro valor como **“Administrativo”**, fallarán los intentos de ejecutar análisis, descargar resultados y ejecutar cancelación.

Para resolver este problema, debe actualizar el usuario de la aplicación **'Comprobador de PowerApps'** con el modo de acceso 'No interactivo'.

### <a name="how-to-update-user-access-mode"></a>Cómo actualizar el modo de acceso del usuario

Para actualizar el modo de acceso del usuario del Comprobador de PowerApps:

1. Abra la organización de Common Data Service y vaya a **Configuración** > **Seguridad** > **Usuarios**.
2. Seleccione el usuario del **“Comprobador de PowerApps”** de la lista de usuarios y haga doble clic para abrir el formulario de usuario.
3. Vaya a la sección **'Administración'** > **'Información de licencia de acceso de cliente (CAL)'** del formulario.
4. Seleccione **'No interactivo'** en el control desplegable **Modo de acceso**.<br/>
![Modo de acceso](media/solution-checker-access-mode.png)

5. Guarde y cierre el formulario de usuario.
6. Volver a ejecutar el Comprobador de soluciones

## <a name="solution-checker-fails-due-to-disabled-first-party-application-in-aad"></a>El comprobador de soluciones falla debido a que la aplicación de primera parte está deshabilitada en AAD

La identidad de la aplicación de empresa de primera parte utilizada por el Comprobador de soluciones (PowerApps-Advisor) no debe ser deshabilitada en Azure Active Directory (AAD). Si está deshabilitada, la identidad no puede autenticarse cuando se solicitan tokens de portador para Common Data Service y otros proveedores necesarios de recursos en nombre del usuario que realiza la solicitud. 

Siga los pasos indicados a continuación para comprobar que la identidad de la aplicación no se ha deshabilitado en AAD y, si es necesario, habilite la aplicación.

### <a name="how-to-verify-andor-modify-application-enabled-status"></a>Cómo comprobar y/o modificar el estado habilitado de la aplicación

Para comprobar y/o modificar el estado habilitado de la identidad de la aplicación empresarial PowerApps-Advisor

1. Obtenga acceso al inquilino en el [Portal de Azure Active Directory (AAD)](https://aad.portal.azure.com/).
2. Navegue a **Otras aplicaciones**.
3. Seleccione **Toda la aplicación** y busque **'PowerApps-Advisor'**.<br/>
![Busque la aplicación de PowerApps-Advisor](media/solution-checker-search-advisor-app.png)

4. Seleccione **“PowerApps-Advisor”** para ver los detalles de la aplicación.
5. Seleccione **Propiedades**.
6. Compruebe el estado de **Habilitado para que los usuarios inicien sesión**. Si **'No'**, la aplicación se ha deshabilitado.<br/>
![Aplicación de empresa deshabilitada](media/solution-checker-disabled-app.png)

7. Seleccione el control de radio para cambiar el valor a **'Sí'**. Se habilita la aplicación.<br/>
![Habilitar aplicación PowerApps-Advisor](media/solution-checker-enable-app.png)

8. Seleccione **Guardar**. La aplicación está habilitada ahora. Es posible que tenga que esperar unos minutos para que el cambio se propague.
9. Volver a ejecutar el Comprobador de soluciones

> [!IMPORTANT]
> Debe tener privilegios de administrador en Azure Active Directory (AAD) para editar aplicaciones empresariales.

## <a name="solution-checker-fails-to-export-solutions-with-draft-business-process-flow-components"></a>El Comprobador de soluciones no exporta soluciones con componentes de flujo de proceso de negocio de borrador

Si una solución contiene un componente del flujo de proceso de negocio con el estado de borrador que nunca se ha activado anteriormente, el Comprobador de soluciones no podrá exportar la solución para análisis. Este error no es exclusivo del Comprobador de soluciones y es producido por el flujo de proceso de negocio que tiene una dependencia en un componente de entidad de apoyo (personalizado) que no se crea hasta que el flujo de proceso de negocio se activa por primera vez. Este problema también puede producirse si un flujo de proceso de negocio se activa desde el Explorador de soluciones.

Referencia [Artículo de KB #4337537: Exportación no válida - Falta entidad de proceso de negocio](https://support.microsoft.com/en-hk/help/4337537/invalid-export-business-process-entity-missing) para obtener más información sobre el problema y pasos para la resolución.

## <a name="solution-checker-fails-to-export-patched-solutions"></a>El Comprobador de soluciones no exporta las soluciones con parches

Si a una solución se le han aplicado [parches](https://docs.microsoft.com/powerapps/developer/common-data-service/create-patches-simplify-solution-updates), el Comprobador de soluciones no podrá exportar la solución para analizarla. Cuando se aplicaron parches a una solución, la solución original pasa a bloquearse y no se puede cambiarla o exportarla mientras haya revisiones dependientes que existan en la organización que identifica la solución como solución primaria.

Para resolver este problema, clone la solución para que todos los parches relacionados con la solución se implementen en una solución recién creada. Esto desbloquea la solución y permite exportarla desde el sistema.  Para obtener más información, consulte [Clonar una solución](use-segmented-solutions-patches-simplify-updates.md#clone-a-solution).

## <a name="solution-checker-will-not-analyze-empty-solutions"></a>El Comprobador de soluciones no analizará soluciones vacías

Si el Comprobador de soluciones exporta una solución que no contiene componentes para analizar, finalizará el posterior procesamiento y considerará la ejecución un error. Asegúrese de que la solución seleccionada enviada para un análisis del Comprobador de soluciones contiene al menos un componente.

## <a name="solution-checker-fails-to-export-large-solutions"></a>El Comprobador de soluciones no exporta soluciones grandes

La escenario principal por el que no se exporta una solución grande desde el entorno de Common Data Service implica una excepción de tiempo de espera en la solicitud de exportación. Esto se producirá si la solicitud supera 20 minutos. Las soluciones pesadas, como la solución predeterminada, puedan experimentar errores para poder exportarse en este intervalo de tiempo y la comprobación no se completará correctamente. Si el Comprobador de soluciones encuentra un tiempo de espera agotado durante la exportación, lo volverá a intentar tres veces antes de que dé error en el trabajo, por lo que pueden pasar más de una hora antes de que reciba una notificación de error.

La solución provisional es crear soluciones más pequeñas con menos componentes para analizar. Si el gran tamaño del archivo de la solución se debe a muchos componentes de ensamblado de complementos, consulte las instrucciones en [Optimizar el desarrollo de ensamblados personalizados](../../developer/common-data-service/best-practices/business-logic/optimize-assembly-development.md). 

> [!IMPORTANT]
> Para reducir los falsos positivos, asegúrese de agregar las personalizaciones dependientes. Cuando cree una solución y agregue estos componentes, incluya lo siguiente:
> - Cuando agregue complementos, incluya las Pasos de procesamiento de mensajes de SDK para el complemento.
> - Cuando agregue formularios de entidades, incluya los recursos web de JavaScript que se adjuntan a los eventos de formulario.  
> - Cuando agregue recursos web de JavaScript, incluya cualquier recurso web de JavaScript dependiente.
> - Cuando agregue recursos web de HTML, incluya cualquier dependiente script que esté definido en el recurso web HTML.
> - Cuando agregue flujos de trabajo personalizados, incluya el ensamblado que se usa en el flujo de trabajo.

## <a name="line-number-references-for-issues-in-html-resources-with-embedded-javascript-are-not-correct"></a>Las referencias de número de línea para problemas en los recursos de HTML con JavaScript insertada no son correctas 

Cuando se procesan recursos web HTML en el Comprobador de soluciones, el recurso web HTML se procesa independientemente de JavaScript en el recurso de web HTML. Por este motivo, el número de número de línea de la infracción detectada en `<script>` del recurso web HTML no es correcto.

## <a name="web-unsupported-syntax-issue-for-web-resources"></a>Problema de sintaxis web no admitida para recursos web

ECMAScript 6 (2015) o las versiones posteriores no se admiten actualmente en el Comprobador de soluciones. Cuando el Comprobador de soluciones analiza JavaScript con ECMAScript 6 o versiones posteriores, se registra un problema de sintaxis web no admitida para el recurso web.  

## <a name="multiple-violations-reported-for-plug-ins-and-workflow-activities-based-on-call-scope"></a>Informes de varias infracciones para complementos y actividades de flujo de trabajo en función de ámbito de llamada

Para reglas de complemento y de actividad de flujo de trabajo donde el problema sólo es relevante en el contexto de llamadas, la herramienta Comprobador de soluciones inicia su análisis en la implementación de la interfaz de IPlugin y atraviesa un gráfico de llamada para detectar problemas en el ámbito de esa implementación.  En algunos casos, muchas rutas de llamada pueden llegar a la misma ubicación donde se detecta el problema.  Puesto que el problema es relevante al ámbito de llamadas, la herramienta puede informar en función de ese ámbito para proporcionar una mejor imagen del impacto en lugar de en ubicaciones distintas. Como resultado, varios problemas pueden hacer referencia a una sola ubicación que deben ser corregida.

## <a name="see-also"></a>Vea también
[Prácticas recomendadas e instrucciones para Common Data Service](../../developer/common-data-service/best-practices/index.md)<br/>
[Prácticas recomendadas e instrucciones para aplicaciones basadas en modelos](../../developer/model-driven-apps/best-practices/index.md)<br/>
