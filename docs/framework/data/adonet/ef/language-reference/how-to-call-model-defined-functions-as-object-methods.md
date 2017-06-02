---
title: "Procedura: chiamare funzioni definite dal modello come metodi di oggetto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 33bae8a8-4ed8-4a1f-85d1-c62ff288cc61
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: chiamare funzioni definite dal modello come metodi di oggetto
In questo argomento viene descritto come chiamare una funzione definita dal modello come metodo in un oggetto <xref:System.Data.Objects.ObjectContext> oppure come metodo statico di una classe personalizzata.  Una *funzione definita dal modello* è una funzione che è definita nel modello concettuale.  Le procedure descritte in questo argomento mostrano come chiamare queste funzioni direttamente anziché chiamarle da query LINQ to Entities.  Per informazioni sulla chiamata di funzioni definite dal modello tramite query LINQ to Entities, vedere [Procedura: chiamare funzioni definite dal modello nelle query](../../../../../../docs/framework/data/adonet/ef/language-reference/how-to-call-model-defined-functions-in-queries.md).  
  
 Sia che si chiami una funzione definita dal modello come metodo <xref:System.Data.Objects.ObjectContext> o come metodo statico in una classe personalizzata, è necessario innanzitutto eseguire il mapping del metodo alla funzione definita dal modello con un oggetto <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>.  Tuttavia, quando si definisce un metodo nella classe <xref:System.Data.Objects.ObjectContext>, è necessario usare la proprietà <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> per esporre il provider LINQ, mentre quando si definisce un metodo statico in una classe personalizzata, è necessario usare la proprietà <xref:System.Linq.IQueryable.Provider%2A> per esporre il provider LINQ.  Per altre informazioni, vedere gli esempi che seguono le procedure.  
  
 Le procedure descritte di seguito forniscono strutture di alto livello per la chiamata di una funzione definita dal modello come metodo in un oggetto <xref:System.Data.Objects.ObjectContext> e come metodo statico in una classe personalizzata.  Negli esempi che seguono vengono forniti dettagli aggiuntivi sui passaggi delle procedure.  In queste procedure si presuppone che sia stata definita una funzione nel modello concettuale.  Per altre informazioni, vedere [How to: Define Custom Functions in the Conceptual Model](http://msdn.microsoft.com/it-it/0dad7b8b-58f6-4271-b238-f34810d68e5f).  
  
### Per chiamare una funzione definita dal modello come metodo in un oggetto ObjectContext  
  
1.  Aggiungere un file di origine per estendere la classe parziale derivata dalla classe <xref:System.Data.Objects.ObjectContext>, generata automaticamente dagli strumenti di Entity Framework.  La definizione dello stub CLR in un file di origine separato impedirà la perdita delle modifiche durante la rigenerazione del file.  
  
2.  Aggiungere un metodo Common Language Runtime \(CLR\) alla classe <xref:System.Data.Objects.ObjectContext> che:  
  
    -   Esegue il mapping alla funzione definita nel modello concettuale.  Per eseguire il mapping del metodo, è necessario applicare un oggetto <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> al metodo.  Si noti che i parametri <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> e <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> dell'attributo sono rispettivamente il nome dello spazio dei nomi del modello concettuale e il nome della funzione nel modello concettuale.  La risoluzione del nome della funzione per LINQ rileva la distinzione tra maiuscole e minuscole.  
  
    -   Restituisce i risultati del metodo <xref:System.Linq.IQueryProvider.Execute%2A> che viene restituito dalla proprietà <xref:System.Data.Objects.ObjectContext.QueryProvider%2A>.  
  
3.  Chiamare il metodo come membro di un'istanza della classe <xref:System.Data.Objects.ObjectContext>.  
  
### Per chiamare una funzione definita dal modello come metodo statico in una classe personalizzata  
  
1.  Aggiungere una classe all'applicazione con un metodo statico che:  
  
    -   Esegue il mapping alla funzione definita nel modello concettuale.  Per eseguire il mapping del metodo, è necessario applicare un oggetto <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> al metodo.  Si noti che i parametri <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> e <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> dell'attributo sono rispettivamente il nome dello spazio dei nomi del modello concettuale e il nome della funzione nel modello concettuale.  
  
    -   Accetta un argomento <xref:System.Linq.IQueryable>.  
  
    -   Restituisce i risultati del metodo <xref:System.Linq.IQueryProvider.Execute%2A> che viene restituito dalla proprietà <xref:System.Linq.IQueryable.Provider%2A>.  
  
2.  Chiamare il metodo come membro di un metodo statico nella classe personalizzata  
  
## Esempio  
 **Chiamata di una funzione definita dal modello come metodo in un oggetto ObjectContext**  
  
 Nell'esempio seguente viene mostrato come chiamare una funzione definita dal modello come metodo in un oggetto <xref:System.Data.Objects.ObjectContext>.  Nell'esempio viene usato il [Modello Sales di AdventureWorks](http://msdn.microsoft.com/it-it/f16cd988-673f-4376-b034-129ca93c7832).  
  
 Considerare la seguente funzione del modello concettuale che restituisce il ricavo di prodotto per un prodotto specificato.  Per informazioni sull'aggiunta della funzione al modello concettuale, vedere [How to: Define Custom Functions in the Conceptual Model](http://msdn.microsoft.com/it-it/0dad7b8b-58f6-4271-b238-f34810d68e5f).  
  
 <!-- TODO: review snippet reference [!code-xml[DP L2E Methods on ObjectContext#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/obj/x86/debug/edmxresourcestoembed/adventureworks.csdl#4)]  -->
 <!-- TODO: review snippet reference [!code-xml[DP L2E Methods on ObjectContext#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/obj/x86/debug/edmxresourcestoembed/adventureworks.csdl#4)]  -->
 [!code-xml[DP L2E Methods on ObjectContext#4](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#4)]  
  
## Esempio  
 Nel codice seguente viene aggiunto un metodo alla classe `AdventureWorksEntities` che esegue il mapping alla suddetta funzione del modello concettuale.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#2)]
 [!code-vb[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#2)]  
  
## Esempio  
 Nel codice seguente viene chiamato il metodo sopraindicato per visualizzare il ricavo di prodotto per un prodotto specificato:  
  
 [!code-csharp[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#3)]
 [!code-vb[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#3)]  
  
## Esempio  
 Nell'esempio seguente viene mostrato come chiamare una funzione definita dal modello che restituisce una raccolta \(come un oggetto <xref:System.Linq.IQueryable%601>\).  Considerare la seguente funzione del modello concettuale che restituisce tutti i `SalesOrderDetails` per un dato ID di prodotto.  
  
 [!code-xml[DP L2E Methods on ObjectContext#7](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#7)]  
  
## Esempio  
 Nel codice seguente viene aggiunto un metodo alla classe `AdventureWorksEntities` che esegue il mapping alla suddetta funzione del modello concettuale.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#8)]
 [!code-vb[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#8)]  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene chiamato il metodo.  Si noti che la query <xref:System.Linq.IQueryable%601> restituita è ridefinita ulteriormente in modo da restituire i totali delle righe per ogni `SalesOrderDetail`.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#9)]
 [!code-vb[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#9)]  
  
## Esempio  
 **Chiamata di una funzione definita dal modello come metodo statico in una classe personalizzata**  
  
 Nell'esempio seguente viene dimostrato come chiamare una funzione definita dal modello come metodo statico in una classe personalizzata.  Nell'esempio viene usato il [Modello Sales di AdventureWorks](http://msdn.microsoft.com/it-it/f16cd988-673f-4376-b034-129ca93c7832).  
  
> [!NOTE]
>  Quando si chiama una funzione definita dal modello come metodo statico in una classe personalizzata, la funzione definita dal modello deve accettare una raccolta e restituire un'aggregazione di valori nella raccolta.  
  
 Considerare la seguente funzione del modello concettuale che restituisce il ricavo di prodotto per una raccolta SalesOrderDetail.  Per informazioni sull'aggiunta della funzione al modello concettuale, vedere [How to: Define Custom Functions in the Conceptual Model](http://msdn.microsoft.com/it-it/0dad7b8b-58f6-4271-b238-f34810d68e5f).  
  
 <!-- TODO: review snippet reference [!code-xml[DP L2E Methods on ObjectContext#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/obj/x86/debug/edmxresourcestoembed/adventureworks.csdl#1)]  -->
 <!-- TODO: review snippet reference [!code-xml[DP L2E Methods on ObjectContext#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/obj/x86/debug/edmxresourcestoembed/adventureworks.csdl#1)]  -->
 [!code-xml[DP L2E Methods on ObjectContext#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#1)]  
  
## Esempio  
 Nel codice seguente viene aggiunta una classe all'applicazione contenente un metodo statico che esegue il mapping alla suddetta funzione del modello concettuale.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#5)]
 [!code-vb[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#5)]  
  
## Esempio  
 Nel codice seguente viene chiamato il metodo sopraindicato per visualizzare il ricavo di prodotto per una raccolta SalesOrderDetail:  
  
 [!code-csharp[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#6)]
 [!code-vb[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#6)]  
  
## Vedere anche  
 [.edmx File Overview](http://msdn.microsoft.com/it-it/f4c8e7ce-1db6-417e-9759-15f8b55155d4)   
 [Query in LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)   
 [Chiamata di funzioni nelle query LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md)