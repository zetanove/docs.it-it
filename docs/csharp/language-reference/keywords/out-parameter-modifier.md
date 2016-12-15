---
title: "Modificatore del parametro out (Riferimenti per C#) | Microsoft Docs"
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
  - "out (parametri) [C#]"
  - "parametri [C#], out"
ms.assetid: 3fce0dc5-03f4-4faa-bd61-36c41bc6baf1
caps.latest.revision: 9
caps.handback.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Modificatore del parametro out (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Con la parola chiave `out` gli argomenti vengono passati per riferimento.  È simile alla parola chiave [ref](../../../csharp/language-reference/keywords/ref.md), ad eccezione del fatto che con `ref` è necessario inizializzare la variabile prima che venga passata.  Per utilizzare un parametro `out`, è necessario che la definizione del metodo e il metodo chiamante utilizzino in modo esplicito la parola chiave `out`.  Di seguito è riportato un esempio:  
  
 [!code-cs[csrefKeywordsMethodParams#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-parameter-modifier_1.cs)]  
  
 Anche se le variabili passate come argomenti `out` non devono necessariamente essere già state inizializzate prima di essere passate, il metodo chiamato deve assegnare un valore prima che venga completato.  
  
 Anche se le parole chiave `ref` e `out` provocano un comportamento in fase di esecuzione diverso, non sono considerate parte della firma del metodo in fase di compilazione.  Non è pertanto possibile eseguire l'overload dei metodi se l'unica differenza consiste nel fatto che un metodo accetta un argomento `ref` e l'altro un argomento `out`.  Il codice seguente non viene ad esempio compilato:  
  
 [!code-cs[csrefKeywordsMethodParams#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-parameter-modifier_2.cs)]  
  
 L'overload può essere tuttavia eseguito se un metodo accetta un argomento `ref` o `out` e l'altro non ne utilizza, come riportato di seguito:  
  
 [!code-cs[csrefKeywordsMethodParams#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-parameter-modifier_3.cs)]  
  
 Le proprietà non sono variabili e pertanto non possono essere passate come parametri `out`.  
  
 Per ulteriori informazioni sul passaggio delle matrici, vedere [Passaggio di matrici mediante ref e out](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md).  
  
 Non è possibile utilizzare le parole chiave `out` e `ref` per i seguenti tipi di metodi:  
  
-   Metodi di Asincrona, definite utilizzando il modificatore [async](../../../csharp/language-reference/keywords/async.md).  
  
-   Metodi di iteratore, che includono un'istruzione `yield break` o [prestazioni](../../../csharp/language-reference/keywords/yield.md).  
  
## Esempio  
 La dichiarazione di un metodo `out` risulta utile quando si desidera che un metodo restituisca più valori.  Nell'esempio seguente viene utilizzato `out` per restituire tre variabili con un'unica chiamata al metodo.  Si noti che il terzo argomento è assegnato a null.  In questo modo i metodi possono restituire valori in modo facoltativo.  
  
 [!code-cs[csrefKeywordsMethodParams#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-parameter-modifier_4.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parametri di metodo](../../../csharp/language-reference/keywords/method-parameters.md)