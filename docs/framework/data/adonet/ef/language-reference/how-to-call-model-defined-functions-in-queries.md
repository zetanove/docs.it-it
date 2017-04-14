---
title: "Procedura: chiamare funzioni definite dal modello nelle query | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c804e4d-f348-4afd-9f63-d3f0f24bc6a9
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: chiamare funzioni definite dal modello nelle query
In questo argomento viene descritto come chiamare funzioni definite nel modello concettuale dall'interno di query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)].  
  
 La procedura descritta di seguito fornisce una struttura di alto livello per la chiamata di una funzione definita dal modello dall'interno di una query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)].  Nell'esempio che segue vengono forniti dettagli aggiuntivi sui passaggi della procedura.  In questa procedura si presuppone che sia stata definita una funzione nel modello concettuale.  Per altre informazioni, vedere [How to: Define Custom Functions in the Conceptual Model](http://msdn.microsoft.com/it-it/0dad7b8b-58f6-4271-b238-f34810d68e5f).  
  
### Per chiamare una funzione definita nel modello concettuale  
  
1.  Aggiungere un metodo CLR \(Common Language Runtime\) all'applicazione che esegue il mapping alla funzione definita nel modello concettuale.  Per eseguire il mapping del metodo, è necessario applicare un oggetto <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> al metodo.  Si noti che i parametri <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> e <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> dell'attributo sono rispettivamente il nome dello spazio dei nomi del modello concettuale e il nome della funzione nel modello concettuale.  La risoluzione del nome della funzione per LINQ rileva la distinzione tra maiuscole e minuscole.  
  
2.  Chiamare la funzione in una query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)].  
  
## Esempio  
 Nell'esempio seguente viene mostrato come chiamare una funzione definita nel modello concettuale dall'interno di una query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)].  Nell'esempio viene usato il modello School.  Per informazioni sull'esempio del modello School, vedere [Creating the School Sample Database](http://msdn.microsoft.com/it-it/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0) e [Generating the School .edmx File](http://msdn.microsoft.com/it-it/c48b3907-a8be-4fe6-884c-e95af1852758).  
  
 La funzione del modello concettuale seguente restituisce il numero di anni di servizio di un docente.  Per informazioni sull'aggiunta della funzione a un modello concettuale, vedere [How to: Define Custom Functions in the Conceptual Model](http://msdn.microsoft.com/it-it/0dad7b8b-58f6-4271-b238-f34810d68e5f).  
  
 [!code-xml[DP ConceptualModelFunctions#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp conceptualmodelfunctions/xml/school.edmx#1)]
 [!code-xml[DP ConceptualModelFunctions#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/obj/debug/edmxresourcestoembed/school.csdl#1)]  
  
## Esempio  
 Successivamente aggiungere il metodo seguente all'applicazione e usare un oggetto <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> per eseguirne il mapping alla funzione del modello concettuale:  
  
 [!code-csharp[DP ConceptualModelFunctions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/program.cs#2)]
 [!code-vb[DP ConceptualModelFunctions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp conceptualmodelfunctions/vb/module1.vb#2)]  
  
## Esempio  
 A questo punto è possibile chiamare la funzione del modello concettuale dall'interno di una query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)].  Nel codice seguente viene chiamato il metodo per visualizzare tutti i docenti assunti da più di dieci anni:  
  
 [!code-csharp[DP ConceptualModelFunctions#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/program.cs#3)]
 [!code-vb[DP ConceptualModelFunctions#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp conceptualmodelfunctions/vb/module1.vb#3)]  
  
## Vedere anche  
 [.edmx File Overview](http://msdn.microsoft.com/it-it/f4c8e7ce-1db6-417e-9759-15f8b55155d4)   
 [Query in LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)   
 [Chiamata di funzioni nelle query LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md)   
 [Procedura: chiamare funzioni definite dal modello come metodi di oggetto](../../../../../../docs/framework/data/adonet/ef/language-reference/how-to-call-model-defined-functions-as-object-methods.md)