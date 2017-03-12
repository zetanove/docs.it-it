---
title: "GetType Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.GetType"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "GetType operator"
  - "GetType keyword"
ms.assetid: 4f733297-2503-4607-850c-15eba65fff90
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# GetType Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Restituisce un oggetto <xref:System.Type> per il tipo specificato.  L'oggetto <xref:System.Type> fornisce informazioni sul tipo, ad esempio le proprietà, i metodi e gli eventi relativi.  
  
## Sintassi  
  
```  
GetType(typename)  
```  
  
#### Parametri  
  
|||  
|-|-|  
|Parametro|Descrizione|  
|`typename`|Nome del tipo di cui si desidera ottenere informazioni.|  
  
## Note  
 L'operatore `GetType` restituisce l'oggetto <xref:System.Type> per il `typename` specificato.  È possibile passare il nome di qualsiasi tipo definito in `typename`,  I miglioramenti includono quanto segue:  
  
-   Qualsiasi tipo di dati Visual Basic, ad esempio `Boolean` o `Date`.  
  
-   Qualsiasi classe, struttura, interfaccia o modulo .NET Framework, ad esempio <xref:System.ArgumentException?displayProperty=fullName> o <xref:System.Double?displayProperty=fullName>.  
  
-   Qualsiasi classe, struttura, interfaccia o modulo definito dall'applicazione.  
  
-   Qualsiasi matrice definita dall'applicazione.  
  
-   Qualsiasi delegato definito dall'applicazione.  
  
-   Qualsiasi enumerazione definita da Visual Basic, .NET Framework o dall'applicazione.  
  
 Se si desidera ottenere l'oggetto Type di una variabile oggetto, utilizzare il metodo <xref:System.Type.GetType%2A?displayProperty=fullName>.  
  
 L'operatore `GetType` può risultare utile nelle seguenti circostanze:  
  
-   È necessario accedere ai metadati per un tipo in fase di esecuzione.  L'oggetto <xref:System.Type> fornisce metadati quali membri dei tipi e informazioni sulla distribuzione.  Questa necessità si verifica, ad esempio, durante la reflection di un assembly.  Per ulteriori informazioni, vedere <xref:System.Reflection?displayProperty=fullName>.  
  
-   Si desidera confrontare due riferimenti a oggetti per verificare se si riferiscono a istanze dello stesso tipo.  In caso affermativo, `GetType` restituisce riferimenti allo stesso oggetto <xref:System.Type>.  
  
## Esempio  
 Negli esempi riportati di seguito viene illustrato come utilizzare l'operatore `GetType`.  
  
 [!code-vb[VbVbalrOperators#26](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/gettype-operator_1.vb)]  
  
## Vedere anche  
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Operators and Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)