---
title: "Procedura: Eseguire modifiche di base delle stringhe in .NET Framework | Microsoft Docs"
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
  - "stringhe [.NET Framework], esempi"
ms.assetid: 121d1eae-251b-44c0-8818-57da04b8215e
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: Eseguire modifiche di base delle stringhe in .NET Framework
Nell'esempio di codice che segue vengono utilizzati alcuni metodi discussi in [Operazioni di base sulle stringhe](../../../docs/standard/base-types/basic-string-operations.md) per costruire una classe che esegua manipolazioni di stringhe, come può avvenire in un'applicazione reale.  Nella classe `MailToData` il nome e l'indirizzo di un individuo vengono memorizzati in proprietà separate e viene fornito un modo per combinare i campi `City`, `State` e `Zip` in una singola stringa da visualizzare all'utente.  Questa classe inoltre consente all'utente di inserire le informazioni relative a città, provincia e CAP in forma di una singola stringa. Tramite l'applicazione la stringa verrà quindi analizza automaticamente e le informazioni corrette verranno inserite nella proprietà corrispondente.  
  
 Nell'esempio viene utilizzata per semplicità un'applicazione di console con un'interfaccia della riga di comando.  
  
## Esempio  
 [!code-csharp[Conceptual.String.BasicOps#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/basicops.cs#1)]
 [!code-vb[Conceptual.String.BasicOps#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/basicops.vb#1)]  
  
 Al momento dell'esecuzione del codice precedente all'utente viene richiesto di inserire nome e indirizzo.  Le informazioni verranno collocate nelle proprietà corrette e verranno nuovamente visualizzate all'utente in una singola stringa contenente le informazioni relative a città, provincia e CAP.  
  
## Vedere anche  
 [Operazioni di base su stringhe](../../../docs/standard/base-types/basic-string-operations.md)