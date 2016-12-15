---
title: "Delegati (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, delegati"
  - "delegati [C#]"
ms.assetid: 97de039b-c76b-4b9c-a27d-8c1e1c8d93da
caps.latest.revision: 30
caps.handback.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Delegati (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

[Delegato](../../../csharp/language-reference/keywords/delegate.md) è un tipo che rappresenta riferimenti ai metodi con un elenco di parametri e un tipo restituito particolari.  Quando si crea un'istanza di un delegato, è possibile associare l'istanza a qualsiasi metodo con una firma compatibile e un tipo restituito.  Tramite l'istanza di delegato è possibile richiamare \(o chiamare\) il metodo.  
  
 I delegati vengono utilizzati per passare metodi come argomenti ad altri metodi.  I gestori di evento non sono altro che metodi richiamati tramite delegati.  Creare un metodo personalizzato e una classe, ad esempio un controllo Windows, che può chiamare tale metodo quando si verifica un determinato evento.  Nell'esempio che segue viene illustrata la dichiarazione di un delegato:  
  
 [!code-cs[csProgGuideDelegates#20](../../../csharp/programming-guide/delegates/codesnippet/CSharp/index_1.cs)]  
  
 Qualsiasi metodo di qualsiasi classe o struct accessibile che corrisponde al tipo di delegato può essere assegnato al delegato.  Il metodo può essere un metodo statico o di istanza.  In questo modo è possibile modificare le chiamate ai metodi a livello di codice, nonché inserire nuovo codice nelle classi esistenti.  
  
> [!NOTE]
>  Nel contesto di overload dei metodi, la firma di un metodo non include il valore restituito,  mentre nel contesto dei delegati, la firma include il valore restituito.  In altre parole, un metodo deve restituire lo stesso tipo del delegato.  
  
 La possibilità di fare riferimento a un metodo come parametro rende i delegati ideali per la definizione di metodi di callback.  È ad esempio possibile passare un riferimento a un metodo per il confronto di due oggetti passati come argomento a un algoritmo di ordinamento.  Poiché il codice di confronto è in una routine separata, l'algoritmo di ordinamento può essere scritto in modo più generale.  
  
## Panoramica dei delegati  
 Di seguito sono riportate le proprietà dei delegati:  
  
-   Sono simili ai puntatori a funzione del linguaggio C\+\+, ma sono indipendenti dai tipi.  
  
-   Consentono di passare metodi come parametri.  
  
-   Possono essere utilizzati per definire metodi di callback.  
  
-   Possono essere concatenati, ad esempio per chiamare più metodi su un singolo evento.  
  
-   Non devono corrispondere necessariamente al tipo del delegato.  Per ulteriori informazioni, vedere [Utilizzo della varianza nei delegati](../Topic/Using%20Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md).  
  
-   In C\# versione 2.0 è stato introdotto il concetto di [metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md), che consentono di passare blocchi di codice come parametri anziché un metodo definito a parte.  In C\# 3.0 sono state introdotte le espressioni lambda per scrivere in modo più conciso i blocchi di codice in linea.  I metodi anonimi e le espressioni lambda vengono compilati, in determinati contesti, in tipi delegati.  Queste funzionalità sono ora note complessivamente come funzioni anonime.  Per ulteriori informazioni sulle espressioni lambda, vedere [Funzioni anonime](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md).  
  
## Argomenti della sezione  
  
-   [Utilizzo di delegati](../../../csharp/programming-guide/delegates/using-delegates.md)  
  
-   [When to Use Delegates Instead of Interfaces \(C\# Programming Guide\)](http://msdn.microsoft.com/it-it/2e759bdf-7ca4-4005-8597-af92edf6d8f0)  
  
-   [Delegati con metodi denominati e anonimi](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)  
  
-   [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)  
  
-   [Utilizzo della varianza nei delegati](../Topic/Using%20Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)  
  
-   [Procedura: combinare delegati multicast](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)  
  
-   [Procedura: dichiarare un delegato, crearne un'istanza e utilizzarlo](../../../csharp/programming-guide/delegates/how-to-declare-instantiate-and-use-a-delegate.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Capitoli del libro rappresentati  
 [Delegates, Events, and Lambda Expressions](http://go.microsoft.com/fwlink/?LinkId=195395) in [C\# 3.0 Cookbook, Third Edition: More than 250 solutions for C\# 3.0 programmers](http://go.microsoft.com/fwlink/?LinkId=195369)  
  
 [Delegates and Events](http://go.microsoft.com/fwlink/?LinkId=195418) in [Learning C\# 3.0: Master the fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)  
  
## Vedere anche  
 <xref:System.Delegate>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)