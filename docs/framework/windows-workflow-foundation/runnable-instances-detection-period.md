---
title: "Runnable Instances Detection Period | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4ea5c787-b638-47fd-bfc8-ede8c2898ce6
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Runnable Instances Detection Period
L'archivio di istanze del flusso di lavoro SQL esegue un'attività interna che attiva e rileva periodicamente istanze eseguibili o attivabili nel database di persistenza.La proprietà **Runnable Instances Detection Period** dell'archivio di istanze del flusso di lavoro SQL specifica il periodo di tempo dopo cui l'archivio di istanze del flusso di lavoro SQL esegue un'attività di rilevamento per individuare eventuali istanze del flusso di lavoro eseguibili o attivabili nel database di persistenza dopo il ciclo di rilevamento precedente.  
  
 L'impostazione di un intervallo più breve per questa proprietà riduce il tempo tra la scadenza di un timer associato a un'istanza del flusso di lavoro e la segnalazione dell'evento e il successivo caricamento dell'istanza.Tuttavia, aumenta anche il carico di elaborazione su un host e ciò può risultare non appropriato in scenari con timer durevoli e\/o errori host.Il tipo della proprietà è TimeSpan e il valore della proprietà segue il formato: hh:mm:ss.Il valore minimo per questa proprietà è 00:00:01.Il valore predefinito della proprietà è 00:00:05.  
  
 Per ulteriori informazioni sul rilevamento e l'attivazione di istanze del flusso di lavoro eseguibili e attivabili, vedere [Attivazione di istanze](../../../docs/framework/windows-workflow-foundation//instance-activation.md).