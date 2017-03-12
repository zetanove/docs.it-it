---
title: "Utilizzo degli spazi dei nomi (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.names"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "nomi completi [C#]"
  - "spazi dei nomi [C#], modalità di utilizzo"
ms.assetid: 1fe8bf39-addc-438a-bd9e-86410e32381d
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# Utilizzo degli spazi dei nomi (Guida per programmatori C#)
Gli spazi dei nomi vengono ampiamente utilizzati all'interno dei programmi C\# in due modi.  In primo luogo, vengono utilizzati in .NET Framework per organizzare le numerose classi disponibili.  In secondo luogo, nei progetti di programmazione di grandi dimensioni la dichiarazione di spazi dei nomi consente di controllare l'ambito dei nomi di classi e metodi.  
  
## Accesso agli spazi dei nomi  
 La maggior parte delle applicazioni C\# inizia con una sezione di direttive `using`.  In questa sezione sono elencati gli spazi dei nomi che verranno utilizzati di frequente dall'applicazione, evitando al programmatore di specificare un nome completo ogni volta che viene utilizzato un metodo incluso in uno di questi spazi.  
  
 Ad esempio, includendo la riga:  
  
 [!code-cs[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/using.cs#1)]  
  
 all'inizio di un programma, il programmatore potrà utilizzare il codice:  
  
 [!code-cs[csProgGuide#31](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/progGuide.cs#31)]  
  
 anziché:  
  
 [!code-cs[csProgGuide#30](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/progGuide.cs#30)]  
  
## Alias degli spazi dei nomi  
 La direttiva [Direttiva using](../../../csharp/language-reference/keywords/using-directive.md) può essere utilizzata anche per creare un alias per uno [spazio dei nomi](../../../csharp/language-reference/keywords/namespace.md).  Se ad esempio si utilizza uno spazio dei nomi scritto in precedenza che contiene spazi dei nomi annidati, è possibile dichiarare un alias per fare riferimento in modo rapido a uno spazio in particolare, come illustrato nell'esempio riportato di seguito:  
  
 [!code-cs[csProgGuideNamespaces#7](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces2.cs#7)]  
  
## Utilizzo degli spazi dei nomi per controllare l'ambito  
 La parola chiave `namespace` viene utilizzata per dichiarare un ambito.  La possibilità di creare ambiti nel progetto consente di organizzare il codice e di creare tipi univoci globali.  Nell'esempio riportato di seguito viene definita una classe denominata `SampleClass` in due spazi dei nomi, l'uno annidato all'interno dell'altro.  Per identificare il metodo che verrà chiamato, viene utilizzato l'[. Operatore](../../../csharp/language-reference/operators/member-access-operator.md).  
  
 [!code-cs[csProgGuideNamespaces#8](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces.cs#8)]  
  
## Nomi completi  
 Gli spazi dei nomi e i tipi hanno nomi univoci, specificati da nomi completi che indicano una gerarchia logica.  Ad esempio, l'istruzione `A.B` implica che `A` è il nome dello spazio dei nomi o tipo e che `B` è annidato al suo interno.  
  
 Nell'esempio riportato di seguito sono inclusi classi e spazi dei nomi annidati.  Il nome completo è indicato come un commento a lato di ogni entità.  
  
 [!code-cs[csProgGuideNamespaces#9](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces.cs#9)]  
  
 Nel segmento di codice precedente:  
  
-   Lo spazio dei nomi `N1` è un membro dello spazio dei nomi globale.  Il relativo nome completo è `N1`.  
  
-   Lo spazio dei nomi `N2` è un membro di `N1`.  Il relativo nome completo è `N1.N2`.  
  
-   La classe `C1` è un membro di `N1`.  Il relativo nome completo è `N1.C1`.  
  
-   Il nome della classe `C2` è utilizzato due volte in questo codice.  Tuttavia, i nomi completi sono univoci.  La prima istanza di `C2` è dichiarata in `C1`; pertanto, il nome completo è `N1.C1.C2`.  La seconda istanza di `C2` è dichiarata in uno spazio dei nomi `N2`; pertanto, il nome completo è `N1.N2.C2`.  
  
 Utilizzando il segmento di codice precedente è possibile aggiungere un nuovo membro della classe, `C3`, allo spazio dei nomi `N1.N2`, come indicato di seguito:  
  
 [!code-cs[csProgGuideNamespaces#10](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces.cs#10)]  
  
 In generale, utilizzare `::` per fare riferimento a un alias di uno spazio dei nomi oppure `global::` per fare riferimento allo spazio dei nomi globale e `.` per qualificare i tipi o i membri.  
  
 È errato utilizzare `::` con un alias che fa riferimento a un tipo anziché a uno spazio dei nomi.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideNamespaces#11](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces2.cs#11)]  
  
 [!code-cs[csProgGuideNamespaces#12](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces2.cs#12)]  
  
 Tenere presente che la parola `global` non è un alias predefinito. Di conseguenza, `global.X` non ha un significato particolare,  ma ne acquisisce uno solo se utilizzato con `::`.  
  
 L'avviso del compilatore CS0440 viene generato se si definisce un alias denominato global, in quanto `global::` fa sempre riferimento allo spazio dei nomi globale e non a un alias.  Il messaggio di avviso viene ad esempio generato dalla seguente riga:  
  
 [!code-cs[csProgGuideNamespaces#13](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces2.cs#13)]  
  
 Con gli alias è consigliabile utilizzare `::`, che fornisce la protezione anche dall'introduzione imprevista di tipi aggiuntivi.  Esaminare l'esempio riportato di seguito:  
  
 [!code-cs[csProgGuideNamespaces#14](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces.cs#14)]  
  
 [!code-cs[csProgGuideNamespaces#15](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces.cs#15)]  
  
 La procedura è valida, ma se in seguito viene aggiunto un tipo denominato `Alias`, `Alias.` verrà associato a tale tipo.  L'utilizzo `Alias::Exception` assicura che `Alias` venga considerato come un alias di uno spazio dei nomi e non erroneamente come un tipo.  
  
 Per ulteriori informazioni sull'alias `global`, vedere [Procedura: utilizzare l'alias dello spazio dei nomi globale](../../../csharp/programming-guide/namespaces/how-to-use-the-global-namespace-alias.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Spazi dei nomi](../../../csharp/programming-guide/namespaces/index.md)   
 [Parole chiave per spazi dei nomi](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [. Operatore](../../../csharp/language-reference/operators/member-access-operator.md)   
 [Operatore ::](../../../csharp/language-reference/operators/namespace-alias-qualifer.md)   
 [extern](../../../csharp/language-reference/keywords/extern.md)