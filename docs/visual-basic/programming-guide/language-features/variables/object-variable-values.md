---
title: Valori della variabile (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- object variables, values
- values, of object variables
- data types [Visual Basic], object variable
- variables [Visual Basic], object
ms.assetid: 31555704-58a3-49f1-9a0a-6421f605664f
caps.latest.revision: 18
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: ff219571de9c76802d3f8d3046cf6b6f9d5be9d5
ms.lasthandoff: 03/13/2017

---
# <a name="object-variable-values-visual-basic"></a>Valori di variabili oggetto (Visual Basic)
Una variabile di [tipo di dati Object](../../../../visual-basic/language-reference/data-types/object-data-type.md) può fare riferimento a qualsiasi tipo di dati. Il valore memorizzato in un `Object` variabile viene mantenuta in un' posizione in memoria, mentre la variabile contiene un puntatore ai dati.  
  
## <a name="object-classifier-functions"></a>Funzioni di classificazione di oggetto  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce funzioni che restituiscono informazioni su un `Object` variabile fa riferimento, come illustrato nella tabella seguente.  
  
|Funzione|Restituisce True se la variabile oggetto fa riferimento a|  
|--------------|---------------------------------------------------|  
|<xref:Microsoft.VisualBasic.Information.IsArray%2A></xref:Microsoft.VisualBasic.Information.IsArray%2A>|Matrice di valori, anziché un singolo valore|  
|<xref:Microsoft.VisualBasic.Information.IsDate%2A></xref:Microsoft.VisualBasic.Information.IsDate%2A>|Oggetto [tipo di dati Date](../../../../visual-basic/language-reference/data-types/date-data-type.md) valore o una stringa che può essere interpretata come valore di data e ora|  
|<xref:Microsoft.VisualBasic.Information.IsDBNull%2A></xref:Microsoft.VisualBasic.Information.IsDBNull%2A>|Un oggetto di tipo <xref:System.DBNull>che rappresenta dati mancanti o inesistenti</xref:System.DBNull>|  
|<xref:Microsoft.VisualBasic.Information.IsError%2A></xref:Microsoft.VisualBasic.Information.IsError%2A>|Un oggetto eccezione che deriva da<xref:System.Exception></xref:System.Exception>|  
|<xref:Microsoft.VisualBasic.Information.IsNothing%2A></xref:Microsoft.VisualBasic.Information.IsNothing%2A>|[Nothing](../../../../visual-basic/language-reference/nothing.md), vale a dire, nessun oggetto è attualmente assegnato alla variabile|  
|<xref:Microsoft.VisualBasic.Information.IsNumeric%2A></xref:Microsoft.VisualBasic.Information.IsNumeric%2A>|Un numero o una stringa che può essere interpretata come un numero|  
|<xref:Microsoft.VisualBasic.Information.IsReference%2A></xref:Microsoft.VisualBasic.Information.IsReference%2A>|Un tipo di riferimento (ad esempio una stringa, matrice, delegato o tipo di classe)|  
  
 È possibile utilizzare queste funzioni per evitare l'invio di un valore non valido a un'operazione o una routine.  
  
## <a name="typeof-operator"></a>Operatore TypeOf  
 È inoltre possibile utilizzare il [operatore TypeOf](../../../../visual-basic/language-reference/operators/typeof-operator.md) per determinare se una variabile oggetto fa attualmente riferimento a un tipo di dati specifico. The `TypeOf`... `Is` espressione viene valutata `True` se il tipo in fase di esecuzione dell'operando è derivato da o implementa il tipo specificato.  
  
 Nell'esempio seguente viene utilizzato `TypeOf` su variabili oggetto che fa riferimento ai tipi di riferimento e valore.  
  
```  
' The following statement puts a value type (Integer) in an Object variable.  
Dim num As Object = 10  
' The following statement puts a reference type (Form) in an Object variable.  
Dim frm As Object = New Form()  
If TypeOf num Is Long Then Debug.WriteLine("num is Long")  
If TypeOf num Is Integer Then Debug.WriteLine("num is Integer")  
If TypeOf num Is Short Then Debug.WriteLine("num is Short")  
If TypeOf num Is Object Then Debug.WriteLine("num is Object")  
If TypeOf frm Is Form Then Debug.WriteLine("frm is Form")  
If TypeOf frm Is Label Then Debug.WriteLine("frm is Label")  
If TypeOf frm Is Object Then Debug.WriteLine("frm is Object")  
```  
  
 Nell'esempio precedente scrive le righe seguenti per il **Debug** finestra:  
  
 `num is Integer`  
  
 `num is Object`  
  
 `frm is Form`  
  
 `frm is Object`  
  
 La variabile oggetto `num` fa riferimento a dati di tipo `Integer`, e `frm` fa riferimento a un oggetto della classe <xref:System.Windows.Forms.Form>.</xref:System.Windows.Forms.Form>  
  
## <a name="object-arrays"></a>Matrici di oggetti  
 È possibile dichiarare e utilizzare una matrice di `Object` variabili. Ciò è utile quando è necessario gestire un'ampia gamma di tipi di dati e le classi di oggetti. Tutti gli elementi in una matrice devono avere gli stessi dati dichiarati di tipo. Dichiarazione di questo tipo di dati come `Object` consente di archiviare oggetti e le istanze insieme ad altri tipi di dati nella matrice di classe.  
  
## <a name="see-also"></a>Vedere anche  
 [Variabili oggetto](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Dichiarazione di variabili oggetto](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [Assegnazione di variabili oggetto](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [Procedura: fare riferimento all'istanza corrente di un oggetto](../../../../visual-basic/programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)   
 [Procedura: determinare a quale tipo fa riferimento una variabile oggetto](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-what-type-an-object-variable-refers-to.md)   
 [Procedura: determinare se due oggetti sono correlati](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)   
 [Procedura: determinare se due oggetti sono identici](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)   
 [Tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
