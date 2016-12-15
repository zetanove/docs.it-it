---
title: "What&#39;s New for Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "VB.StartPage.WhatsNew"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "new features, Visual Basic"
  - "what's new [Visual Basic]"
  - "Visual Basic, what's new"
ms.assetid: d7e97396-7f42-4873-a81c-4ebcc4b6ca02
caps.latest.revision: 145
caps.handback.revision: 145
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# What&#39;s New for Visual Basic
[!INCLUDE[vs2017banner](../../csharp/includes/vs2017banner.md)]

Questa pagina elenca i nomi delle funzionalità chiave per ogni versione di Visual Basic con le descrizioni delle funzionalità nuove e migliorate nell'ultima versione del linguaggio.  
  
## Versioni precedenti  
 Visual Basic\/Visual Studio .NET 2002  
 Prima versione  
  
 Visual Basic\/Visual Studio .NET 2003  
 Operatori di scorrimento bit, dichiarazione di variabile del ciclo  
  
 Visual Basic\/Visual Studio .NET 2005  
 Tipo `My` e tipi di helper \(accesso all'app, al computer, al file system, alla rete\)  
  
 Visual Basic\/Visual Studio .NET 2008  
 Language Integrated Query \(LINQ\), valori letterali XML, inferenza del tipo di variabile locale, inizializzatori di oggetto, tipi anonimi, metodi di estensione, inferenza del tipo `var` locale, espressioni lambda, operatore `if`, metodi parziali, tipi di valore nullable  
  
 Visual Basic, Visual Studio .NET 2010  
 Proprietà implementate automaticamente, inizializzatori di insieme, continuazione di riga implicita, elementi dinamici, covarianza\/controvarianza generica, accesso agli spazi dei nomi globali  
  
 Visual Basic\/Visual Studio .NET 2012  
 Iteratori `Async`\/`await`, attributi informativi sul chiamante  
  
 Visual Basic\/Visual Studio .NET 2013  
 Technology Preview di .NET Compiler Platform \("Roslyn"\)  
  
 Visual Basic\/Visual Studio .NET 2015  
 Versione corrente, vedere di seguito  
  
## Versione corrente  
 [Nameof](../../csharp/language-reference/keywords/nameof.md)  
 È possibile ottenere il nome di stringa non qualificato di un tipo o di un membro, da usare in un messaggio di errore senza definire una stringa a livello di codice.  In questo modo il codice sarà corretto anche durante il refactoring.  Questa funzionalità è utile anche per l'associazione di collegamenti MVC \(Modello\-Vista\-Controller\) e la generazione di eventi di modifica di proprietà.  
  
 [Interpolazione di stringhe](../../csharp/language-reference/keywords/interpolated-strings.md)  
 È possibile usare espressioni di interpolazione di stringhe per costruire stringhe.  Un'espressione di stringa interpolata è simile a una stringa di modello che contiene espressioni.  C\# crea una stringa sostituendo le espressioni con le rappresentazioni ToString dei risultati delle espressioni.  In relazione agli argomenti, è più facile comprendere una stringa interpolata che la [Formattazione composita](../Topic/Composite%20Formatting.md).  
  
 [Indicizzazione e accesso ai membri condizionali null](../../csharp/language-reference/operators/null-conditional-operators.md)  
 È possibile verificare la presenza di valori null con una sintassi molto leggera prima di eseguire un'operazione di accesso ai membri \(`?.`\) o di indice \(`?[]`\).  Questi operatori consentono di scrivere meno codice per gestire i controlli null, soprattutto per l'ordinamento decrescente delle strutture di dati.  Se l'operando di sinistra o il riferimento a un oggetto è null, le operazioni restituiscono null.  
  
 [Valori letterali multilinea](../../visual-basic/programming-guide/language-features/strings/string-basics.md)  
 I valori letterali stringa possono contenere sequenze di nuove righe.  Non è più necessario usare `<xml><![CDATA[...text with newlines...]]></xml>.Value` come soluzione alternativa.  
  
 Commenti  
 È possibile inserire commenti dopo le continuazioni di riga implicita, all'interno delle espressioni dell'inizializzatore e tra i termini delle espressioni LINQ.  
  
 Risoluzione dei nomi completi più intelligente  
 In precedenza, con un codice come `Threading.Thread.Sleep(1000)`, Visual Basic cercava lo spazio dei nomi "Threading", individuava un'ambiguità tra System.Threading e System.Windows.Threading e quindi segnalava un errore.  Visual Basic ora prende in considerazione entrambi gli spazi dei nomi possibili.  Se si visualizza l'elenco di completamento, l'editor di Visual Studio elenca i membri di entrambi i tipi in questo elenco.  
  
 Valori letterali data con anno all'inizio  
 I valori letterali data possono avere il formato aaaa\-mm\-gg, `#2015-03-17 16:10 PM#`.  
  
 Proprietà dell'interfaccia readonly  
 È possibile implementare proprietà dell'interfaccia readonly usando una proprietà readonly.  L'interfaccia garantisce la funzionalità minima e le classi di implementazione non smettono di consentire l'impostazione della proprietà.  
  
 [TypeOf \<espressione\> IsNot \<tipo\>](../../visual-basic/language-reference/operators/typeof-operator.md)  
 Per una maggiore leggibilità del codice, ora è possibile usare `TypeOf` con `IsNot`.  
  
 [\#Disable Warning \<ID\> e \#Enable Warning \<ID\>](../../visual-basic/language-reference/directives/directives.md)  
 È possibile disabilitare e abilitare avvisi specifici per le aree all'interno di un file di origine.  
  
 Miglioramenti dei commenti ai documenti XML  
 Quando si scrivono commenti ai documenti, si accede a Smart Editor e al supporto per la compilazione per la convalida di nomi di parametro, la corretta gestione di `crefs` \(generics, operatori e così via\), la colorazione e il refactoring.  
  
 [Definizioni di interfacce e moduli parziali](../../visual-basic/language-reference/modifiers/partial.md)  
 Oltre a classi e struct, è possibile dichiarare interfacce e moduli parziali.  
  
 [Direttive \#Region in corpi di metodo](../../visual-basic/language-reference/directives/region-directive.md)  
 È possibile inserire delimitatori \#Region...\#End Region in qualsiasi punto di un file, nelle funzioni o nei corpi delle funzioni.  
  
 [Le definizioni Overrides sono Overloads impliciti](../../visual-basic/language-reference/modifiers/overrides.md)  
 Se si aggiunge il modificatore `Overrides` a una definizione, il compilatore aggiunge in modo implicito `Overloads`. In questo modo è possibile digitare meno codice nella maggior parte dei casi.  
  
 CObj consentito negli argomenti degli attributi  
 Il compilatore generava un errore indicante che CObj\(...\), se usato nelle costruzioni degli attributi, non era una costante.  
  
 Dichiarazione e utilizzo di metodi ambigui da interfacce diverse  
 In precedenza il codice seguente restituiva errori che impedivano di dichiarare `IMock` o di chiamare `GetDetails` \(se questi erano stati dichiarati in c\#\):  
  
```vb  
Interface ICustomer  
  Sub GetDetails(x As Integer)  
End Interface  
  
Interface ITime  
  Sub GetDetails(x As String)  
End Interface  
  
Interface IMock : Inherits ICustomer, ITime  
  Overloads Sub GetDetails(x As Char)  
End Interface  
  
Interface IMock2 : Inherits ICustomer, ITime  
End Interface  
  
```  
  
 Ora il compilatore userà le normali regole di risoluzione dell'overload per scegliere l'oggetto `GetDetails` più appropriato da chiamare ed è possibile dichiarare le relazioni tre le interfacce in Visual Basic, come quelle mostrate nell'esempio.  
  
## Vedere anche  
 [Novità di Visual Studio 2015](/visual-studio/ide/what-s-new-in-visual-studio-2015)