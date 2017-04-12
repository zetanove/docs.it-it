---
title: 'Procedura: eseguire Query sui metadati di un Assembly tramite Reflection (LINQ) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 53caa336-ab83-4181-b0f6-5c87c5f9e4ee
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 7c1bc26d7b23135dd45ad58ea0bd2510b7157448
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-query-an-assembly39s-metadata-with-reflection-linq-visual-basic"></a>Procedura: eseguire Query sui metadati di un Assembly tramite Reflection (LINQ) (Visual Basic)
Nell'esempio seguente viene illustrato come LINQ può essere utilizzato con la reflection per recuperare metadati specifici sui metodi che corrispondono a un criterio di ricerca specificati. In questo caso, la query verranno individuati i nomi di tutti i metodi nell'assembly che restituiscono tipi enumerabili, ad esempio matrici.  
  
## <a name="example"></a>Esempio  
  
```vb  
Imports System.Reflection  
Imports System.IO  
Imports System.Linq  
Module Module1  
  
    Sub Main()  
        Dim asmbly As Assembly =   
            Assembly.Load("System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken= b77a5c561934e089")  
  
        Dim pubTypesQuery = From type In asmbly.GetTypes()   
                            Where type.IsPublic   
                            From method In type.GetMethods()   
                            Where method.ReturnType.IsArray = True   
                            Let name = method.ToString()   
                            Let typeName = type.ToString()   
                            Group name By typeName Into methodNames = Group  
  
        Console.WriteLine("Getting ready to iterate")  
        For Each item In pubTypesQuery  
            Console.WriteLine(item.methodNames)  
  
            For Each type In item.methodNames  
                Console.WriteLine(" " & type)  
            Next  
        Next  
        Console.ReadKey()  
    End Sub  
  
End Module  
```  
  
 Nell'esempio viene utilizzata la <xref:System.Reflection.Assembly.GetTypes%2A>per restituire una matrice di tipi nell'assembly specificato.</xref:System.Reflection.Assembly.GetTypes%2A> Il [clausola Where](../../../../visual-basic/language-reference/queries/where-clause.md) filtro viene applicato in modo che vengano restituiti solo i tipi pubblici. Per ogni tipo pubblico, viene generata una sottoquery utilizzando il <xref:System.Reflection.MethodInfo>matrice restituita dal <xref:System.Type.GetMethods%2A>chiamare.</xref:System.Type.GetMethods%2A> </xref:System.Reflection.MethodInfo> Questi risultati vengono filtrati per restituire solo i metodi il cui tipo restituito è una matrice oppure un tipo che implementa <xref:System.Collections.Generic.IEnumerable%601>.</xref:System.Collections.Generic.IEnumerable%601> Infine, questi risultati vengono raggruppati utilizzando il nome del tipo come chiave.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto destinato a .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e una `Imports` istruzione per lo spazio dei nomi System. Linq.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
