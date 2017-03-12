---
title: "Funzioni anonime (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "funzioni anonime [C#]"
  - "metodi anonimi [C#]"
  - "espressioni lambda [C#], funzioni anonime"
ms.assetid: 6ce3f04d-0c71-4728-9127-634c7e9a8365
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# Funzioni anonime (Guida per programmatori C#)
Una funzione anonima è un'istruzione o espressione "in linea" che può essere utilizzata con un tipo delegato.  È possibile utilizzarla per inizializzare un delegato denominato o passarla come parametro del metodo invece di un tipo delegato denominato.  
  
 Sono disponibili due tipi di funzioni anonime, illustrati singolarmente negli argomenti seguenti:  
  
-   [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
-   [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)  
  
    > [!NOTE]
    >  Le espressioni lambda possono essere associate alle strutture ad albero dell'espressione nonché ai delegati.  
  
## L'evoluzione dei delegati in C\#  
 In C\# 1.0 l'istanza di un delegato viene creata inizializzandola in modo esplicito con un metodo definito in un altro punto del codice.  In C\# 2.0 viene introdotto il concetto dei metodi anonimi per scrivere blocchi di istruzioni in linea senza nome che possono essere eseguiti in una chiamata del delegato.  In C\# 3.0 vengono introdotte le espressioni lambda, che sono concettualmente analoghe ai metodi anonimi ma più esplicite e concise.  Queste due funzionalità sono conosciute collettivamente come *funzioni anonime*.  In generale, le applicazioni che sono destinate alla versione 3.5 e alle versioni successive di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] devono utilizzare le espressioni lambda.  
  
 Nell'esempio seguente viene illustrata l'evoluzione della creazione del delegato da C\# 1.0 a C\# 3.0:  
  
 [!code-cs[csProgGuideLINQ#65](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#65)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Istruzioni, espressioni e operatori](../../../csharp/programming-guide/statements-expressions-operators/index.md)   
 [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Strutture ad albero dell'espressione](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md)