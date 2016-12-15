---
title: "Matrici irregolari (Guida per programmatori C#) | Microsoft Docs"
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
  - "matrici [C#], irregolari"
  - "matrici irregolari [C#]"
ms.assetid: 537c65a6-0e0a-4a00-a2b8-086f38519c70
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Matrici irregolari (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Una matrice di matrici è una matrice i cui elementi sono costituiti da matrici.  Gli elementi di una matrice irregolare possono presentare dimensioni e misure differenti.  Una matrice irregolare è anche detta "matrice di matrici". Negli esempi di codice riportati di seguito viene illustrato come dichiarare, inizializzare e accedere alle matrici irregolari.  
  
 Di seguito è riportata la dichiarazione di una matrice unidimensionale di tre elementi, ciascuno dei quali è una matrice unidimensionale di interi:  
  
 [!code-cs[csProgGuideArrays#19](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_1.cs)]  
  
 Per poter utilizzare `jaggedArray`, è necessario che i corrispondenti elementi siano stati inizializzati.  È possibile inizializzare gli elementi nel modo seguente:  
  
 [!code-cs[csProgGuideArrays#20](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_2.cs)]  
  
 Ciascuno degli elementi è costituito da una matrice unidimensionale di interi.  Il primo elemento è una matrice di 5 interi, il secondo una matrice di 4 interi e il terzo una matrice di 2 interi.  
  
 È anche possibile utilizzare inizializzatori per immettere i valori negli elementi delle matrici. In questo caso, non occorre conoscere la dimensione delle matrici.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideArrays#21](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_3.cs)]  
  
 È inoltre possibile inizializzare la matrice al momento della dichiarazione, come nell'esempio che segue:  
  
 [!code-cs[csProgGuideArrays#22](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_4.cs)]  
  
 È possibile utilizzare la seguente forma abbreviata.  Si noti che è possibile omettere l'operatore `new` poiché non è prevista alcuna inizializzazione predefinita per gli elementi:  
  
 [!code-cs[csProgGuideArrays#23](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_5.cs)]  
  
 Gli elementi di una matrice irregolare sono tipi di riferimento inizializzati su `null`.  
  
 È possibile accedere a singoli elementi di una matrice, come negli esempi che seguono:  
  
 [!code-cs[csProgGuideArrays#24](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_6.cs)]  
  
 È possibile combinare matrici irregolari e matrici multidimensionali.  Di seguito sono riportate la dichiarazione e l'inizializzazione di una matrice irregolare unidimensionale che contiene tre elementi matrice bidimensionali con dimensioni diverse.  Per ulteriori informazioni sulle matrici bidimensionali, vedere [Matrici multidimensionali](../../../csharp/programming-guide/arrays/multidimensional-arrays.md).  
  
 [!code-cs[csProgGuideArrays#25](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_7.cs)]  
  
 È possibile accedere a singoli elementi, come illustrato in questo esempio, in cui viene visualizzato il valore dell'elemento `[1,0]` della prima matrice \(valore `5`\):  
  
 [!code-cs[csProgGuideArrays#26](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_8.cs)]  
  
 Il metodo `Length` restituisce il numero di matrici contenute nella matrice irregolare.  Si supponga, ad esempio, che sia stata dichiarata la matrice precedente. In questo caso, la riga  
  
 [!code-cs[csProgGuideArrays#27](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_9.cs)]  
  
 restituisce un valore di 3.  
  
## Esempio  
 In questo esempio viene compilata una matrice i cui elementi sono costituiti da matrici.  Ciascun elemento della matrice ha una dimensione differente.  
  
 [!code-cs[csProgGuideArrays#18](../../../csharp/programming-guide/arrays/codesnippet/CSharp/jagged-arrays_10.cs)]  
  
## Vedere anche  
 <xref:System.Array>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Matrici unidimensionali](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)   
 [Matrici multidimensionali](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)