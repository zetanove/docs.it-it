---
title: 'Procedura: eseguire una Query per i caratteri in una stringa (LINQ) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 499ebbe0-746c-4235-9dba-ce722c12b50e
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: dabd63e52707f3078c6cdc41db8c4f0e7dfbf70e
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-for-characters-in-a-string-linq-visual-basic"></a>Procedura: eseguire una Query per i caratteri in una stringa (LINQ) (Visual Basic)
Poiché la <xref:System.String>classe implementa l'interfaccia generica <xref:System.Collections.Generic.IEnumerable%601>interfaccia, è possibile eseguire query di qualsiasi stringa come una sequenza di caratteri.</xref:System.Collections.Generic.IEnumerable%601> </xref:System.String> Tuttavia, questo non è un utilizzo comune di LINQ. Per le operazioni di criteri di ricerca complessa, utilizzare la <xref:System.Text.RegularExpressions.Regex>classe.</xref:System.Text.RegularExpressions.Regex>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente esegue una query per determinare il numero di cifre che contiene una stringa. Si noti che la query è "riutilizzare" dopo che viene eseguita la prima volta. Ciò è possibile perché la query stessa non è possibile archiviare i risultati effettivi.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto destinato a .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e una `Imports` istruzione per lo spazio dei nomi System. Linq.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ e stringhe (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)   
 [Procedura: combinare query LINQ con espressioni regolari (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-combine-linq-queries-with-regular-expressions.md)
