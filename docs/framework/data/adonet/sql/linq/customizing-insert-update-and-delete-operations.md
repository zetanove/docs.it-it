---
title: "Personalizzazione delle operazioni Insert, Update e Delete | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 07eef055-8f6c-414d-850e-d323ff946cd0
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Personalizzazione delle operazioni Insert, Update e Delete
Per impostazione predefinita, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene generato codice SQL dinamico per implementare le operazioni di inserimento, lettura, aggiornamento ed eliminazione.  In pratica, tuttavia, l'applicazione viene in genere personalizzata per soddisfare specifiche esigenze aziendali.  
  
> [!NOTE]
>  Se si usa [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)], è possibile personalizzare le operazioni di inserimento, aggiornamento ed eliminazione tramite [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)].  
  
 Negli argomenti di questa sezione vengono descritte le tecniche offerte da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] per personalizzare le operazioni di inserimento, lettura, aggiornamento ed eliminazione in un'applicazione.  
  
## In questa sezione  
 [Cenni preliminari sulla personalizzazione delle operazioni](../../../../../../docs/framework/data/adonet/sql/linq/customizing-operations-overview.md)  
 Vengono descritte le diverse tecniche fornite da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] per personalizzare le operazioni di inserimento, lettura, aggiornamento ed eliminazione.  
  
 [Operazioni Insert, Update e Delete](../../../../../../docs/framework/data/adonet/sql/linq/insert-update-and-delete-operations.md)  
 Vengono descritti i processi predefiniti di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] per la modifica dei dati del database.  
  
 [Responsabilità dello sviluppatore nell'eseguire l'override del comportamento predefinito](../../../../../../docs/framework/data/adonet/sql/linq/responsibilities-of-the-developer-in-overriding-default-behavior.md)  
 Viene descritto il ruolo dello sviluppatore nell'implementazione dei requisiti non applicati da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 [Aggiunta della logica di business utilizzando i metodi parziali](../../../../../../docs/framework/data/adonet/sql/linq/adding-business-logic-by-using-partial-methods.md)  
 Viene descritto come usare metodi parziali per eseguire l'override dei metodi generati automaticamente.