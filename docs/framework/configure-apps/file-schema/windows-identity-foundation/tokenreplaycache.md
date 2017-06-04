---
title: "&lt;tokenReplayCache&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1572ab23-6933-41b5-bfb4-0c4548145500
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;tokenReplayCache&gt;
Registra una cache di riesecuzione del token con un servizio o un insieme di gestore del token di protezione.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <caches>  
      <tokenReplayCache type=xs:string>  
      </tokenReplayCache>  
    </caches>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|type|Un tipo che deriva dal <xref:System.IdentityModel.Tokens.TokenReplayCache> classe.  Per ulteriori informazioni su come specificare un personalizzato `type`, vedere [Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences).|  
  
### Elementi figlio  
 Nessuno  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<caches\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/caches.md)|Registra le cache utilizzate da un servizio o un insieme di gestore del token di protezione.|  
  
## Note  
 La cache di riproduzione dei token viene utilizzata per rilevare i token riprodotti.  Rilevamento riproduzione token è abilitato per la [\<tokenReplayDetection\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaydetection.md) elemento che specifica anche la scadenza massima per i token.  
  
## Esempio  
 il XML riportato di seguito viene illustrata la configurazione di una cache personalizzata per il rilevamento di token riprodotti.  
  
```  
<caches>  
  <tokenReplayCache type="MyCacheLibrary.MyTokenReplayCache, MyCacheLibrary">  
  </tokenReplayCache>  
</caches>  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Tokens.TokenReplayCache>   
 [\<tokenReplayDetection\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaydetection.md)