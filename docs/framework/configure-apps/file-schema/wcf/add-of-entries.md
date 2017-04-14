---
title: "&lt;add&gt; di &lt;entries&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3af4805b-dc72-4f68-b168-da4fba8c6170
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;add&gt; di &lt;entries&gt;
Rappresenta una voce di routing che esegue il mapping di un filtro a un endpoint client definito in precedenza.  I messaggi che corrispondono a questo filtro verranno inviati a questa destinazione.  
  
## Sintassi  
  
```vb  
  
<routing>  
      <filterTables>  
        <filterTable name="String">  
          <entries>  
            <add backupList=”String”  
                 endpointName="String"   
                 filterName="String"   
                 priority="Integer" />  
          </entries>  
        </table>  
      </routingTables>  
</routing>  
  
```  
  
```csharp  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|backupList|Stringa che specifica un riferimento a un elenco di backup di endpoint.|  
|endpoint|Stringa che specifica un riferimento a un endpoint client che riceverà i messaggi corrispondenti al filtro specificato dall'attributo `filterName`.|  
|filterName|Stringa che specifica un riferimento a un elemento di filtro.|  
|priority|Integer che specifica la priorità di questa voce.<br /><br /> Le voci nella tabella di routing verranno valutate in base alla priorità, con 0 come priorità più bassa.  Tutte le voci per una priorità specifica vengono valutate simultaneamente. Se non viene trovata alcuna voce corrispondente per la priorità corrente, verrà valutato il livello di priorità successivo.<br /><br /> Questo valore è facoltativo.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<routing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing.md)|Sezione di configurazione contenente voci di mapping di routing.|  
  
## Vedere anche  
 [System.ServiceModel.Routing.Configuration.RoutingSection](assetId:///System.ServiceModel.Routing.Configuration.RoutingSection?qualifyHint=False&amp;autoUpgrade=True)   
 [System.ServiceModel.Routing.Configuration.FilterTableEntryElement](assetId:///System.ServiceModel.Routing.Configuration.FilterTableEntryElement?qualifyHint=False&amp;autoUpgrade=True)