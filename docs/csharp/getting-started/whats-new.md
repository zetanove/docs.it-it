---
title: "What&#39;s New for Visual C# | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
ms.assetid: 9f18dc26-27fa-4603-a639-b573f07a117b
caps.latest.revision: 39
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 39
---
# What&#39;s New for Visual C# #
Questa pagina elenca i nomi delle funzionalità chiave per ogni versione di C\# con le descrizioni delle funzionalità nuove e migliorate nell'ultima versione del linguaggio.  
  
## Versioni precedenti  
 C\#1, Visual Studio .NET 2002  
 Prima versione  
  
 C\#1.1, Visual Studio .NET 2003  
 Pragma `#line` e commenti documento xml  
  
 C\#2, Visual Studio .NET 2005  
 Metodi anonimi, generics, tipi nullable, iteratori\/yield, classi `static`, covarianza\/controvarianza per i delegati  
  
 C\#3, Visual Studio .NET 2008  
 Inizializzatori di oggetto e di insieme, espressioni lambda, metodi di estensione, tipi anonimi, proprietà automatiche, Language Integrated Query \(LINQ\), tipi anonimi, inferenza del tipo `var` locale, LINQ  
  
 C\#4, Visual Studio .NET 2010  
 `Dynamic`, argomenti denominato, parametri facoltativi, covarianza\/controvarianza generica  
  
 C\#5, Visual Studio .NET 2012  
 `Async`\/`await`, attributi delle informazioni sul chiamante  
  
 Visual Studio .NET 2013  
 Correzioni di bug, miglioramenti delle prestazioni e Technology Preview di .NET Compiler Platform \("Roslyn"\)  
  
 C\#6, Visual Studio .NET 2015  
 Versione corrente, vedere di seguito  
  
## Versione corrente  
 [nameof](../../csharp/language-reference/keywords/nameof.md)  
 È possibile ottenere il nome di stringa non qualificato di un tipo o di un membro, da usare in un messaggio di errore senza definire una stringa a livello di codice.  In questo modo il codice sarà corretto anche durante il refactoring.  Questa funzionalità è utile anche per l'associazione di collegamenti MVC \(Modello\-Vista\-Controller\) e la generazione di eventi di modifica di proprietà.  
  
 [Interpolazione di stringhe](../../csharp/language-reference/keywords/interpolated-strings.md)  
 È possibile usare espressioni di interpolazione di stringhe per costruire stringhe.  Un'espressione di stringa interpolata è simile a una stringa di modello che contiene espressioni.  C\# crea una stringa sostituendo le espressioni con le rappresentazioni ToString dei risultati delle espressioni.  In relazione agli argomenti, è più facile comprendere una stringa interpolata che la [Formattazione composita](../Topic/Composite%20Formatting.md).  
  
 [Indicizzazione e accesso ai membri condizionali null](../../csharp/language-reference/operators/null-conditional-operators.md)  
 È possibile verificare la presenza di valori null con una sintassi molto leggera prima di eseguire un'operazione di accesso ai membri \(`?.`\) o di indice \(`?[]`\).  Questi operatori consentono di scrivere meno codice per gestire i controlli null, soprattutto per l'ordinamento decrescente delle strutture di dati.  Se l'operando di sinistra o il riferimento a un oggetto è null, le operazioni restituiscono null.  
  
 [Inizializzatori di indice](../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).  
 È ora possibile inizializzare elementi specifici di un insieme che supporta l'indicizzazione, ad esempio un dizionario.  
  
 [Inizializzatore di insieme e metodi Aggiungi estensione](../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)  
 Ora è possibile usare gli inizializzatori per gli insiemi quando l'insieme dispone di un metodo Aggiungi estensione.  Prima il metodo di aggiunta doveva essere un metodo di istanza.  
  
 **Risoluzione dell'overload**  
 Il compilatore ha migliorato la risoluzione dell'overload che restituisce altro codice funzionando esattamente come previsto.  È probabile che non si verifichino più problemi quando si sceglie tra overload che accettano tipi di valore nullable o quando si passano gruppi di metodi \(invece di espressioni lambda\) a overload che accettano delegati.  
  
 [Filtri eccezioni](../../csharp/language-reference/keywords/try-catch.md)  
 È possibile usare i filtri eccezioni nelle clausole `catch` per determinare se una clausola catch deve gestire l'eccezione.  Senza questa funzionalità, è necessario rigenerare l'eccezione, che taglia lo stack di chiamate segnalato nell'eccezione rigenerata.  
  
 [Await nei blocchi Catch e Finally](../../csharp/language-reference/keywords/try-catch.md)  
 È possibile usare `await` nelle clausole `catch` e `finally`.  
  
 [Inizializzatori di proprietà automatiche](../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)  
 Ora è possibile inizializzare le proprietà automatiche in modo simile a come si inizializzano i campi.  
  
 [Proprietà automatiche solo getter](../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)  
 Ora è possibile definire proprietà automatiche di sola lettura senza doverle definire con una sintassi completa.  È possibile inizializzare la proprietà dove la si dichiara o nel costruttore del tipo.  
  
 **Membri di funzione con corpi di espressione**  
 È possibile dichiarare membri con corpi di espressione di codice nella stessa sintassi leggera usata con le espressioni lambda.  Vedere [Metodi](../../csharp/programming-guide/classes-and-structs/methods.md), [Proprietà](../../csharp/programming-guide/classes-and-structs/properties.md), [Indicizzatori](../../csharp/programming-guide/indexers/index.md) e [Operatori che supportano l'overload](../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md).  
  
 [Uso di elementi statici](../../csharp/language-reference/keywords/using-directive.md)  
 È possibile importare membri statici accessibili di tipi statici in modo da poter fare riferimento ai membri senza qualificare l'accesso con il nome del tipo.  
  
## Vedere anche  
 [Novità di Visual Studio 2015](/visual-studio/ide/what-s-new-in-visual-studio-2015)