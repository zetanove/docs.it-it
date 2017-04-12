---
title: Tipi di dati compositi (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- classes [Visual Basic], composite data types
- composite types
- composite data types
- data types [Visual Basic], composite
- arrays [Visual Basic], composite data types
- structures, composite data types
- classes [Visual Basic], composite types
- types [Visual Basic], composite
ms.assetid: 62970f2e-52c0-4369-8963-613820f1f434
caps.latest.revision: 19
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d81b2c08155cb16754e780fdfb341b596322302d
ms.lasthandoff: 03/13/2017

---
# <a name="composite-data-types-visual-basic"></a>Tipi di dati compositi (Visual Basic)
Oltre ai tipi di dati elementari [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] alimentatori, è possibile unire elementi di tipi diversi per creare *tipi di dati compositi* , ad esempio classi, matrici e strutture. È possibile compilare i tipi di dati composti da tipi di base e da altri tipi composti. Ad esempio, è possibile definire una matrice di elementi di struttura o una struttura con i membri della matrice.  
  
## <a name="data-types"></a>Riepilogo dei tipi di dati  
 Un tipo composito è diverso dal tipo di dati di uno qualsiasi dei relativi componenti. Ad esempio, una matrice di `Integer` elementi non è il `Integer` tipo di dati.  
  
 Dati di tipo matrice sono in genere rappresentato utilizzando il tipo di elemento tra parentesi e virgole in base alle esigenze. Ad esempio, una matrice unidimensionale di `String` elementi viene rappresentata come `String()`e una matrice bidimensionale di `Boolean` elementi viene rappresentata come `Boolean(,)`.  
  
## <a name="structure-types"></a>Tipi di struttura  
 È disponibile alcun tipo di dati singolo che comprende tutte le strutture. Ogni definizione di una struttura rappresenta invece un tipo di dati univoco, anche se due strutture definiscono elementi identici nello stesso ordine. Tuttavia, se si creano due o più istanze della stessa struttura, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tali dello stesso tipo di dati.  
  
## <a name="array-types"></a>Tipi di matrice  
 È disponibile alcun tipo di dati singolo che comprende tutte le matrici. Il tipo di dati di una determinata istanza di una matrice viene determinato nel modo seguente:  
  
-   Il fatto di essere una matrice  
  
-   La classificazione (numero di dimensioni) della matrice  
  
-   Il tipo di elemento della matrice  
  
 In particolare, la lunghezza di una dimensione specificata non fa parte del tipo di dati dell'istanza. Questa condizione è illustrata nell'esempio seguente.  
  
```  
Dim arrayA( ) As Byte = New Byte(12) {}  
Dim arrayB( ) As Byte = New Byte(100) {}  
Dim arrayC( ) As Short = New Short(100) {}  
Dim arrayD( , ) As Short  
Dim arrayE( , ) As Short = New Short(4, 10) {}  
```  
  
 Nell'esempio precedente, le variabili di matrice `arrayA` e `arrayB` vengono considerati dello stesso tipo di dati, ovvero `Byte()` , anche se vengono inizializzate su lunghezze diverse. Variabili `arrayB` e `arrayC` non sono dello stesso tipo perché i relativi tipi di elemento sono diversi. Variabili `arrayC` e `arrayD` non sono dello stesso tipo perché i relativi indici sono differenti. Variabili `arrayD` e `arrayE` hanno lo stesso tipo, ovvero `Short(,)` , perché le classificazioni e i tipi di elemento sono gli stessi, anche se `arrayD` non ancora inizializzato.  
  
 Per ulteriori informazioni sulle matrici, vedere [matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## <a name="class-types"></a>Tipi di classe  
 È disponibile alcun tipo di dati singolo che comprende tutte le classi. Sebbene una classe può ereditare da un'altra classe, ognuno è un tipo di dati separato. Più istanze della stessa classe sono dello stesso tipo di dati. Se si assegna una variabile di istanza di classe a un altro, non solo sono gli stessi dati di tipo, puntano alla stessa istanza di classe in memoria.  
  
 Per ulteriori informazioni sulle classi, vedere [oggetti e classi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Tipi di dati elementari](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Tipi generici in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Tipi di valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Conversioni di tipi in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Strutture](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Risoluzione dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Procedura: Inserire più valori in una variabile](../../../../visual-basic/programming-guide/language-features/data-types/how-to-hold-more-than-one-value-in-a-variable.md)
