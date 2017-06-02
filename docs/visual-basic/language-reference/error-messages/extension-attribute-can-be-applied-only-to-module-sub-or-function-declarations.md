---
title: "Attributo &quot;Extension&quot; può essere applicato solo alle dichiarazioni &quot;Module&quot;, &quot;Sub&quot; o &quot;Function&quot; | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc36550
- vbc36550
dev_langs:
- VB
helpviewer_keywords:
- BC36550
ms.assetid: 4387a51f-733c-45d7-abdb-eb64d4f51078
caps.latest.revision: 18
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3eee008f737bf625023b6e4d58e1df7d282148d3
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="39extension39-attribute-can-be-applied-only-to-39module39-39sub39-or-39function39-declarations"></a>Attributo 'Extension' può essere applicato solo alle dichiarazioni 'Module', 'Sub' o 'Function'
L'unico modo per estendere un tipo di dati in Visual Basic consiste nel definire un metodo di estensione all'interno di un modulo standard. Il metodo di estensione può essere un `Sub` procedura o una `Function` procedura. Tutti i metodi di estensione devono essere contrassegnati con l'attributo di estensione, `<Extension()>`, dal <xref:System.Runtime.CompilerServices?displayProperty=fullName>dello spazio dei nomi.</xref:System.Runtime.CompilerServices?displayProperty=fullName> Facoltativamente, un modulo che contiene un metodo di estensione può essere contrassegnato nello stesso modo. Nessun altro utilizzo dell'attributo di estensione è valido.  
  
 **ID errore:** BC36550  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Rimuovere l'attributo di estensione.  
  
-   Riprogettare l'estensione di un metodo, definito in un modulo contenitore.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente definisce una `Print` metodo per la `String` tipo di dati.  
  
```  
Imports StringUtility  
Imports System.Runtime.CompilerServices  
Namespace StringUtility  
    <Extension()>   
    Module StringExtensions  
        <Extension()>   
        Public Sub Print (ByVal str As String)  
            Console.WriteLine(str)  
        End Sub  
    End Module  
End Namespace  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sugli attributi](../../../visual-basic/programming-guide/concepts/attributes/index.md)   
 [Metodi di estensione](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)   
 [Istruzione Module](../../../visual-basic/language-reference/statements/module-statement.md)

