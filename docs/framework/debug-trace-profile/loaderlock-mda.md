---
title: "loaderLock MDA | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "deadlocks [.NET Framework]"
  - "LoaderLock MDA"
  - "MDAs (managed debugging assistants), loader locks"
  - "managed debugging assistants (MDAs), loader locks"
  - "operating system loader locks"
  - "loader locks"
  - "locks, threads"
ms.assetid: 8c10fa02-1b9c-4be5-ab03-451d943ac1ee
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# loaderLock MDA
L'assistente al debug gestito `loaderLock` rileva i tentativi di esecuzione di codice gestito su un thread contenente il blocco del caricatore del sistema operativo Microsoft Windows.  Questo tipo di esecuzione non è consentita poiché può causare blocchi critici nonché l'utilizzo delle DLL prima che siano state inizializzate dal caricatore del sistema operativo.  
  
## Sintomi  
 Il problema più comune durante l'esecuzione di codice all'interno del blocco del caricatore del sistema operativo riguarda il blocco critico dei thread quando si tenta di chiamare altre funzioni Win32 che richiedono anch'esse il blocco del caricatore.  Esempi di tali funzioni sono `LoadLibrary`, `GetProcAddress`, `FreeLibrary` e `GetModuleHandle`.  È possibile che queste funzioni non vengano chiamate direttamente dall'applicazione ma da Common Language Runtime a seguito di una chiamata di livello superiore come <xref:System.Reflection.Assembly.Load%2A> o della prima chiamata a un metodo di platform invoke.  
  
 I blocchi critici possono verificarsi anche se un thread è in attesa che venga avviato o terminato un altro thread.  Quando si verifica questa condizione, il thread in attesa deve acquisire il blocco del caricatore del sistema operativo per poter inviare gli eventi alle DLL interessate.  
  
 Esistono infine dei casi in cui le chiamate nelle DLL possono verificarsi prima che le DLL siano state inizializzate correttamente dal caricatore del sistema operativo.  A differenza dei blocchi critici, che possono essere diagnosticati esaminando gli stack di tutti i thread coinvolti nel blocco critico, l'utilizzo di DLL non inizializzate è molto difficile da diagnosticare senza ricorrere a questo assistente al debug gestito.  
  
## Causa  
 Gli assembly C\+\+ misti gestiti\/non gestiti compilati per .NET Framework versione 1.0 o 1.1 tentano in genere di eseguire il codice gestito all'interno del blocco del caricatore, a meno che non sia stata prestata particolare attenzione, ad esempio eseguendo il collegamento con l'opzione **\/NOENTRY**.  Per una descrizione dettagliata di questi problemi, vedere l'articolo "Mixed DLL Loading Problem" in MSDN Library \(informazioni in lingua inglese\).  
  
 Gli assembly C\+\+ misti gestiti\/non gestiti compilati per .NET Framework versione 2.0 sono meno soggetti a questo tipo di problemi, avendo lo stesso rischio delle applicazioni che utilizzano DLL non gestite che violano le regole del sistema operativo.  Se, ad esempio, un punto di ingresso `DllMain` di una DLL non gestita chiama `CoCreateInstance` per ottenere un oggetto gestito che è stato esposto a COM, il risultato è il tentativo di eseguire il codice gestito all'interno del blocco del caricatore.  Per ulteriori informazioni sui problemi relativi al blocco del caricatore in .NET Framework versione 2.0 e successive, vedere [Inizializzazione di assembly misti](../Topic/Initialization%20of%20Mixed%20Assemblies.md).  
  
## Risoluzione  
 In Visual C\+\+ .NET 2002 e Visual C\+\+ .NET 2003 le DLL compilate con l'opzione del compilatore `/clr` potevano causare un deadlock in modo non deterministico al momento del caricamento. Questo problema era noto come blocco del caricatore o del caricamento di DLL miste.   In Visual C\+\+ 2005 e versioni successive questo comportamento non deterministico è stato quasi totalmente rimosso dal processo di caricamento di DLL miste.  Esistono infatti alcuni scenari nei quali il blocco del caricatore può ancora verificarsi \(in modo deterministico\).  Per informazioni dettagliate sulle cause e sui tipi di risoluzione per i problemi di blocco del caricatore rimanenti, vedere [Inizializzazione di assembly misti](../Topic/Initialization%20of%20Mixed%20Assemblies.md).  Se nell'argomento non viene identificato il problema di blocco del caricatore riscontrato, esaminare lo stack dei thread per determinare la causa del blocco del caricatore e individuare una possibile soluzione al problema.  Esaminare la traccia dello stack per individuare il thread che ha attivato questo assistente al debug gestito.  Il thread sta tentando di eseguire una chiamata non valida nel codice gestito mantenendo tuttavia il blocco del caricatore del sistema operativo.  Di conseguenza, nello stack sarà probabilmente visibile un punto di ingresso `DllMain` di una DLL o un punto di ingresso equivalente.  Le regole del sistema operativo relative alle operazioni che possono essere eseguite dall'interno di un tale punto di ingresso sono molto restrittive  e impediscono qualsiasi esecuzione gestita.  
  
## Effetto sul runtime  
 In genere si verificherà un blocco critico di alcuni thread all'interno del processo.  Poiché uno di questi thread è probabilmente responsabile dell'esecuzione della Garbage Collection, questo blocco critico può avere un impatto significativo sull'intero processo.  Impedirà inoltre l'esecuzione di eventuali operazioni aggiuntive che richiedono il blocco del caricatore del sistema operativo, ad esempio il caricamento e lo scaricamento degli assembly o delle DLL oppure l'avvio o l'interruzione dei thread.  
  
 In alcuni casi è anche possibile che si verifichino violazioni di accesso o problemi simili nelle DLL chiamate prima della relativa inizializzazione.  
  
## Output  
 Questo assistente al debug gestito indica che è in corso un tentativo di esecuzione gestita non valida.  È necessario esaminare l'analisi dello stack per determinare la causa del blocco del caricatore e individuare una possibile soluzione al problema.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <loaderLock/>  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)