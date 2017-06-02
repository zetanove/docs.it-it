---
title: "Procedura: generare e utilizzare eventi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "eventi [.NET Framework], generazione"
  - "eventi [.NET Framework], esempi"
  - "generazione di eventi"
ms.assetid: 42afade7-3a02-4f2e-868b-95845f302f8f
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: generare e utilizzare eventi
Gli esempi di questo argomento, illustriamo come utilizzare gli eventi.  Comprendono esempi di un delegato <xref:System.EventHandler>, il delegato <xref:System.EventHandler%601> e un delegato personalizzato, per illustrare gli eventi con e senza dati.  
  
 Negli esempi vengono utilizzati i concetti descritti nell'articolo [Eventi](../../../docs/standard/events/index.md).  
  
## Esempio  
 Nel primo esempio, viene illustrato come generare e utilizzare un evento che non dispone di dati.  Contiene una classe denominata `Counter` che dispone di un evento denominato `ThresholdReached`.  L'evento viene generato, quando il valore del contatore è maggiore o uguale ad un valore soglia.  Il delegato <xref:System.EventHandler> è associato all'evento, poiché non viene fornito nessun dato dell'evento.  
  
 [!code-csharp[EventsOverview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programnodata.cs#5)]
 [!code-vb[EventsOverview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1nodata.vb#5)]  
  
## Esempio  
 Il prossimo esempio, mostra come generare e utilizzare un evento che fornisce dati.  Il delegato <xref:System.EventHandler%601> è associato all'evento e viene fornita un'istanza di un oggetto dati dell'evento personalizzato.  
  
 [!code-cpp[EventsOverview#6](../../../samples/snippets/cpp/VS_Snippets_CLR/eventsoverview/cpp/programwithdata.cpp#6)]
 [!code-csharp[EventsOverview#6](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programwithdata.cs#6)]
 [!code-vb[EventsOverview#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1withdata.vb#6)]  
  
## Esempio  
 Nell'esempio seguente, viene illustrato come viene dichiarato un delegato per un evento.  Il delegato è denominato `ThresholdReachedEventHandler`.  Si tratta solo di un esempio.  In genere, non è necessario dichiarare un delegato per un evento, perché è possibile utilizzare il <xref:System.EventHandler> o delegato di <xref:System.EventHandler%601>.  Si dovrebbe dichiarare un delegato solamente in rari scenari, come la realizzazione di una classe che mette a disposizione codice legacy che non può essere utilizzato genericamente.  
  
 [!code-csharp[EventsOverview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programwithdelegate.cs#7)]
 [!code-vb[EventsOverview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1withdelegate.vb#7)]  
  
## Vedere anche  
 [Eventi](../../../docs/standard/events/index.md)