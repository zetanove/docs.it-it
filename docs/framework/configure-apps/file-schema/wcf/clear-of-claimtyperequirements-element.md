---
title: "Elemento &lt;clear&gt; di &lt;claimTypeRequirements&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ef42fde7-f292-4610-9111-9fea382c3b5f
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Elemento &lt;clear&gt; di &lt;claimTypeRequirements&gt;
Specifica tutti i tipi di attestazioni da rimuovere nella credenziale federativa.  Ciò consente di assicurare che la raccolta sia inizialmente vuota.  
  
## Sintassi  
  
```  
  
<claimTypeRequirements>  
      <clear />  
</claimTypeRequirements>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<requisitiTipoAttestazione\>](../../../../../docs/framework/configure-apps/file-schema/wcf/claimtyperequirements-for-message.md)|Specifica una raccolta di tipi di attestazione obbligatori.  Ciascun elemento è di tipo <xref:System.ServiceModel.Configuration.ClaimTypeElement>.<br /><br /> In un scenario federato, i servizi attestano i requisiti per le credenziali in ingresso.  Ad esempio, le credenziali in ingresso devono disporre di un certo set di tipi di attestazioni.  Ogni elemento di questa raccolta specifica i tipi di attestazione obbligatori e facoltativi previsti in una credenziale federata.|  
  
## Vedere anche  
 <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.ClaimTypeRequirements%2A>   
 <xref:System.ServiceModel.Security.Tokens.ClaimTypeRequirement>   
 <xref:System.ServiceModel.Configuration.FederatedMessageSecurityOverHttpElement.ClaimTypeRequirements%2A>   
 <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>   
 <xref:System.ServiceModel.Configuration.ClaimTypeElement>