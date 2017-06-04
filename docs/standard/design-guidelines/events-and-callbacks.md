---
title: "Eventi e callback | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "eventi di estensibilità [.NET Framework]"
  - "callback, metodi [.NET Framework]"
  - "metodi di callback"
  - "callback"
ms.assetid: 48b55c60-495f-4089-9396-97f9122bba7c
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Eventi e callback
I callback sono i punti di estensibilità che consentono a un framework richiamare il codice utente tramite un delegato. Questi delegati sono in genere passati al framework tramite un parametro di un metodo.  
  
 Gli eventi sono un tipo speciale di callback che supporta la sintassi semplice e coerenza per fornire il delegato \(un gestore eventi\). Inoltre, il completamento delle istruzioni e finestre di progettazione di Visual Studio forniscono informazioni sull'utilizzo di API basate su eventi. Per informazioni, vedere [Progettazione di eventi](../../../docs/standard/design-guidelines/event.md).  
  
 **✓ PROVARE** tramite callback per consentire agli utenti di fornire codice personalizzato deve essere eseguito dal framework.  
  
 **✓ PROVARE** utilizzo di eventi per consentire agli utenti di personalizzare il comportamento di un framework senza la necessità di informazioni sulla progettazione orientata agli oggetti.  
  
 **✓ si** preferire gli eventi semplici callback, perché sono più familiare per una gamma più ampia di sviluppatori e sono integrati con il completamento delle istruzioni di Visual Studio.  
  
 **X evitare** tramite callback nelle API sensibili alle prestazioni.  
  
 **✓ si** utilizzare il nuovo `Func<...>`, `Action<...>`, o `Expression<...>` tipi anziché delegati personalizzati, quando si definiscono le API con i callback.  
  
 `Func<...>` e `Action<...>` rappresentano delegati generici.`Expression<...>` rappresenta le definizioni di funzione che possono essere compilate e successivamente richiamate in fase di esecuzione ma che può anche essere serializzate e passate a processi remoti.  
  
 **✓ si** misurare e comprendere le implicazioni sulle prestazioni dell'utilizzo `Expression<...>`, anziché `Func<...>` e `Action<...>` delegati.  
  
 `Expression<...>` i tipi sono in genere logicamente equivalente a `Func<...>` e `Action<...>` delegati. La differenza principale è che i delegati sono destinati a essere utilizzato in scenari di processo locale. le espressioni devono essere casi in cui è utile e consente di valutare l'espressione in un computer o un processo remoto.  
  
 **✓ si** comprendere che la chiamata a un delegato, si eseguono codice arbitrario e che potrebbe avere ripercussioni di sicurezza, correttezza e compatibilità.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Progettazione finalizzata all'estensibilità](../../../docs/standard/design-guidelines/designing-for-extensibility.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)