---
title: Tipi di valore e tipi di riferimento | Documenti di Microsoft
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
- reference data types
- reference types
- value types
- value data types
- types [Visual Basic]
- data types [Visual Basic], value types
- data types [Visual Basic], reference types
ms.assetid: fc82ce15-5a40-4c5c-a1e1-a556830e7391
caps.latest.revision: 14
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
ms.openlocfilehash: de8016b4b2a5550b32373a41c89a484fa996c596
ms.lasthandoff: 03/13/2017

---
# <a name="value-types-and-reference-types"></a>Value Types and Reference Types
In Visual Basic, tipi di dati vengono implementati in base alla relativa classificazione. Il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tipi di dati possono essere classificati in base a che una variabile di un determinato tipo archivi i propri dati o un puntatore ai dati. Se archivia i propri dati è un *tipo di valore*; se contiene un puntatore ai dati in un' posizione in memoria è un *tipo di riferimento*.  
  
## <a name="value-types"></a>Tipi valore  
 Un tipo di dati è un *tipo di valore* se contiene i dati nella propria allocazione di memoria. Tipi di valore includono quanto segue:  
  
-   Tutti i tipi di dati numerici  
  
-   `Boolean`, `Char` e `Date`  
  
-   Tutte le strutture, anche se i relativi membri sono tipi di riferimento  
  
-   Le enumerazioni, in quanto il relativo tipo sottostante è sempre `SByte`, `Short`, `Integer`, `Long`, `Byte`, `UShort`, `UInteger`, o`ULong`  
  
 Ogni struttura è un tipo di valore, anche se contiene membri di tipo riferimento. Per questo motivo, i tipi valore, ad esempio `Char` e `Integer` sono implementati da strutture di .NET Framework.  
  
 È possibile dichiarare un tipo di valore utilizzando la parola chiave riservata, ad esempio, `Decimal`. È inoltre possibile utilizzare il `New` (parola chiave) per inizializzare un tipo di valore. Ciò è particolarmente utile se il tipo ha un costruttore che accetta parametri. Un esempio di questo è il <xref:System.Decimal.%23ctor%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Byte%29>costruttore, che crea un nuovo `Decimal` valore dalle parti fornite.</xref:System.Decimal.%23ctor%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Byte%29>  
  
## <a name="reference-types"></a>Tipi di riferimento  
 Oggetto *tipo di riferimento* contiene un puntatore a un'altra posizione di memoria che contiene i dati. Tipi di riferimento includono quanto segue:  
  
-   `String`  
  
-   Tutte le matrici, anche se i relativi elementi sono tipi di valore  
  
-   Tipi di classe, ad esempio<xref:System.Windows.Forms.Form></xref:System.Windows.Forms.Form>  
  
-   Delegati  
  
 Una classe è un *tipo di riferimento*. Per questo motivo, tipi di riferimento, ad esempio `Object` e `String` sono supportati da [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] classi. Si noti che ogni matrice è un tipo di riferimento, anche se i relativi membri sono tipi di valore.  
  
 Poiché ogni tipo di riferimento rappresenta una classe .NET Framework sottostante, è necessario utilizzare il [nuovo operatore](../../../../visual-basic/language-reference/operators/new-operator.md) parola chiave quando si inizializza. L'istruzione seguente consente di inizializzare una matrice.  
  
```  
Dim totals() As Single = New Single(8) {}  
```  
  
## <a name="elements-that-are-not-types"></a>Elementi che non sono tipi  
 I seguenti elementi di programmazione non è qualificano come tipi, perché non è possibile specificare uno di essi come tipo di dati per un elemento dichiarato:  
  
-   Spazi dei nomi  
  
-   Moduli  
  
-   Eventi  
  
-   Le proprietà e procedure  
  
-   Le variabili, costanti e campi  
  
## <a name="working-with-the-object-data-type"></a>Utilizzo del tipo di dati oggetto  
 È possibile assegnare un tipo di riferimento o un tipo di valore a una variabile del `Object` tipo di dati. Un `Object` variabile contiene sempre un puntatore ai dati, mai i dati stessi. Tuttavia, se si assegna un tipo di valore a un `Object` variabile, si comporta come se contenesse i propri dati. Per ulteriori informazioni, vedere [tipo di dati Object](../../../../visual-basic/language-reference/data-types/object-data-type.md).  
  
 È possibile scoprire se un `Object` variabile funge da un tipo di riferimento o un tipo di valore passandola al <xref:Microsoft.VisualBasic.Information.IsReference%2A>metodo la <xref:Microsoft.VisualBasic.Information>classe del <xref:Microsoft.VisualBasic?displayProperty=fullName>dello spazio dei nomi.</xref:Microsoft.VisualBasic?displayProperty=fullName> </xref:Microsoft.VisualBasic.Information> </xref:Microsoft.VisualBasic.Information.IsReference%2A> <xref:Microsoft.VisualBasic.Information.IsReference%2A?displayProperty=fullName>Restituisce `True` se il contenuto di `Object` variabile rappresenta un tipo di riferimento.</xref:Microsoft.VisualBasic.Information.IsReference%2A?displayProperty=fullName>  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di valore nullable](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [Conversioni di tipi in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Istruzione Structure](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Utilizzo efficiente dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [Tipo di dati Object](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
