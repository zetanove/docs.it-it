---
title: "const (Riferimenti per C#) | Microsoft Docs"
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
  - "const_CSharpKeyword"
  - "const"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "const (parola chiave) [C#]"
ms.assetid: 79eb447c-117b-4418-933f-97c50aa472db
caps.latest.revision: 28
caps.handback.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# const (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Si usa la parola chiave `const` per dichiarare un campo costante o una variabile locale costante.  I campi e le variabili locali costanti non sono variabili e non sono quindi modificabili.  Gli elementi costanti possono essere numeri, valori booleani, stringhe o un riferimento Null.  Non creare una costante per rappresentare informazioni di cui si prevede la modifica in qualsiasi momento.  Un campo costante, ad esempio, non deve essere usato per archiviare il prezzo di un servizio, il numero di versione di un prodotto o il nome dell'organizzazione di una società.  Tali valori potrebbero cambiare nel tempo e, poiché i compilatori propagano le costanti, eventuale altro codice compilato con quelle librerie dovrebbe essere ricompilato per riflettere le modifiche.  Vedere anche la parola chiave [readonly](../../../csharp/language-reference/keywords/readonly.md).  Ad esempio:  
  
```  
  
      const int x = 0;  
public const double gravitationalConstant = 6.673e-11;  
private const string productName = "Visual C#";  
```  
  
## Note  
 Il tipo di una dichiarazione di costante specifica il tipo di membri introdotti dalla dichiarazione.  L'inizializzatore di una variabile locale costante o di un campo costante deve essere un'espressione costante che possa essere convertita in modo implicito nel tipo di destinazione.  
  
 Un'espressione di costanti è un'espressione che può essere valutata interamente in fase di compilazione.  Di conseguenza, gli unici valori possibili per le costanti dei tipi di riferimento sono `string` e il riferimento Null.  
  
 La dichiarazione di costante può includere più costanti, ad esempio:  
  
```  
public const double x = 1.0, y = 2.0, z = 3.0;  
```  
  
 Il modificatore `static` non è consentito in una dichiarazione di costante.  
  
 Una costante può far parte di un'espressione costante, ad esempio:  
  
```  
public const int c1 = 5;  
public const int c2 = c1 + 100;  
```  
  
> [!NOTE]
>  La parola chiave [readonly](../../../csharp/language-reference/keywords/readonly.md) è diversa dalla parola chiave `const`.  Un campo `const` può essere inizializzato solo nella dichiarazione del campo.  Un campo `readonly` può essere inizializzato nella dichiarazione o in un costruttore.  I campi `readonly` possono quindi presentare valori diversi a seconda del costruttore usato.  Inoltre, mentre un campo `const` rappresenta una costante in fase di compilazione, il campo `readonly` può essere usato per le costanti in fase di esecuzione, come nella riga seguente: `public static readonly uint l1 = (uint)DateTime.Now.Ticks;`  
  
## Esempio  
 [!code-cs[csrefKeywordsModifiers#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/const_1.cs)]  
  
## Esempio  
 In questo esempio viene illustrato come usare le costanti come variabili locali.  
  
 [!code-cs[csrefKeywordsModifiers#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/const_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [readonly](../../../csharp/language-reference/keywords/readonly.md)