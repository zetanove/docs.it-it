---
title: LINQ to Objects (Visual Basic) | Documenti di Microsoft
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
ms.assetid: dd4c30bc-1c9b-4781-a482-b5eada38deb2
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d2bc048fea9affd4998430783d20b978317f3897
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-objects-visual-basic"></a>LINQ to Objects (Visual Basic)
Il termine "LINQ agli oggetti" si riferisce all'utilizzo di LINQ una query con qualsiasi <xref:System.Collections.IEnumerable>o <xref:System.Collections.Generic.IEnumerable%601>raccolta direttamente, senza l'utilizzo di un provider LINQ o un'API come intermedio [LINQ to SQL](https://msdn.microsoft.com/library/bb386976) o [LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13).</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.IEnumerable> È possibile utilizzare LINQ per eseguire query su qualsiasi raccolta enumerabile, ad esempio <xref:System.Collections.Generic.List%601>, <xref:System.Array>, o <xref:System.Collections.Generic.Dictionary%602>.</xref:System.Collections.Generic.Dictionary%602> </xref:System.Array> </xref:System.Collections.Generic.List%601> La raccolta può essere definita dall'utente o può essere restituita da un'API di .NET Framework.  
  
 Concetto di base, LINQ to Objects rappresenta un nuovo approccio alle raccolte. In passato, era necessario scrivere cicli `For Each` complessi che specificavano come recuperare i dati da una raccolta. Nell'approccio LINQ, scrivere codice dichiarativo che descrive ciò che si desidera recuperare.  
  
 Inoltre, le query LINQ offrono tre vantaggi principali rispetto alla tradizionale `For Each` cicli:  
  
1.  Sono più brevi e leggibili, soprattutto quando si filtrano più condizioni.  
  
2.  Forniscono funzioni potenti di filtro, ordinamento e raggruppamento con un codice dell'applicazione minimo.  
  
3.  Possono essere trasferiti in altre origini dati con modifiche minime o nulle.  
  
 In generale, più è complessa l'operazione da eseguire sui dati, maggiore sarà il vantaggio si potrà trarre dall'utilizzo di LINQ rispetto alle tecniche di iterazione tradizionali.  
  
 Lo scopo di questa sezione è illustrato l'approccio LINQ con alcuni esempi specificamente selezionati. Tali informazioni non devono essere ritenute esaustive.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [LINQ e stringhe (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)  
 Viene illustrato come utilizzare LINQ per eseguire query e trasformare stringhe e raccolte di stringhe. Include anche collegamenti ad argomenti che illustrano questi principi.  
  
 [LINQ e Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-reflection.md)  
 Collegamenti a un esempio che illustra come LINQ utilizza la reflection.  
  
 [Directory di File (Visual Basic) e LINQ](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)  
 Viene illustrato come utilizzare LINQ per interagire con i sistemi di file. Include anche collegamenti ad argomenti che illustrano questi concetti.  
  
 [Procedura: eseguire Query su un ArrayList con LINQ (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)  
 Viene illustrato come eseguire query su un oggetto ArrayList in c#.  
  
 [Procedura: aggiungere metodi personalizzati per le query LINQ (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-add-custom-methods-for-linq-queries.md)  
 Viene illustrato come estendere il set di metodi che è possibile utilizzare per le query LINQ aggiungendo metodi di estensione per il <xref:System.Collections.Generic.IEnumerable%601>interfaccia.</xref:System.Collections.Generic.IEnumerable%601>  
  
 [Language-Integrated Query (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/index.md)  
 Vengono forniti collegamenti ad argomenti che illustrano LINQ e vengono forniti esempi di codice che eseguono query.
