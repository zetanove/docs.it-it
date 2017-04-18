---
title: Struttura di un programma Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- conditional compilation, Visual Basic
- program structure, Visual Basic
- procedures, structure
- Visual Basic code, program structure
ms.assetid: ad0c6531-d762-4c77-a700-de16b07b6119
caps.latest.revision: 17
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 64aab045538461d86946c870fa428bf8ad4ec15e
ms.lasthandoff: 03/13/2017

---
# <a name="structure-of-a-visual-basic-program"></a>Struttura di un programma Visual Basic
Oggetto [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] programma è composto da blocchi di compilazione standard. Oggetto *soluzione* comprende uno o più progetti. Oggetto *progetto* a sua volta può contenere uno o più assembly. Ogni *assembly* viene compilato da uno o più file di origine. Oggetto *file di origine* fornisce la definizione e implementazione di classi, strutture, moduli e interfacce che indirettamente contengono tutto il codice.  
  
 Per ulteriori informazioni su questi blocchi predefiniti di un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] del programma, vedere [soluzioni e progetti](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio) e [assembly e Global Assembly Cache](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md).  
  
## <a name="file-level-programming-elements"></a>Elementi di programmazione a livello di file  
 Quando si avvia un progetto o un file e aprire l'editor di codice, viene visualizzato codice già in uso e nell'ordine corretto. Qualsiasi codice scritto deve seguire la sequenza seguente:  
  
1.  `Option`istruzioni  
  
2.  `Imports`istruzioni  
  
3.  `Namespace`istruzioni e gli elementi a livello di spazio dei nomi  
  
 Se si immette istruzioni in un ordine diverso, possono comportare errori di compilazione.  
  
 Un programma può inoltre contenere istruzioni di compilazione condizionale. È possibile alternare queste nel file di origine tra le istruzioni della sequenza precedente.  
  
### <a name="option-statements"></a>Istruzioni Option  
 `Option`le istruzioni stabiliscono le regole di base per il codice successivo, contribuendo ad evitare errori di sintassi e la logica. Il [istruzione Option Explicit](../../../visual-basic/language-reference/statements/option-explicit-statement.md) garantisce che tutte le variabili vengono dichiarate e ortografia, riducendo in fase di debug. Il [istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md) consente di ridurre al minimo la logica degli errori e perdita di dati che può verificarsi quando si utilizzano variabili di tipi di dati diversi. Il [istruzione Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md) specifica le modalità di stringhe vengono confrontate tra loro, in base a una loro `Binary` o `Text` valori.  
  
### <a name="imports-statements"></a>Istruzioni Imports  
 È possibile includere un [istruzione Imports (tipo e Namespace .NET)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) per importare i nomi definiti all'esterno del progetto. Un `Imports` istruzione consente al codice fare riferimento alle classi e altri tipi definiti nello spazio dei nomi importato, senza la necessità di fornire il nome completo. È possibile utilizzare il numero `Imports` istruzioni appropriate. Per ulteriori informazioni, vedere [riferimenti e istruzione Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md).  
  
### <a name="namespace-statements"></a>Istruzioni Namespace  
 Guida di spazi dei nomi organizzare e classificare gli elementi di programmazione per facilitare il raggruppamento e l'accesso. Utilizzare il [istruzione Namespace](../../../visual-basic/language-reference/statements/namespace-statement.md) per classificare le seguenti istruzioni all'interno di un determinato spazio dei nomi. Per ulteriori informazioni, vedere [spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md).  
  
### <a name="conditional-compilation-statements"></a>Istruzioni di compilazione condizionale  
 Istruzioni di compilazione condizionale possono apparire quasi ovunque nel file di origine. Provocano parti del codice per includere o escludere in fase di compilazione in base a determinate condizioni. È possibile anche utilizzarli per il debug dell'applicazione, poiché il codice condizionale viene eseguito solo in modalità debug. Per ulteriori informazioni, vedere [la compilazione condizionale](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md).  
  
## <a name="namespace-level-programming-elements"></a>Elementi di programmazione a livello di Namespace  
 Classi, strutture e i moduli contengono tutto il codice nel file di origine. Sono *a livello di spazio dei nomi* elementi che possono essere visualizzate all'interno di uno spazio dei nomi o a livello di file di origine. Questi file contengono le dichiarazioni di tutti gli altri elementi di programmazione. Interfacce che definiscono le firme degli elementi ma non forniscono alcuna implementazione, vengono visualizzati anche a livello di modulo. Per ulteriori informazioni sugli elementi a livello di modulo, vedere quanto segue:  
  
-   [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)  
  
-   [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
-   [Istruzione Module](../../../visual-basic/language-reference/statements/module-statement.md)  
  
-   [Istruzione Interface](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 Gli elementi di dati a livello di spazio dei nomi sono delegati ed enumerazioni.  
  
## <a name="module-level-programming-elements"></a>Elementi di programmazione a livello di modulo  
 Le procedure, operatori, proprietà ed eventi sono gli unici elementi di programmazione che possono contenere codice eseguibile (istruzioni che eseguono azioni in fase di esecuzione). Sono il *a livello di modulo* elementi del programma. Per ulteriori informazioni sugli elementi di livello di stored procedure, vedere quanto segue:  
  
-   [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
-   [Istruzione Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
-   [Istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
-   [Istruzione Operator](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
-   [Istruzione Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
-   [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 Gli elementi di dati a livello di modulo sono variabili, costanti, enumerazioni e delegati.  
  
## <a name="procedure-level-programming-elements"></a>Elementi di programmazione a livello di routine  
 La maggior parte dei contenuti di *a livello di routine* gli elementi sono eseguibili che costituiscono il codice in fase di esecuzione del programma. Tutto il codice eseguibile deve essere in una procedura (`Function`, `Sub`, `Operator`, `Get`, `Set`, `AddHandler`, `RemoveHandler`, `RaiseEvent`). Per ulteriori informazioni, vedere [istruzioni](../../../visual-basic/programming-guide/language-features/statements.md).  
  
 Gli elementi di dati a livello di routine sono limitati a costanti e variabili locali.  
  
## <a name="the-main-procedure"></a>La procedura principale  
 Il `Main` procedura è la prima parte di codice da eseguire quando l'applicazione è stata caricata. `Main`serve come punto di partenza e controllo generale per l'applicazione. Esistono quattro tipi di `Main`:  
  
-   `Sub Main()`  
  
-   `Sub Main(ByVal cmdArgs() As String)`  
  
-   `Function Main() As Integer`  
  
-   `Function Main(ByVal cmdArgs() As String) As Integer`  
  
 Il più comune di questa procedura è `Sub Main()`. Per ulteriori informazioni, vedere [routine Main in Visual Basic](../../../visual-basic/programming-guide/program-structure/main-procedure.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Routine Main in Visual Basic](../../../visual-basic/programming-guide/program-structure/main-procedure.md)   
 [Convenzioni di denominazione di Visual Basic](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [Limitazioni di Visual Basic](../../../visual-basic/programming-guide/program-structure/limitations.md)
