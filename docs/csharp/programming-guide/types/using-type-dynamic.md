---
title: "Utilizzo del tipo dinamico (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "dynamic [C#], informazioni sul tipo dinamico"
  - "tipo dinamico [C#]"
ms.assetid: 3828989d-c967-4a51-b948-857ebc8fdf26
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# Utilizzo del tipo dinamico (Guida per programmatori C#)
In [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp-dev10-long-md.md)] è stato introdotto un nuovo tipo, `dynamic`.  Il tipo è statico, ma un oggetto di tipo `dynamic` ignora il controllo del tipo statico.  Nella maggior parte dei casi, funziona come se disponesse del tipo `object`.  In fase di compilazione, si presume che un elemento tipizzato come `dynamic` supporti qualsiasi operazione.  Non è pertanto importante se l'oggetto ottiene il valore da un'API COM, da un linguaggio dinamico quale IronPython, dal modello DOM \(Document Object Model\) HTML, dalla reflection o da un altro elemento del programma.  Se, tuttavia, il codice non è valido, vengono intercettati errori in fase di esecuzione.  
  
 Se, ad esempio, il metodo di istanza `exampleMethod1` nel codice seguente dispone di un solo parametro, il compilatore riconosce che la prima chiamata al metodo, `ec.exampleMethod1(10, 4)`, non è valida perché contiene due argomenti.  La chiamata genera errori di compilazione.  La seconda chiamata al metodo, `dynamic_ec.exampleMethod1(10, 4)`, non viene controllata dal compilatore poiché il tipo di `dynamic_ec` è `dynamic`.  Non viene, pertanto, segnalato alcun errore del compilatore.  L'errore, tuttavia, non viene ignorato indefinitamente.  Viene intercettato in fase di esecuzione e provoca un'eccezione in fase di esecuzione.  
  
 [!code-cs[CsProgGuideTypes#50](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_1.cs)]  
  
 [!code-cs[CsProgGuideTypes#56](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_2.cs)]  
  
 Il ruolo del compilatore in questi esempi consiste nel raggruppare le informazioni sull'operazione prevista da ciascuna istruzione in relazione all'oggetto o all'espressione tipizzata come `dynamic`.  In fase di esecuzione, le informazioni archiviate vengono esaminate e qualsiasi istruzione non valida provoca un'eccezione in fase di esecuzione.  
  
 Il risultato della maggior parte delle operazioni dinamiche è `dynamic`.  Se, ad esempio, si posiziona il puntatore del mouse sull'utilizzo di `testSum` nell'esempio seguente, IntelliSense visualizza il tipo **\(variabile locale\) dynamic testSum**.  
  
 [!code-cs[CsProgGuideTypes#51](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_3.cs)]  
  
 Le operazioni nelle quali il risultato non è `dynamic` includono le conversioni da `dynamic` a un altro tipo e le chiamate al costruttore che includono argomenti di tipo `dynamic`.  Il tipo di `testInstance`, ad esempio, nella dichiarazione seguente è `ExampleClass`, non `dynamic`.  
  
 [!code-cs[CsProgGuideTypes#52](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_4.cs)]  
  
 Esempi di conversione sono illustrati nella sezione seguente, "Conversioni".  
  
## Conversioni  
 Le conversioni tra oggetti dinamici e altri tipi sono facili.  In questo modo lo sviluppatore può passare dal comportamento dinamico a quello non dinamico e viceversa.  
  
 Un oggetto può essere convertito in tipo dinamico in modo implicito, come illustrato negli esempi seguenti.  
  
 [!code-cs[CsProgGuideTypes#53](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_5.cs)]  
  
 Al contrario, una conversione implicita può essere applicata in modo dinamico a qualsiasi espressione di tipo `dynamic`.  
  
 [!code-cs[CsProgGuideTypes#54](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_6.cs)]  
  
## Risoluzione dell'overload con argomenti di tipo dinamico  
 La risoluzione dell'overload si verifica in fase di esecuzione anziché in fase di compilazione se uno o più argomenti in una chiamata al metodo dispongono del tipo `dynamic` o se il ricevitore della chiamata al metodo è di tipo `dynamic`.  Nell'esempio seguente, se il solo metodo `exampleMethod2` accessibile è definito in modo che accetti un argomento di tipo stringa, l'invio di `d1` come argomento non provoca un errore del compilatore, bensì un'eccezione in fase di esecuzione.  La risoluzione dell'overload non riesce in fase di esecuzione perché il tipo in fase di esecuzione di `d1` è `int` e `exampleMethod2` richiede una stringa.  
  
 [!code-cs[CsProgGuideTypes#55](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_7.cs)]  
  
## Dynamic Language Runtime  
 DLR \(Dynamic Language Runtime\) è una nuova API in [!INCLUDE[net_v40_short](../../../csharp/programming-guide/types/includes/net-v40-short-md.md)].  Fornisce l'infrastruttura che supporta il tipo `dynamic` in C\# oltre all'implementazione di linguaggi di programmazione dinamici, quali IronPython e IronRuby.  Per ulteriori informazioni su DLR, vedere [Dynamic Language Runtime Overview](../Topic/Dynamic%20Language%20Runtime%20Overview.md).  
  
## Interoperabilità COM  
 [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp-dev10-long-md.md)] include diverse funzionalità che migliorano l'interoperabilità con le API COM, ad esempio le API di automazione di Office.  Tra i miglioramenti è compreso l'utilizzo del tipo `dynamic` e di [argomenti denominati e facoltativi](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md).  
  
 Diversi metodi COM consentono la variazione nei tipi di argomento e nel tipo restituito designando i tipi come `object`.  Per questo motivo è necessario il cast esplicito dei valori per la coordinazione con le variabili fortemente tipizzate in C\#.  Se si esegue la compilazione utilizzando l'opzione [\/link \(Link to COM Assembly\)](../../../csharp/language-reference/compiler-options/link-compiler-option.md), l'introduzione del tipo `dynamic` consente di trattare le occorrenze di `object` nelle firme COM come se fossero di tipo `dynamic` e di evitare in tal modo gran parte del cast.  Le istruzioni seguenti sono ad esempio in contrasto con la modalità di accesso a una cella in un foglio di calcolo di Microsoft Office Excel con il tipo `dynamic` e senza il tipo `dynamic`.  
  
 [!code-cs[csOfficeWalkthrough#12](../../../csharp/programming-guide/interop/codesnippet/CSharp/using-type-dynamic_8.cs)]  
  
 [!code-cs[csOfficeWalkthrough#13](../../../csharp/programming-guide/interop/codesnippet/CSharp/using-type-dynamic_9.cs)]  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[dynamic](../../../csharp/language-reference/keywords/dynamic.md)|Viene descritto l'utilizzo della parola chiave `dynamic`.|  
|[Dynamic Language Runtime Overview](../Topic/Dynamic%20Language%20Runtime%20Overview.md)|Viene fornita una panoramica di DLR, un ambiente di runtime che estende Common Language Runtime \(CLR\) con un set di servizi per linguaggi dinamici.|  
|[Procedura dettagliata: creazione e utilizzo di oggetti dinamici](../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)|Fornisce istruzioni dettagliate per la creazione di un oggetto dinamico personalizzato e per la creazione di un progetto che accede a una libreria `IronPython`.|  
|[Procedura: accedere agli oggetti di interoperabilità di Office usando le funzionalità di Visual C\#](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)|Viene illustrato come creare un progetto che utilizza argomenti denominati e facoltativi, il tipo `dynamic` e altri miglioramenti che semplificano l'accesso agli oggetti API di Office.|