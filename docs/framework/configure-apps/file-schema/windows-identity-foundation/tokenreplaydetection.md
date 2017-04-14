---
title: "&lt;tokenReplayDetection&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ac3f588e-5f75-4275-b969-2d492ecc3b47
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;tokenReplayDetection&gt;
Consente il rilevamento riproduzione di token e specifica la data di scadenza dei token.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <tokenReplayDetection enabled=xs:boolean expirationPeriod=TimeSpan>  
    </tokenReplayDetection>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Tipo  
 <xref:System.IdentityModel.Configuration.TokenReplayDetectionElement>  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|enabled|Un valore che specifica se il rilevamento riproduzione dei token è abilitato; “true„ attivazione del rilevamento riproduzione dei token.|  
|expirationPeriod|<xref:System.TimeSpan> che specifica il tempo massimo di prima di un elemento viene considerata scaduta e rimosso dalla cache.  per ulteriori informazioni su come specificare i valori di <xref:System.TimeSpan> , vedere .|  
  
### Elementi figlio  
 Nessuno  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|Specifica le impostazioni dell' identità del livello di servizio.|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|Fornisce la configurazione per una raccolta di gestori del token di sicurezza.|  
  
## Note  
 Un elemento di `<tokenReplayDetection>` può essere specificato a livello del servizio nell' elemento di `<identityConfiguration>` o a livello di raccolta per la gestione del token di sicurezza nell' elemento di `<securityTokenHandlerConfiguration>` .  Impostazioni di override di raccolta di gestori di quelli specificati dal servizio.  
  
 Il tipo della cache token di tipo replay è specificato  dall' elemento.