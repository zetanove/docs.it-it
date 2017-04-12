---
title: "Tipo &quot;&lt;typename&gt;&quot; non è definito | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30002
- bc30002
dev_langs:
- VB
helpviewer_keywords:
- BC30002
ms.assetid: b0faf204-57fd-44de-8c05-9db027eea663
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 09aa7c535fd5e17ddcd0e743fb5ec17ebadd4f7d
ms.lasthandoff: 03/13/2017

---
# <a name="type-39lttypenamegt39-is-not-defined"></a>Tipo '&lt;typename&gt;' non è definito
L'istruzione ha fatto riferimento a un tipo che non è stato definito. È possibile definire un tipo in un'istruzione di dichiarazione, ad esempio `Enum`, `Structure`, `Class`, o `Interface`.  
  
 **ID errore:** BC30002  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Assicurarsi che la definizione del tipo e il relativo riferimento utilizzano la stessa ortografia.  
  
-   Assicurarsi che la definizione del tipo sia accessibile al riferimento. Ad esempio, se il tipo è un altro modulo ed è stato dichiarato `Private`, spostare la definizione del tipo di modulo di riferimento o dichiararla `Public`.  
  
-   Verificare che lo spazio dei nomi del tipo non sia ridefinito all'interno del progetto. In tal caso, utilizzare il `Global` parola chiave per il nome tipo completo. Ad esempio, se un progetto definisce uno spazio dei nomi denominato `System`, <xref:System.Object?displayProperty=fullName>tipo non è possibile accedere a meno che non è completo, con la `Global` (parola chiave): `Global.System.Object`.</xref:System.Object?displayProperty=fullName>  
  
-   Se il tipo è definito, ma non è registrata la libreria di oggetto o una libreria dei tipi in cui è definito [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], fare clic su **Aggiungi riferimento** sul **progetto** dal menu e quindi selezionare la libreria di oggetto appropriato o una libreria dei tipi.  
  
-   Verificare che il tipo in un assembly che fa parte del profilo di .NET Framework di destinazione. Per ulteriori informazioni, vedere [risoluzione dei problemi di destinazione .NET Framework](https://docs.microsoft.com/visualstudio/msbuild/troubleshooting-dotnet-framework-targeting-errors).  
  
## <a name="see-also"></a>Vedere anche  
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [Istruzione Enum](../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Istruzione Interface](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Gestione dei riferimenti in un progetto](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)
