---
title: "Passaggio di matrici come argomenti (Guida per programmatori C#) | Microsoft Docs"
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
  - "matrici [C#], passaggio come argomenti"
ms.assetid: f3a0971e-c87c-4a1f-8262-bc0a3b712772
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Passaggio di matrici come argomenti (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Le matrici possono essere passate come argomenti ai parametri di metodo.  Le matrici sono infatti tipi di parametri, pertanto il metodo può modificare il valore degli elementi.  
  
## Passaggio di matrici unidimensionali come parametri  
 È possibile passare una matrice unidimensionale inizializzata a un metodo.  L'istruzione seguente, ad esempio, invia una matrice a un metodo di stampa.  
  
 [!code-cs[csProgGuideArrays#34](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-as-arguments_1.cs)]  
  
 Nel codice seguente viene illustrata un'implementazione parziale del metodo di stampa.  
  
 [!code-cs[csProgGuideArrays#33](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-as-arguments_2.cs)]  
  
 È possibile inizializzare e passare una nuova matrice in un passaggio, come mostrato nell'esempio seguente.  
  
 [!code-cs[CsProgGuideArrays#35](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-as-arguments_3.cs)]  
  
## Esempio  
  
### Descrizione  
 Nell'esempio seguente, una matrice di stringhe viene inizializzata e passata come argomento a un metodo `PrintArray` per le stringhe.  Nel metodo vengono visualizzati gli elementi della matrice.  Vengono quindi chiamati i metodi `ChangeArray` e `ChangeArrayElement` per dimostrare che l'invio di un argomento di matrice per valore non impedisce le modifiche agli elementi della matrice.  
  
### Codice  
 [!code-cs[csProgGuideArrays#30](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-as-arguments_4.cs)]  
  
## Passaggio di matrici multidimensionali come parametri  
 Una matrice multidimensionale inizializzata viene passata a un metodo nello stesso modo di una matrice unidimensionale.  
  
 [!code-cs[csProgGuideArrays#41](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-as-arguments_5.cs)]  
  
 Nel codice seguente viene illustrata una dichiarazione parziale di un metodo di stampa che accetta una matrice bidimensionale come argomento.  
  
 [!code-cs[csProgGuideArrays#36](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-as-arguments_6.cs)]  
  
 È possibile inizializzare e passare una nuova matrice in un passaggio, come mostrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideArrays#32](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-as-arguments_7.cs)]  
  
## Esempio  
  
### Descrizione  
 Nell'esempio seguente, una matrice bidimensionale di Integer viene inizializzata e passata al metodo `Print2DArray`.  Nel metodo vengono visualizzati gli elementi della matrice.  
  
### Codice  
 [!code-cs[csProgGuideArrays#31](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-as-arguments_8.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Matrici unidimensionali](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)   
 [Matrici multidimensionali](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)   
 [Matrici irregolari](../../../csharp/programming-guide/arrays/jagged-arrays.md)