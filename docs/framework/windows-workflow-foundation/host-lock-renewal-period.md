---
title: "Host Lock Renewal Period | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f8ba94fc-27e0-4d8e-8f85-50a6d2a3cd43
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Host Lock Renewal Period
La proprietà **Host Lock Renewal Period** dell'archivio di istanze del flusso di lavoro SQL consente di specificare il periodo di tempo entro il quale l'host rinnova il relativo blocco su un'istanza del flusso di lavoro.Il blocco rimane valido per Host Lock Renewal Period \+ 30 secondi.Se l'host non riesce a rinnovare il blocco \(ovvero estende il lease\) entro questo periodo di tempo, il blocco scade e il provider di persistenza sblocca l'istanza.Il valore di questa proprietà è di tipo TimeSpan nel formato "hh:mm:ss".Il valore minimo consentito è "00:00:01" \(1 secondo\).Il valore predefinito di questa proprietà è "00:00:30" \(30 secondi\).  
  
 Questa proprietà è significativa nelle situazioni in cui un host del servizio flusso di lavoro non riesce prima che possa sbloccare un'istanza del servizio flusso di lavoro che possiede.In questo scenario il blocco sull'istanza del servizio flusso di lavoro nel database di persistenza viene rimosso dal provider di persistenza dopo la scadenza del blocco in modo che un altro host del servizio flusso di lavoro in esecuzione nello stesso computer o in un altro computer in una server farm possa acquisire il blocco e caricare l'istanza del servizio flusso di lavoro in memoria per riprendere l'esecuzione dall'ultimo stato persistente.  
  
 L'impostazione di un valore più alto per questa proprietà determina il blocco delle istanze del servizio flusso di lavoro nel database di persistenza per un periodo più lungo e pertanto il recupero dell'istanza dall'ultimo punto di persistenza viene ritardato.L'impostazione di un intervallo breve per questa proprietà determina il prelievo in modo rapido dell'istanza del servizio flusso di lavoro da parte dell'host del servizio flusso di lavoro, ma provoca un aumento del carico di lavoro per l'host del servizio flusso di lavoro e il database di SQL Server.  
  
 L'archivio di istanze del flusso di lavoro SQL esegue un'attività interna che attiva e rileva periodicamente istanze i cui blocchi sono scaduti.Quando trova istanze con i blocchi scaduti, posiziona le istanze nella tabella RunnableInstances in modo che queste istanze possano essere prelevate ed eseguite da un host del flusso di lavoro.