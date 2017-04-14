---
title: "&lt;providerPersistenza&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a37049c5-a7ea-4519-94f2-912eeb010380
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;providerPersistenza&gt;
Specifica il tipo di implementazione del provider di persistenza da usare, nonché il timeout da usare per le operazioni di persistenza.  
  
## Sintassi  
  
```  
  
<persistenceProvider persistenceOperationTimeout="TimeSpan"  
   type="String" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|persistenceOperationTimeout|Valore di tipo <xref:System.TimeSpan> che specifica il timeout usato per le operazioni di persistenza.  L'impostazione predefinita è "00:00:30".|  
|tipo|Stringa che specifica il tipo della factory del provider di persistenza da usare.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un elemento di comportamento.|  
  
## Note  
 Questo elemento specifica il provider di persistenza da usare per serializzare lo stato di un servizio WCF.  È necessario usarlo insieme a `wsHttpContextBinding`, che consente di passare le informazioni sullo stato nelle intestazioni HTTP.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.PersistenceProviderElement>   
 <xref:System.ServiceModel.Persistence.PersistenceProvider>