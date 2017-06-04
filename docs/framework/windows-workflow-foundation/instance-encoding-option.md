---
title: "Instance Encoding Option | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 89e4b029-4f68-438c-8117-9b21fe094ef4
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Instance Encoding Option
La proprietà **Instance Encoding Option** dell'archivio di istanze del flusso di lavoro SQL consente di specificare se il provider di persistenza SQL deve comprimere le informazioni sullo stato dell'istanza del flusso di lavoro utilizzando l'algoritmo GZip prima di salvare le informazioni nel database di persistenza.I valori consentiti per questa proprietà sono GZip e None.Il valore predefinito è None.Nell'elenco seguente vengono descritte queste opzioni.  
  
1.  **GZip**.Il provider di persistenza codifica le informazioni sullo stato utilizzando l'algoritmo GZip prima di rendere persistenti le informazioni sullo stato nel database di persistenza.  
  
2.  **None**.Il provider di persistenza non codifica le informazioni sullo stato prima di salvare le informazioni nel database di persistenza.  
  
 La codifica delle informazioni sullo stato dell'istanza del flusso di lavoro tramite l'algoritmo GZip riduce il consumo di memoria nel database SQL e anche l'utilizzo della rete se il database si trova in un computer della rete diverso dal computer in cui è in esecuzione l'host del servizio del flusso di lavoro.Se lo stato dell'istanza del flusso di lavoro è piccolo è consigliabile impostare la proprietà **Instance Encoding Option** su **None**.