---
title: "yield (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "yield"
  - "yield_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "yield (parola chiave) [C#]"
ms.assetid: 1089194f-9e53-46a2-8642-53ccbe9d414d
caps.latest.revision: 46
caps.handback.revision: 46
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# yield (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando si utilizza la parola chiave `yield` in un'istruzione, si indica che il metodo, l'operatore o la funzione di accesso `get` in cui appare è un iteratore.  Utilizzando `yield` per definire un iteratore, si elimina la necessità di una classe esplicita aggiuntiva \(la classe che contiene lo stato per un'enumerazione, vedere <xref:System.Collections.Generic.IEnumerator%601> per un esempio\) quando si implementano i modelli <xref:System.Collections.IEnumerator> e di <xref:System.Collections.IEnumerable> per un tipo di raccolta personalizzato.  
  
 Nell'esempio seguente vengono illustrate le due forme dell'istruzione `yield`.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
## Note  
 Si utilizza un'istruzione `yield return` per restituire un elemento alla volta.  
  
 Si utilizza un metodo iteratore tramite un'istruzione [foreach](../../../csharp/language-reference/keywords/foreach-in.md) o una query LINQ.  Ogni iterazione del ciclo `foreach` chiama il metodo iteratore.  Quando si raggiunge un'istruzione `yield return` nel metodo iteratore, viene restituito `expression` e viene mantenuta la posizione corrente nel codice.  L'esecuzione viene riavviata a partire da quella posizione la volta successiva che viene chiamata la funzione iteratore.  
  
 È possibile utilizzare un'istruzione `yield break` per terminare l'iterazione.  
  
 Per ulteriori informazioni sugli iteratori, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Metodi e funzioni di accesso get dell'iteratore  
 La dichiarazione di un iteratore deve soddisfare i seguenti requisiti:  
  
-   Il tipo restituito deve essere <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator> o <xref:System.Collections.Generic.IEnumerator%601>.  
  
-   La dichiarazione non può avere parametri [ref](../../../csharp/language-reference/keywords/ref.md) o [out](../../../csharp/language-reference/keywords/out.md).  
  
 Il tipo `yield` di un iteratore che restituisce <xref:System.Collections.IEnumerable> o <xref:System.Collections.IEnumerator> è `object`.  Se l'iteratore restituisce <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Collections.Generic.IEnumerator%601>, deve essere presente una conversione implicita dal tipo dell'espressione nell'istruzione `yield return` al parametro di tipo generico.  
  
 Non è possibile includere un'istruzione `yield return` o `yield break` nei metodi che presentano le seguenti caratteristiche:  
  
-   Metodi anonimi.  Per ulteriori informazioni, vedere [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md).  
  
-   Metodi contenenti blocchi unsafe.  Per ulteriori informazioni, vedere [non protette](../../../csharp/language-reference/keywords/unsafe.md).  
  
## Gestione delle eccezioni  
 Un'istruzione `yield return` non può essere inclusa in un blocco try\-catch.  Un'istruzione `yield return` può essere inclusa nel blocco try di un'istruzione try\-finally.  
  
 Un'istruzione `yield break` può essere inclusa in un blocco try o in un blocco catch ma non in un blocco finally.  
  
 Se il corpo di `foreach` \(esterno al metodo iteratore\) genera un'eccezione, viene eseguito un blocco `finally` nel metodo iteratore.  
  
## Implementazione tecnica  
 Il codice seguente restituisce `IEnumerable<string>` da un metodo iteratore e quindi scorre i relativi elementi.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 La chiamata a `MyIteratorMethod` non esegue il corpo del metodo.  La chiamata restituisce invece `IEnumerable<string>` nella variabile `elements`.  
  
 In un'iterazione del ciclo `foreach`, il metodo <xref:System.Collections.IEnumerator.MoveNext%2A> viene chiamato per `elements`.  Questa chiamata esegue il corpo di `MyIteratorMethod` fino a quando non viene raggiunta l'istruzione `yield return` successiva.  L'espressione restituita dall'istruzione `yield return` determina non solo il valore della variabile `element` per l'utilizzo dal corpo del ciclo, ma anche la proprietà <xref:System.Collections.Generic.IEnumerator%601.Current%2A> degli elementi, ovvero `IEnumerable<string>`.  
  
 In ogni iterazione successiva del ciclo `foreach`, l'esecuzione del corpo dell'iteratore continua da dove è stata interrotta, fermandosi ancora quando raggiunge un'istruzione `yield return`.  Il ciclo `foreach` termina quando si raggiunge la fine del metodo iteratore o un'istruzione `yield break`.  
  
## Esempio  
 L'esempio seguente contiene un'istruzione `yield return` all'interno di un ciclo `for`.  Ogni iterazione del corpo dell'istruzione `foreach` in `Process` crea una chiamata alla funzione iteratore `Power`.  Ogni chiamata alla funzione iteratore procede fino alla prossima esecuzione dell'istruzione `yield return`, che si verifica durante l'iterazione successiva del ciclo `for`.  
  
 Il tipo restituito del metodo iteratore è <xref:System.Collections.IEnumerable>, ovvero un tipo di interfaccia iteratore.  Quando il metodo iteratore viene chiamato, restituisce un oggetto enumerabile che contiene le potenze di un numero.  
  
 [!code-cs[csrefKeywordsContextual#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/yield_1.cs)]  
  
## Esempio  
 Nell'esempio seguente viene illustrata una funzione di accesso `get` che è un iteratore.  Nell'esempio, ogni istruzione `yield return` restituisce un'istanza di una classe definita dall'utente.  
  
 [!code-cs[csrefKeywordsContextual#21](../../../csharp/language-reference/keywords/codesnippet/CSharp/yield_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)