---
title: "Uso di WS-AtomicTransaction | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Protocollo WS-AT [WCF]"
ms.assetid: 04a4c200-0af0-4c5d-a3d9-87cb7339e054
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Uso di WS-AtomicTransaction
WS\-AtomicTransaction \(WS\-AT\) è un protocollo di transazione interoperativo.Consente di propagare transazioni distribuite utilizzando i messaggi dei servizi Web e di eseguire il coordinamento in modo interoperativo tra infrastrutture di transazioni eterogenee.WS\-AT utilizza il protocollo di commit a due fasi per condurre un risultato atomico tra applicazioni distribuite, gestori di transazioni e gestori di risorse.  
  
 L'implementazione di WS\-AT fornita da [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] comprende un servizio di protocollo incorporato nel gestore di transazioni MSDTC \(Microsoft Distributed Transaction Coordinator\).Utilizzando WS\-AT, le applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] possono propagare le transazioni ad altre applicazioni, compresi servizi Web interoperativi creati mediante tecnologie di terze parti.  
  
 Durante la propagazione di una transazione tra un'applicazione client e un'applicazione server, il protocollo di transazione utilizzato viene determinato dall'associazione esposta dal server sull'endpoint selezionato dal client.Alcune associazioni fornite dal sistema [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] specificano per impostazione predefinita il protocollo `OleTransactions` come formato di propagazione delle transazioni, mentre altre specificano il protocollo WS\-AT.La scelta del protocollo di transazione può anche essere modificata a livello di codice all'interno di una determinata associazione.  
  
 La scelta del protocollo influisce sugli elementi seguenti:  
  
-   Formato delle intestazioni dei messaggi utilizzate propagare la transazione dal client al server.  
  
-   Protocollo di rete utilizzato per eseguire il protocollo di commit a due fasi tra il gestore di transazioni del client e la transazione del server, al fine di risolvere il risultato della transazione.  
  
 Se il server e il client vengono scritti utilizzando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], non è necessario utilizzare WS\-AT.È possibile invece utilizzare le impostazioni predefinite di `NetTcpBinding` con l'attributo `TransactionFlow` abilitato, in modo da utilizzare il protocollo `OleTransactions`.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][\<netTcpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md).In caso contrario, se le transazioni vengono propagate a servizi Web basati su tecnologie di terze parti, sarà necessario utilizzare WS\-AT.  
  
## Vedere anche  
 [Configurazione del supporto transazioni WS\-Atomic](../../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)