---
title: "&lt;backupLists&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 593b3390-f65b-4684-ad40-0596b62f0954
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;backupLists&gt;
Rappresenta una sezione di configurazione per la definizione di un set di servizi di backup usati nella gestione degli errori.  Ogni elemento figlio è un elenco di backup che enumera un set di endpoint che si desidera vengano usati dal servizio di routing quando non è possibile raggiungere l'endpoint primario. Se il primo endpoint dell'elenco non funziona, il servizio di routing eseguirà automaticamente il failover nel successivo endpoint dell'elenco. In questo modo è possibile migliorare rapidamente l'affidabilità all'applicazione senza che sia necessario indicare all'applicazione client come gestire modelli complessi o la posizione in cui i servizi sono distribuiti.  
  
## Sintassi  
  
```vb  
  
<routing>  
  <backupLists>  
    <backupList name="String">  
      <add endpointName="String" />  
    </backupList>    
  </backupLists>  
</routing>  
  
```  
  
```csharp  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<filtro\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filter.md)|Contiene un elenco di endpoint che dovranno essere usati nel servizio di routing quando non è possibile raggiungere l'endpoint primario.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<routing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing.md)|Rappresenta una sezione di configurazione per la definizione di un set di filtri di routing che determinano il tipo di <xref:System.ServiceModel.Dispatcher.MessageFilter> di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] da usare durante la valutazione di messaggi in arrivo, nonché di tabelle di routing che definiscono gli endpoint di destinazione ai quali inviare i messaggi quando viene trovata una corrispondenza di filtro.|  
  
## Vedere anche  
 [System.ServiceModel.Routing.Configuration.BackupListCollection](assetId:///System.ServiceModel.Routing.Configuration.BackupListCollection?qualifyHint=False&amp;autoUpgrade=True)