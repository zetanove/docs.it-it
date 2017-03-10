---
title: "Boolean Data Type (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.FALSE"
  - "vb.TRUE"
  - "vb.Boolean"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Boolean data type"
  - "Boolean values, False keyword"
  - "False keyword [Visual Basic]"
  - "True keyword [Visual Basic]"
  - "Boolean values, True keyword"
ms.assetid: 4858e630-4813-4216-a55e-f4d0feb884e4
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Boolean Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Contiene valori che possono essere solo `True` o `False`.  Le parole chiave `True` e `False` corrispondono ai due stati delle variabili `Boolean`.  
  
## Note  
 Utilizzare il [Boolean Data Type \(Visual Basic\)](../../../visual-basic/language-reference/data-types/boolean-data-type.md) per includere valori a due stati, ad esempio true\/false, yes\/no o on\/off.  
  
 Il valore predefinito di `Boolean` è `False`.  
  
 I valori `Boolean` non sono archiviati come numeri e i valori archiviati non vengono considerati equivalenti ai numeri.  Non è consentito scrivere codice basato su valori numerici equivalenti di `True` e `False`.  Se possibile, è opportuno utilizzare le variabili `Boolean` soltanto per i valori logici per cui sono progettate.  
  
## Conversioni di tipi  
 Quando i valori dei tipi di dati numerici vengono convertiti in `Boolean`, 0 diventa `False` e tutti gli altri valori diventano `True`.  Quando i valori `Boolean` vengono convertiti in tipi numerici, `False` diventa 0 e `True` diventa \-1.  
  
 Quando si esegue la conversione tra valori `Boolean` e tipi di dati numerici, tenere presente che i metodi di conversione .NET Framework non producono sempre gli stessi risultati generati dalle parole chiave di conversione Visual Basic.  In Visual Basic, infatti, la conversione mantiene un comportamento compatibile con le versioni precedenti.  Per ulteriori informazioni, vedere la sezione relativa alla mancanza di accuratezza durante la conversione del tipo Boolean nel tipo numerico in [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md).  
  
## Suggerimenti per la programmazione  
  
-   **Numeri negativi.** `Boolean` non è un tipo numerico e non può rappresentare un valore negativo.  In ogni caso, si consiglia di non utilizzare `Boolean` per includere valori numerici.  
  
-   **Caratteri tipo.** `Boolean` non ha alcun carattere di tipo letterale o carattere identificatore di tipo.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.Boolean?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio riportato di seguito `runningVB` è una variabile `Boolean` che memorizza una semplice impostazione sì\/no.  
  
```  
Dim runningVB As Boolean  
' Check to see if program is running on Visual Basic engine.  
If scriptEngine = "VB" Then  
    runningVB = True  
End If  
```  
  
## Vedere anche  
 <xref:System.Boolean?displayProperty=fullName>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Funzione CType](../../../visual-basic/language-reference/functions/ctype-function.md)