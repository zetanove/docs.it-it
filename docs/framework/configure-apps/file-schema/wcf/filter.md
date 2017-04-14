---
title: "&lt;filtro&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3266700b-904b-44e4-93a7-e06a1a445100
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;filtro&gt;
Definisce un filtro di routing che determina il tipo di <xref:System.ServiceModel.Dispatcher.MessageFilter> di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] da usare durante la valutazione di messaggi in arrivo, nonché gli eventuali dati o parametri di supporto necessari per il filtro.  
  
## Sintassi  
  
```vb  
  
<routing>  
      <filters>  
        <filter customType=”String”  
                filterData=”String”  
                filterType="Action/Address/AddressPrefix/And/Custom/Endpoint/MatchAll/XPath"   
                name="String" />  
      </filters>  
</routing>  
  
```  
  
```csharp  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|customType|Stringa contenente il nome di tipo completo del tipo personalizzato da usare come filtro. Se `filterType`è impostato su `custom`, questo attributo contiene il nome di tipo completo della classe da creare. `filterData` può inoltre contenere valori da usare durante la valutazione del filtro di tipo personalizzato.|  
|filterData|Stringa contenente i dati del filtro.  Per altre informazioni su come specificare questo attributo, vedere <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A>.|  
|filterType|Stringa contenente i tipo di filtro.  L'attributo è di tipo <xref:System.ServiceModel.Routing.Configuration.FilterType>.  Per altre informazioni sul funzionamento con l'attributo `filterData`, vedere <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A>.|  
|name|Stringa contenente il nome univoco di questo elemento di filtro.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<routing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing.md)|Sezione di configurazione per la definizione di un set di filtri di routing che determinano il tipo di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]<xref:System.ServiceModel.Dispatcher.MessageFilter> da usare durante la valutazione di messaggi in arrivo.|  
  
## Vedere anche  
 [System.ServiceModel.Routing.Configuration.FilterElement](assetId:///System.ServiceModel.Routing.Configuration.FilterElement?qualifyHint=False&amp;autoUpgrade=True)   
 <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A>   
 <xref:System.ServiceModel.Routing.Configuration.FilterType>