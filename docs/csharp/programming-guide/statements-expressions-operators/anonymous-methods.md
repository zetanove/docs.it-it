---
title: "Metodi anonimi (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "metodi anonimi [C#]"
  - "delegati [C#], metodi anonimi"
  - "metodi [C#], anonimi"
ms.assetid: a62441fa-f0a3-4acb-9aa6-93762a635275
caps.latest.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 31
---
# Metodi anonimi (Guida per programmatori C#)
Nelle versioni di C\# precedenti alla 2.0 era possibile dichiarare un [delegato](../../../csharp/language-reference/keywords/delegate.md) solo tramite [metodi denominati](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md).  In C\# 2.0 sono stati introdotti i metodi anonimi e in C\# 3.0 e versioni successive le espressioni lambda sostituiscono i metodi anonimi come modalità preferita per scrivere il codice in linea.  Le informazioni sui metodi anonimi presenti in questo argomento sono tuttavia valide anche per le espressioni lambda.  Esiste solo un caso in cui un metodo anonimo fornisce funzionalità non presenti nelle espressioni lambda.  I metodi anonimi consentono di omettere l'elenco di parametri.  Questo significa che un metodo anonimo può essere convertito in delegati con diverse firme.  Ciò non è possibile con le espressioni lambda.  Per ulteriori informazioni specifiche sulle espressioni lambda, vedere [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 La creazione di metodi anonimi consente essenzialmente di passare un blocco di codice come parametro del delegato.  Di seguito sono riportati due esempi:  
  
 [!code-cs[csProgGuideDelegates#6](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#6)]  
  
 [!code-cs[csProgGuideDelegates#5](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#5)]  
  
 Utilizzando i metodi anonimi si riduce l'overhead della codifica nella creazione di istanze dei delegati, poiché non è necessario creare un metodo separato.  
  
 La specifica di un blocco di codice al posto di un delegato può risultare utile nelle situazioni in cui la necessità di creare un metodo potrebbe sembrare un overhead inutile,  ad esempio quando viene avviato un nuovo thread.  Questa classe crea un thread e contiene anche il codice eseguito dal thread, senza richiedere la creazione di un metodo aggiuntivo per il delegato.  
  
 [!code-cs[csProgGuideDelegates#7](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#7)]  
  
## Note  
 L'ambito dei parametri di un metodo anonimo è il *blocco di metodi anonimi*.  
  
 È errato inserire nel blocco di metodi anonimi un'istruzione di salto, ad esempio [goto](../../../csharp/language-reference/keywords/goto.md), [break](../../../csharp/language-reference/keywords/break.md) o [continue](../../../csharp/language-reference/keywords/continue.md) se la destinazione è esterna al blocco.  È altresì errato inserire all'esterno del blocco di metodi anonimi un'istruzione di salto, ad esempio `goto`, `break` o `continue`, se la destinazione è interna al blocco.  
  
 Le variabili e i parametri locali il cui ambito contiene una dichiarazione di metodo anonimo sono denominati variabili *esterne* del metodo anonimo.  Nel segmento di codice riportato di seguito, ad esempio, `n` è una variabile esterna:  
  
 [!code-cs[csProgGuideDelegates#8](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#8)]  
  
 Un riferimento alla variabile esterna `n` viene detto  *acquisiti* quando viene creato il delegato.  A differenza delle variabili locali, la durata di una variabile acquisita estende finché i delegati che fanno riferimento i metodi anonimi sono idonei per la procedura di garbage collection.  
  
 Un metodo anonimo non può accedere ai parametri [ref](../../../csharp/language-reference/keywords/ref.md) o [out](../../../csharp/language-reference/keywords/out.md) di un ambito esterno.  
  
 All'interno del *blocco di metodi anonimi* non è possibile accedere a codice unsafe.  
  
 Non è possibile utilizzare metodi anonimi sul lato sinistro dell'operatore [is](../../../csharp/language-reference/keywords/is.md).  
  
## Esempio  
 Nell'esempio seguente vengono illustrati i due modi disponibili per la creazione di un'istanza di un delegato:  
  
-   Associazione del delegato con un metodo anonimo.  
  
-   Associazione del delegato con un metodo denominato \(`DoWork`\).  
  
 In ogni caso quando il delegato viene richiamato verrà visualizzato un messaggio.  
  
 [!code-cs[csProgGuideDelegates#4](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#4)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Delegati con metodi denominati e anonimi](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)