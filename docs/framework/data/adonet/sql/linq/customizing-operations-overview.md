---
title: "Cenni preliminari sulla personalizzazione delle operazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a3546296-1443-4b88-aa6e-d41011041ba7
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Cenni preliminari sulla personalizzazione delle operazioni
Per impostazione predefinita, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene generato codice SQL dinamico per le operazioni di inserimento, aggiornamento ed eliminazione basate su mapping. In pratica, tuttavia, la logica di business viene generalmente aggiunta per fornire sicurezza, convalida e così via.  
  
 Di seguito sono riportate alcune delle tecniche [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] per la personalizzazione di queste operazioni.  
  
## Caricamento di opzioni  
 Nelle query è possibile controllare la quantità di dati relativi alla destinazione principale recuperata durante la connessione al database.  Questa funzionalità viene ampiamente implementata usando <xref:System.Data.Linq.DataLoadOptions>.  Per altre informazioni, vedere [Caricamento rinviato e immediato](../../../../../../docs/framework/data/adonet/sql/linq/deferred-versus-immediate-loading.md).  
  
## Metodi parziali  
 Nel mapping predefinito di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] vengono forniti metodi parziali per facilitare l'implementazione della logica di business.  Per altre informazioni, vedere [Aggiunta della logica di business utilizzando i metodi parziali](../../../../../../docs/framework/data/adonet/sql/linq/adding-business-logic-by-using-partial-methods.md).  
  
## Stored procedure e funzioni definite dall'utente  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] supporta l'uso di stored procedure e funzioni definite dall'utente.  Le stored procedure vengono solitamente usate per personalizzare operazioni.  Per altre informazioni, vedere [Stored procedure](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md).  
  
## Vedere anche  
 [Personalizzazione delle operazioni Insert, Update e Delete](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)