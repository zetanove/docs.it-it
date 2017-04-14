---
title: "Attenuazione: AuthorizationContext predefinito | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6cfeee63-b148-429a-a7e6-6fe9b0cb7610
caps.latest.revision: 3
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 3
---
# Attenuazione: AuthorizationContext predefinito
L'implementazione dell'oggetto <xref:System.IdentityModel.Policy.AuthorizationContext> restituito da una chiamata al metodo <xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext%28System.Collections.Generic.IList%7BSystem.IdentityModel.Policy.IAuthorizationPolicy%7D%29> con un argomento `null` `authorizationPolicies` è cambiata in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)].  
  
## Impatto  
 In rari casi, le app WCF che usano l'autenticazione personalizzata possono riscontrare differenze di comportamento.  
  
## Attenuazione  
 È possibile ripristinare il comportamento precedente in due modi diversi:  
  
-   Ricompilare l'app per destinarla a una versione precedente rispetto a .NET Framework 4.6.  Per i servizi ospitati in IIS, usare l'elemento `<httpRuntime targetFramework="x.x" />` per destinare l'app a una versione precedente di .NET Framework.  
  
-   Aggiungere la riga seguente alla sezione `<appSettings>` del file app.config:  
  
    ```  
    <add key="appContext.SetSwitch:Switch.System.IdentityModel.EnableCachedEmptyDefaultAuthorizationContext" value="true" />  
    ```  
  
## Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)