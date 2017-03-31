---
title: LINQ to Objects (C#) | Microsoft Docs
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
ms.assetid: c5c2c178-3529-4f6c-b3df-2d5267af7f22
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 33402b552672fa79925fd1264444f39b19c02cd9
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-objects-c"></a>LINQ to Objects (C#)
Il termine "LINQ to Objects" si riferisce all'uso diretto di query LINQ con qualsiasi raccolta <xref:System.Collections.IEnumerable> o <xref:System.Collections.Generic.IEnumerable%601>, senza l'uso di un provider LINQ o un'API intermedi, come per [LINQ to SQL](https://msdn.microsoft.com/library/bb386976) o [LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13). È possibile usare LINQ per eseguire query su qualsiasi raccolta enumerabile, ad esempio <xref:System.Collections.Generic.List%601>, <xref:System.Array>, o <xref:System.Collections.Generic.Dictionary%602>. La raccolta può essere definita dall'utente o restituita da un'API di .NET Framework.  
  
 Come concetto di base, LINQ to Objects rappresenta un nuovo approccio alle raccolte. In passato, era necessario scrivere cicli `foreach` complessi che specificavano come recuperare i dati da una raccolta. Con l'approccio LINQ, è possibile scrivere il codice dichiarativo che descrive i dati da recuperare.  
  
 Le query LINQ offrono anche tre vantaggi principali rispetto ai cicli `foreach` tradizionali:  
  
1.  Sono più brevi e leggibili, soprattutto quando si filtrano più condizioni.  
  
2.  Forniscono funzioni potenti di filtro, ordinamento e raggruppamento con un codice dell'applicazione minimo.  
  
3.  Possono essere trasferiti in altre origini dati con modifiche minime o nulle.  
  
 In generale, più è complessa l'operazione da eseguire sui dati, maggiore sarà il vantaggio che si potrà trarre dall'uso di LINQ rispetto alle tecniche di iterazione tradizionali.  
  
 Lo scopo di questa sezione è illustrare l'approccio LINQ con alcuni esempi specificamente selezionati. Tali informazioni non devono essere ritenute esaustive.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [LINQ e stringhe (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)  
 Viene illustrato come usare LINQ per eseguire query e trasformare stringhe e raccolte di stringhe. Include anche collegamenti ad argomenti che illustrano questi principi.  
  
 [LINQ e reflection (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-reflection.md)  
 Collegamenti a un esempio che illustra l'uso di reflection in LINQ.  
  
 [Directory di file e LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-file-directories.md)  
 Viene illustrato come usare LINQ per interagire con i file system. Include anche collegamenti ad argomenti che illustrano questi concetti.  
  
 [Procedura: Eseguire una query su un ArrayList con LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)  
 Viene illustrato come eseguire una query su un oggetto ArrayList in C#.  
  
 [Procedura: Aggiungere metodi personalizzati per le query LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-add-custom-methods-for-linq-queries.md)  
 Viene illustrato come estendere il set di metodi da usare per le query LINQ aggiungendo metodi di estensione per l'interfaccia <xref:System.Collections.Generic.IEnumerable%601>.  
  
 [Language-Integrated Query (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/index.md)  
 Vengono specificati collegamenti ad argomenti che descrivono LINQ e offrono esempi di codice per l'esecuzione di query.
