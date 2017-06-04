---
title: "Utilizzo di gestori eccezioni filtrati dall&#39;utente | Microsoft Docs"
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
  - "eccezioni, filtrate dall'utente"
  - "eccezioni filtrate dall'utente"
ms.assetid: aa80d155-060d-41b4-a636-1ceb424afee8
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Utilizzo di gestori eccezioni filtrati dall&#39;utente
In Visual Basic sono attualmente supportate eccezioni filtrate dall'utente.  I gestori eccezioni filtrati dall'utente intercettano e gestiscono le eccezioni in base a requisiti definiti dall'utente per le singole eccezioni.  Tali gestori utilizzano l'istruzione **Catch** con la parola chiave **When**.  
  
 Questa tecnica è utile quando un particolare oggetto eccezione corrisponde a più errori.  In questo caso l'oggetto presenta in genere una proprietà che contiene il codice di errore specifico associato all'errore.  È possibile utilizzare la proprietà del codice di errore nell'espressione per selezionare solo l'errore particolare che si desidera gestire in tale clausola **Catch**.  
  
 Nell'esempio di Visual Basic che segue viene illustrata l'istruzione **Catch\/When**.  
  
```  
Try  
      'Try statements.  
   Catch When Err = VBErr_ClassLoadException  
      'Catch statements.  
End Try  
```  
  
 L'espressione della clausola filtrata dall'utente non è sottoposta ad alcuna restrizione.  Se durante l'esecuzione dell'espressione filtrata dall'utente si verifica un'eccezione, quest'ultima viene ignorata e si considera che l'espressione di filtro abbia restituito il valore false.  In questo caso, Common Language Runtime continua la ricerca di un gestore per l'eccezione corrente.  
  
## Combinazione di un'eccezione specifica e di clausole filtrate dall'utente  
 Un'istruzione catch può contenere sia l'eccezione specifica che le clausole filtrate dall'utente.  Nel runtime viene prima eseguito il test dell'eccezione specifica.  Se l'eccezione specifica ha esito positivo, verrà eseguito il filtro dell'utente.  Il filtro generico può contenere un riferimento alla variabile dichiarata nel filtro della classe.  Si noti che non è possibile invertire l'ordine delle due clausole di filtro.  
  
 Nell'esempio di Visual Basic riportato di seguito vengono illustrate l'eccezione specifica `ClassLoadException` nell'istruzione **Catch** e la clausola filtrata dall'utente che utilizza la parola chiave **When**.  
  
```  
Try  
      'Try statements.  
   Catch cle As ClassLoadException When cle.IsRecoverable()  
      'Catch statements.  
End Try  
```  
  
## Vedere anche  
 [Procedura: Usare il blocco try\/catch per l'intercettazione di eccezioni](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)   
 [Procedura: utilizzare eccezioni specifiche in un blocco catch](../../../docs/standard/exceptions/how-to-use-specific-exceptions-in-a-catch-block.md)   
 [Suggerimenti per le eccezioni](../../../docs/standard/exceptions/best-practices-for-exceptions.md)   
 [Nozioni fondamentali sulla gestione delle eccezioni](../../../docs/standard/exceptions/exception-handling-fundamentals.md)