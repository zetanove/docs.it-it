---
title: "out (Riferimenti per C#) | Microsoft Docs"
ms.date: "2017-03-01"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "out_CSharpKeyword"
  - "out"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "out [C#]"
  - "out (parola chiave) [C#]"
ms.assetid: 7e911a0c-3f98-4536-87be-d539b7536ca8
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# out (Riferimenti per C#)
È possibile usare la parola chiave contestuale `out` in due contesti \(ciascuno dei quali è un collegamento a informazioni dettagliate\), come un [modificatore di parametro](../../../csharp/language-reference/keywords/out-parameter-modifier.md) o in [dichiarazioni di parametri di tipo generico](../../../csharp/language-reference/keywords/out-generic-modifier.md) in interfacce e delegati.  In questo argomento viene descritto il modificatore di parametro, ma è possibile consultare [questo altro argomento](../../../csharp/language-reference/keywords/out-generic-modifier.md) per informazioni sulle dichiarazioni di parametri di tipo generico.  
  
 La parola chiave `out` fa sì che gli argomenti vengono passati per riferimento.  È come per la parola chiave [ref](../../../csharp/language-reference/keywords/ref.md), con la differenza che  richiede l'inizializzazione della variabile prima di essere passato.  Per usare un parametro `out`, la definizione del metodo e il metodo chiamante devono usare in modo esplicito la parola chiave `out`.  Ad esempio:  
  
 [!code-cs[csrefKeywordsMethodParams#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/out_1.cs)]  
  
 Nonostante le variabili passate come `out` non debbano essere inizializzate prima di essere passate, è necessario il metodo chiamato per assegnare un valore prima che il metodo sia restituito.  
  
 Nonostante le parole chiave `ref` e `out` determinino un comportamento differente in fase di esecuzione, non sono considerate parte della firma del metodo in fase di compilazione.  Non è quindi possibile eseguirne l'overload se l'unica differenza è che un metodo accetta un argomento `ref` e l'altro un argomento `out`.  Il codice seguente, ad esempio, non verrà compilato:  
  
 [!code-cs[csrefKeywordsMethodParams#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/out_2.cs)]  
  
 L'overload può essere eseguito, tuttavia, se un metodo accetta un argomento `ref` o `out` e l'altro non ne usa, come segue:  
  
 [!code-cs[csrefKeywordsMethodParams#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/out_3.cs)]  
  
 Le proprietà non sono variabili e quindi non possono essere passate come parametri `out`.  
  
 Per altre informazioni sul passaggio di matrici, vedere [Passaggio di matrici mediante ref e out](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md).  
  
 Non è possibile usare le parole chiave `ref` e `out` per i seguenti tipi di metodi:  
  
-   Metodi Async, definiti usando il modificatore [async](../../../csharp/language-reference/keywords/async.md).  
  
-   Metodi Iterator, che comprendono un'istruzione [yield return](../../../csharp/language-reference/keywords/yield.md) o `yield break`.  
  
## Esempio  
 La dichiarazione di un metodo `out` è utile quando si vuole che un metodo restituisca più valori.  Nell'esempio seguente viene usato `out` per restituire tre variabili con una sola chiamata al metodo.  Notare che il terzo argomento è assegnato a null.  In questo modo i metodi restituiscono i valori facoltativamente.  
  
 [!code-cs[csrefKeywordsMethodParams#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/out_4.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)