---
title: 'Procedura: Eseguire una query per trovare caratteri in una stringa (LINQ) (C#) | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 727a1be7-dbec-4ab8-b414-bc2d56feb6ff
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 537a46e918ad9613f01d0c8997bbdc8589c00dab
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-for-characters-in-a-string-linq-c"></a>Procedura: Eseguire una query per trovare caratteri in una stringa (LINQ) (C#)
Poiché la classe <xref:System.String> implementa l'interfaccia generica <xref:System.Collections.Generic.IEnumerable%601>, è possibile eseguire una query su qualsiasi stringa come una sequenza di caratteri. Tuttavia, questo uso di LINQ non è comune. Per le operazioni con criteri di ricerca complessi, usare la classe <xref:System.Text.RegularExpressions.Regex>.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene eseguita una query su una stringa per determinare il numero di cifre che contiene. Si noti che, dopo la prima esecuzione, la query viene "riutilizzata". Ciò è possibile perché la query stessa non archivia i risultati effettivi.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto che usi .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e alle direttive `using` per gli spazi dei nomi System.Linq e System.IO.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ e stringhe (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)   
 [Procedura: Combinare query LINQ con espressioni regolari (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-combine-linq-queries-with-regular-expressions.md)
