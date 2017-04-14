---
title: "Generazione di eccezioni | Microsoft Docs"
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
  - "eccezioni, generazione"
  - "in modo esplicito la generazione di eccezioni"
  - "generazione di eccezioni, linee guida di progettazione"
ms.assetid: 5388e02b-52f5-460e-a2b5-eeafe60eeebe
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Generazione di eccezioni
Linee guida che generano eccezioni descritte in questa sezione richiedono una buona definizione del significato di errore di esecuzione. Errore di esecuzione si verifica ogni volta che un membro non è stato progettato per offrire \(quali il nome del membro implica\). Ad esempio, se il `OpenFile` metodo non può restituire un handle di file aperto al chiamante, viene considerato un errore di esecuzione.  
  
 Maggior parte degli sviluppatori acquisita familiarità con l'utilizzo di eccezioni per gli errori di utilizzo, ad esempio divisione per zero o un riferimento null. In Framework, le eccezioni vengono utilizzate per tutte le condizioni di errore, compresi gli errori di esecuzione.  
  
 **X non** restituiscono codici di errore.  
  
 Le eccezioni sono il mezzo principale di segnalazione degli errori di Framework.  
  
 **✓ si** segnala gli errori di esecuzione mediante la generazione di eccezioni.  
  
 **✓ PROVARE** terminare il processo chiamando `System.Environment.FailFast` \(funzionalità di .NET Framework 2.0\) anziché generare un'eccezione se il codice rileva una situazione in cui non è sicuro per l'esecuzione di ulteriori.  
  
 **X non** utilizzare eccezioni per il normale flusso di controllo, se possibile.  
  
 Fatta eccezione per gli errori di sistema e le operazioni con potenziali race condition, progettisti del framework necessario progettare le API in modo gli utenti possono scrivere codice che non vengono generate eccezioni. Ad esempio, è possibile fornire un modo per controllare le condizioni preliminari prima di chiamare un membro in modo gli utenti possono scrivere codice che non vengono generate eccezioni.  
  
 Il membro utilizzato per controllare le precondizioni di un altro membro è noto anche come un tester e il membro che esegue l'effettiva viene chiamato un agente.  
  
 Vi sono alcuni casi il modello Tester\-agente può avere un overhead di prestazioni accettabile. In questi casi, è necessario considerare il modello di analisi Try cosiddette \(vedere [Eccezioni e prestazioni](../../../docs/standard/design-guidelines/exceptions-and-performance.md) Per ulteriori informazioni\).  
  
 **✓ PROVARE** le implicazioni sulle prestazioni di generazione di eccezioni. Velocità di generazione superiore a 100 al secondo in genere influire notevolmente sulle prestazioni della maggior parte delle applicazioni.  
  
 **✓ si** documento tutte le eccezioni generate da membri chiamabili pubblicamente a causa di una violazione del membro del contratto \(invece di un errore di sistema\) e di manipolarli come parte del contratto.  
  
 Le eccezioni che fanno parte del contratto non devono modificare da una versione al successivo \(ad esempio, non è necessario modificare il tipo di eccezione e non devono essere aggiunte nuove eccezioni\).  
  
 **X non** sono membri pubblici che possono generare o non basato su un'opzione.  
  
 **X non** esistono membri pubblici che restituiscono eccezioni come valore restituito o un `out` parametro.  
  
 Restituzione di eccezioni da API pubbliche anziché generare li vanifica molti dei vantaggi di segnalazione degli errori basata sulle eccezioni.  
  
 **✓ PROVARE** utilizzando metodi del generatore di eccezione.  
  
 È comune per la stessa eccezione da diverse posizioni. Per evitare il sovraccarico del codice, utilizzare i metodi di supporto che le eccezioni di creare e inizializzare le relative proprietà.  
  
 Inoltre, non si ricevono i membri che generano eccezioni inline. Spostare l'istruzione throw all'interno del generatore di potrebbe consentire il membro può essere resa inline.  
  
 **X non** generare eccezioni da blocchi di filtro eccezioni.  
  
 Quando un filtro eccezioni genera un'eccezione, l'eccezione viene intercettata da CLR e il filtro restituisce false. Questo comportamento non è distinguibile dal filtro eseguito e viene restituito false in modo esplicito ed è pertanto molto difficile eseguire il debug.  
  
 **X evitare** in modo esplicito la generazione di eccezioni da blocchi finally. Le eccezioni generate in modo implicito risultante dalla chiamata di metodi che generano sono accettabili.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Linee guida di progettazione per le eccezioni](../../../docs/standard/design-guidelines/exceptions.md)