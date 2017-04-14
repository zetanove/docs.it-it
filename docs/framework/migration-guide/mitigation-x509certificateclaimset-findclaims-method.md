---
title: "Attenuazione: Metodo X509CertificiateClaimSet.FindClaims | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee356e3b-f932-48f5-875a-5e42340bee63
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 3
---
# Attenuazione: Metodo X509CertificiateClaimSet.FindClaims
A partire dalle app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], il metodo <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=fullName> tenterà di far corrispondere l'argomento `claimType` con tutte le voci DNS nel relativo campo SAN.  
  
## Impatto  
 Questa modifica interessa solo le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)].  
  
 Per le app destinate alle versioni precedenti di .NET Framework, il metodo <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=fullName> prova a far corrispondere l'argomento `claimType` solo con l'ultima voce DNS.  
  
## Attenuazione  
 Se la modifica è indesiderata, le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] la possono rifiutare esplicitamente aggiungendo l'impostazione di configurazione seguente alla sezione [\<runtime\>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file di configurazione dell'app:  
  
```xml  
  
<runtime> <AppContextSwitchOverrides value="Switch.System.IdentityModel.DisableMultipleDNSEntriesInSANCertificate=true" /> </runtime>  
  
```  
  
 Inoltre, le app destinate alle versioni precedenti di .NET Framework, ma in esecuzione su [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] possono optare per questo comportamento aggiungendo l'impostazione di configurazione seguente alla sezione [\<runtime\>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file di configurazione dell'app:  
  
```xml  
  
<runtime> <AppContextSwitchOverrides value="Switch.System.IdentityModel.DisableMultipleDNSEntriesInSANCertificate=false" /> </runtime>  
  
```  
  
## Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-1.md)