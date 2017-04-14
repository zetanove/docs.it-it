---
title: "&lt;backupList&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a3d9d1f9-4a53-45e9-a880-86c8bee0b833
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;backupList&gt;
Rappresenta una sezione di configurazione per definire un elenco di backup che enumera un set di endpoint da usare nel servizio di routing quando non è possibile raggiungere l'endpoint primario. Se il primo endpoint dell'elenco non funziona, il servizio di routing eseguirà automaticamente il failover al successivo endpoint dell'elenco. In questo modo è possibile migliorare rapidamente l'affidabilità all'applicazione senza che sia necessario indicare all'applicazione client come gestire modelli complessi o la posizione in cui i servizi sono distribuiti.  
  
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
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|name|Stringa che specifica il nome usato per identificare l'elenco di endpoint.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<filtro\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filter.md)||  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<routing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing.md)|Elenco di endpoint di backup.|  
  
## Note  
 Questa sezione include una raccolta ordinata di endpoint ai quali verrà trasmesso un messaggio nel caso venga generata un'eccezione di comunicazione durante l'invio all'endpoint primario.  
  
 Se un invio all'endpoint primario elencato nell'attributo `endpointName` di [\<aggiunta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-entries.md) non riesce e viene generata un'eccezione di comunicazione, il servizio di routing tenterà di inviare il messaggio al primo endpoint incluso in questa sezione di configurazione.  Se anche questo invio non riesce e viene generata un'eccezione di comunicazione, il servizio di routing tenterà di inviare il messaggio all'endpoint successivo incluso in questa sezione fino a quando il tentativo di invio non ha esito positivo, non viene restituito un errore diverso da un'eccezione di comunicazione o tutti gli endpoint inclusi nella raccolta non restituiscono un errore.  
  
 Nell'esempio seguente, se un invio all'endpoint primario denominato "Destination" restituisce un'eccezione di comunicazione, il servizio tenterà di inviare il messaggio a "alternateServiceQueue".  Se anche questo tentativo restituisce un'eccezione di comunicazione, il servizio di routing tenterà di inviare il messaggio all'endpoint successivo incluso nella raccolta.  
  
```  
  
<filterTables>  
     <filterTable name="filterTable1">  
          <add filterName="MatchAllFilter1" endpointName="Destination" backupList="backupEndpointList"/>  
     </filterTable>  
</filterTables>  
<backupLists>  
     <backupList name="backupEndpointList">  
          <add endpointName="backupServiceQueue" />  
          <add endpointName="alternateServiceQueue" />  
     </backupList>  
</backupLists>  
```  
  
## Vedere anche  
 [System.ServiceModel.Routing.Configuration.BackupEndpointCollection](assetId:///System.ServiceModel.Routing.Configuration.BackupEndpointCollection?qualifyHint=False&amp;autoUpgrade=True)