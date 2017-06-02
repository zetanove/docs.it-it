---
title: "Procedura: chiamare funzioni di database personalizzate | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4354e5eb-dd45-469d-97fb-1c495705ee59
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: chiamare funzioni di database personalizzate
In questo argomento viene descritto come chiamare funzioni personalizzate definite nel database dall'interno di query LINQ to Entities.  
  
 Le funzioni di database che sono chiamate dalle query LINQ to Entities vengono eseguite nel database.  L'esecuzione di funzioni nel database può migliorare le prestazioni dell'applicazione.  
  
 La procedura descritta di seguito fornisce una struttura di alto livello per la chiamata di una funzione di database personalizzata.  Nell'esempio che segue vengono forniti dettagli aggiuntivi sui passaggi della procedura.  
  
### Per chiamare funzioni personalizzate definite nel database  
  
1.  Creare una funzione personalizzata nel database.  
  
     Per altre informazioni sulla creazione di funzioni personalizzate in SQL Server, vedere [CREATE FUNCTION \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkID=139871).  
  
2.  Dichiarare una funzione nel linguaggio Store Schema Definition Language \(SSDL\) del file .edmx.  Il nome della funzione deve essere identico a quello della funzione dichiarata nel database.  
  
     Per altre informazioni, vedere [Function Element \(SSDL\)](http://msdn.microsoft.com/it-it/b60cfc3d-8b93-423e-8c99-b867256640a4).  
  
3.  Aggiungere un metodo corrispondente a una classe nel codice dell'applicazione e applicare un <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> al metodo. Si noti che i parametri <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> e <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> dell'attributo sono rispettivamente il nome dello spazio dei nomi del modello concettuale e il nome della funzione nel modello concettuale.  La risoluzione del nome della funzione per LINQ rileva la distinzione tra maiuscole e minuscole.  
  
4.  Chiamare il metodo in una query LINQ to Entities.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come chiamare una funzione di database personalizzata dall'interno una query LINQ to Entities.  Nell'esempio viene usato il modello School.  Per informazioni sull'esempio del modello School, vedere [Creating the School Sample Database](http://msdn.microsoft.com/it-it/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0) e [Generating the School .edmx File](http://msdn.microsoft.com/it-it/c48b3907-a8be-4fe6-884c-e95af1852758).  
  
 Nel codice seguente viene aggiunta la funzione `AvgStudentGrade` al database di esempio School.  
  
> [!NOTE]
>  I passaggi per la chiamata di una funzione di database personalizzata sono gli stessi indipendentemente dal server database.  Tuttavia, il codice seguente è specifico per la creazione di una funzione in un database SQL Server.  Il codice per la creazione di una funzione personalizzata in altri server database potrebbe essere differente.  
  
 [!code-sql[DP L2E MapToDBFunction#1](../../../../../../samples/snippets/tsql/VS_Snippets_Data/dp l2e maptodbfunction/tsql/create_avgstudentgrade.sql#1)]  
  
## Esempio  
 Dichiarare una funzione nel linguaggio Store Schema Definition Language \(SSDL\) del file .edmx.  Nel codice seguente viene dichiarata la funzione `AvgStudentGrade` in SSDL:  
  
 [!code-xml[DP L2E MapToDBFunction#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e maptodbfunction/cs/school.edmx#2)]  
  
## Esempio  
 A questo punto creare un metodo ed eseguirne il mapping alla funzione dichiarata in SSDL.  Il metodo nella classe seguente viene mappato alla funzione definita in SSDL \(sopra\) tramite un oggetto <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>.  Quando il metodo viene chiamato, viene eseguita la funzione corrispondente nel database.  
  
 [!code-csharp[DP L2E MapToDBFunction#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e maptodbfunction/cs/program.cs#3)]
 [!code-vb[DP L2E MapToDBFunction#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e maptodbfunction/vb/module1.vb#3)]  
  
## Esempio  
 Chiamare infine il metodo in una query LINQ to Entities.  Nel codice seguente vengono visualizzati i cognomi di studenti e le medie dei voti alla console:  
  
 [!code-csharp[DP L2E MapToDBFunction#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e maptodbfunction/cs/program.cs#4)]
 [!code-vb[DP L2E MapToDBFunction#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e maptodbfunction/vb/module1.vb#4)]  
  
## Vedere anche  
 [.edmx File Overview](http://msdn.microsoft.com/it-it/f4c8e7ce-1db6-417e-9759-15f8b55155d4)   
 [Query in LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)