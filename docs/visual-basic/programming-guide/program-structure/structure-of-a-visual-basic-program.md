---
title: "Structure of a Visual Basic Program | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "conditional compilation, Visual Basic"
  - "program structure, Visual Basic"
  - "procedures, structure"
  - "Visual Basic code, program structure"
ms.assetid: ad0c6531-d762-4c77-a700-de16b07b6119
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Structure of a Visual Basic Program
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un programma [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] è composto da blocchi di compilazione standard.  Una *soluzione* comprende uno o più progetti.  Un *progetto* a sua volta può contenere uno o più assembly.  Ogni *assembly* viene compilato da uno o più file di origine.  Un *file di origine* fornisce la definizione e l'implementazione di classi, strutture, moduli e interfacce che indirettamente contengono tutto il codice.  
  
 Per ulteriori informazioni su tali blocchi predefiniti di un programma [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], vedere [Soluzioni e progetti](/visual-studio/ide/solutions-and-projects-in-visual-studio) e [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Elementi di programmazione a livello di file  
 Quando si avvia un progetto o un file e si apre l'editor di codice, viene visualizzata una parte del codice già a posto e nell'ordine corretto.  Qualsiasi codice scritto dovrebbe seguire la sequenza elencata di seguito:  
  
1.  Istruzioni `Option`  
  
2.  Istruzioni `Imports`  
  
3.  Istruzioni `Namespace` ed elementi a livello di spazio dei nomi  
  
 Se si inseriscono le istruzioni in ordine diverso è probabile che si verifichino degli errori di compilazione.  
  
 Inoltre un programma può contenere istruzioni di compilazione condizionali.  È possibile alternare queste istruzioni nel file di origine con le istruzioni della sequenza precedente.  
  
### Istruzioni Option  
 Le istruzioni `Option` stabiliscono le regole di base per il codice successivo, contribuendo ad evitare errori di sintassi e di logica.  L'[Option Explicit Statement](../../../visual-basic/language-reference/statements/option-explicit-statement.md) assicura che tutte le variabili vengano dichiarate e digitate correttamente. In questo modo la durata del debug verrà notevolmente ridotta.  L'[Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md) consente di ridurre al minimo gli errori logici e la perdita di dati che può verificarsi quando si utilizzano variabili di tipi di dati diversi.  L'[Option Compare Statement](../../../visual-basic/language-reference/statements/option-compare-statement.md) consente di specificare il modo in cui le stringhe vengono confrontate tra loro, in base ai loro valori `Binary` o `Text`.  
  
### Istruzioni Imports  
 Per importare i nomi definiti all'esterno del progetto, è possibile includere un'[Imports Statement \(.NET Namespace and Type\)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  Grazie a un'istruzione `Imports` il codice può far riferimento a classi e ad altri tipi definiti all'interno dello spazio dei nomi importato, senza doverne fornire il nome completo.  È possibile utilizzare un numero di istruzioni `Imports` appropriato.  Per ulteriori informazioni, vedere [References and the Imports Statement](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md).  
  
### Istruzioni Namespace  
 Grazie agli spazi dei nomi è possibile organizzare e classificare gli elementi di programmazione per facilitare il raggruppamento e l'accesso.  Utilizzare l'istruzione [Namespace Statement](../../../visual-basic/language-reference/statements/namespace-statement.md) per classificare le istruzioni seguenti all'interno di uno spazio dei nomi particolare.  Per ulteriori informazioni, vedere [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md).  
  
### Istruzioni di compilazione condizionale  
 Le istruzioni di compilazione condizionale possono apparire quasi ovunque nel file di origine.  Provocano l'inclusione o l'esclusione di parti del codice in fase di compilazione in base a certe condizioni.  Inoltre è possibile utilizzarle per il debug dell'applicazione, in quando il codice condizionale viene eseguito solo in modalità di debug.  Per ulteriori informazioni, vedere [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md).  
  
## Elementi di programmazione a livello di spazio dei nomi  
 Classi, strutture e moduli contengono tutti il codice del file di origine.  Si tratta di elementi *a livello di spazio dei nomi* che possono apparire all'interno di uno spazio dei nomi o a livello del file di origine.  Contengono le dichiarazioni di tutti gli altri elementi di programmazione.  Le interfacce che definiscono le firme degli elementi ma non forniscono alcuna implementazione appaiono anch'esse a livello di modulo.  Per ulteriori informazioni sugli elementi a livello di modulo, vedere:  
  
-   [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)  
  
-   [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
-   [Module Statement](../../../visual-basic/language-reference/statements/module-statement.md)  
  
-   [Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 Gli elementi dei dati a livello di spazio dei nomi sono enumerazioni e delegati.  
  
## Elementi di programmazione a livello di modulo  
 Procedure, operatori, proprietà ed eventi sono gli unici elementi di programmazione in grado di contenere codice eseguibile \(istruzioni che effettuano operazioni in fase di esecuzione\).  Si tratta degli elementi del programma *a livello di modulo*.  Per ulteriori informazioni sugli elementi a livello di routine, vedere:  
  
-   [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)  
  
-   [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
-   [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
-   [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
-   [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)  
  
-   [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 Gli elementi dei dati a livello di modulo sono variabili, costanti, enumerazioni e delegati.  
  
## Elementi di programmazione a livello di routine  
 La maggior parte del contenuto degli elementi a *livello di routine* è composta da routine eseguibili che costituiscono il codice di esecuzione del programma.  È necessario che il codice eseguibile sia tutto contenuto in una procedura \(`Function`, `Sub`, `Operator`, `Get`, `Set`, `AddHandler`, `RemoveHandler`, `RaiseEvent`\).  Per ulteriori informazioni, vedere [Statements](../../../visual-basic/programming-guide/language-features/statements.md).  
  
 Gli elementi dei dati a livello di routine sono limitati alle variabili e alle costanti locali.  
  
## Routine Main  
 La routine `Main` è il primo codice ad essere eseguito al caricamento dell'applicazione.  `Main` funge da punto di partenza e controllo generale dell'applicazione.  Di seguito sono riportati i quattro tipi di routine `Main` disponibili.  
  
-   `Sub Main()`  
  
-   `Sub Main(ByVal cmdArgs() As String)`  
  
-   `Function Main() As Integer`  
  
-   `Function Main(ByVal cmdArgs() As String) As Integer`  
  
 Il tipo più comunemente utilizzato è `Sub Main()`.  Per ulteriori informazioni, vedere [Main Procedure in Visual Basic](../../../visual-basic/programming-guide/program-structure/main-procedure.md).  
  
## Vedere anche  
 [NIB: Visual Basic Version of Hello, World](http://msdn.microsoft.com/it-it/9d030b60-e148-4366-a462-69532f02294c)   
 [Main Procedure in Visual Basic](../../../visual-basic/programming-guide/program-structure/main-procedure.md)   
 [Visual Basic Naming Conventions](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [Visual Basic Limitations](../../../visual-basic/programming-guide/program-structure/limitations.md)