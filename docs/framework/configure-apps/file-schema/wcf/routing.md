---
title: "&lt;routing&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a210c209-3940-4288-9a8e-39b1e62606bc
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;routing&gt;
Rappresenta una sezione di configurazione per la definizione di un set di filtri di routing che determinano il tipo di <xref:System.ServiceModel.Dispatcher.MessageFilter> di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] da usare durante la valutazione di messaggi in arrivo, nonché di tabelle di routing che definiscono gli endpoint di destinazione ai quali inviare i messaggi quando viene trovata una corrispondenza di filtro.  
  
## Sintassi  
  
```vb  
  
<routing>  
      <filters>  
        <filter customType=”String”  
                filterData=”String”  
                filterType="Action/Address/AddressPrefix/And/Custom/Endpoint/MatchAll/XPath"   
                name="String" />  
      </filters>  
      <routingTables>  
        <table name="String">  
          <entries>  
            <add endpoint="String"   
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
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<filtri\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filters-of-routing.md)|Contiene un set di filtri di routing che determinano il tipo di MessageFilter di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] che verrà usato durante la valutazione di messaggi in arrivo.|  
|[\<filterTables\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filtertables.md)|Contiene i mapping tra i filtri di routing e gli endpoint di destinazione per la specifica dell'endpoint da usare quando viene trovata una corrispondenza di filtro.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|system.ServiceModel|Elemento radice di tutti gli elementi di configurazione WCF.|  
  
## Vedere anche  
 [System.ServiceModel.Routing.Configuration.RoutingSection](assetId:///System.ServiceModel.Routing.Configuration.RoutingSection?qualifyHint=False&amp;autoUpgrade=True)