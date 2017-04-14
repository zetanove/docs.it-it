---
title: "Metodi generici Field e SetField (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1883365f-9d6c-4ccb-9187-df309f47706d
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Metodi generici Field e SetField (LINQ to DataSet)
In [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] sono disponibili metodi di estensione della classe <xref:System.Data.DataRow> per l'accesso ai valori di colonna: il metodo <xref:System.Data.DataRowExtensions.Field%2A> e il metodo <xref:System.Data.DataRowExtensions.SetField%2A>. Questi metodi semplificano l'accesso ai valori di colonna per gli sviluppatori, in particolare per quanto riguarda i valori Null. <xref:System.Data.DataSet> utilizza <xref:System.DBNull.Value> per rappresentare valori Null, mentre [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] utilizza il supporto dei tipi che ammettono i valori Null introdotto in [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)].  L'utilizzo della funzione di accesso della colonna preesistente in <xref:System.Data.DataRow> richiede di eseguire il cast dell'oggetto restituito nel tipo appropriato.  Se un determinato campo di <xref:System.Data.DataRow>può essere Null, è necessario verificare in modo esplicito la presenta di un valore Null, perché se viene restituito <xref:System.DBNull.Value> e ne viene eseguito il cast in modo implicito in un altro tipo, verrà generata un'eccezione <xref:System.InvalidCastException>.  Nell'esempio seguente, se non viene usato il metodo <xref:System.Data.DataRow.IsNull%2A> per verificare la presenza di un valore Null, verrà generata un'eccezione nel caso l'indicizzatore restituisca <xref:System.DBNull.Value> e tenti di eseguirne il cast in <xref:System.String>.  
  
 [!code-csharp[DP LINQ to DataSet Examples#WhereIsNull](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#whereisnull)]
 [!code-vb[DP LINQ to DataSet Examples#WhereIsNull](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#whereisnull)]  
  
 Il metodo <xref:System.Data.DataRowExtensions.Field%2A> fornisce l'accesso ai valori di colonna di <xref:System.Data.DataRow> e <xref:System.Data.DataRowExtensions.SetField%2A> imposta i valori di colonna in <xref:System.Data.DataRow>.  Poiché i metodi <xref:System.Data.DataRowExtensions.Field%2A> e <xref:System.Data.DataRowExtensions.SetField%2A> gestiscono tipi nullable, non è necessario verificare in modo esplicito la presenza di valori Null, a differenza dell'esempio precedente.  Entrambi metodi sono inoltre generici, quindi non è necessario eseguire i cast del tipo restituito.  
  
 Nell'esempio seguente viene usato il metodo <xref:System.Data.DataRowExtensions.Field%2A>:  
  
 [!code-csharp[DP LINQ to DataSet Examples#Where3](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#where3)]
 [!code-vb[DP LINQ to DataSet Examples#Where3](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#where3)]  
  
 Si noti che il tipo di dati specificato nel parametro `T` generico del metodo <xref:System.Data.DataRowExtensions.Field%2A> e del metodo <xref:System.Data.DataRowExtensions.SetField%2A> deve corrispondere al tipo del valore sottostante.  In caso contrario, verrà generata un'eccezione <xref:System.InvalidCastException>.  Il nome di colonna specificato deve inoltre corrispondere al nome di una colonna presente in <xref:System.Data.DataSet>; in caso contrario, verrà generata un'eccezione <xref:System.ArgumentException>.  In entrambi casi, l'eccezione viene generata in fase di esecuzione durante l'enumerazione dei dati quando viene eseguita la query.  
  
 Il metodo <xref:System.Data.DataRowExtensions.SetField%2A> non esegue alcun tipo di conversione.  Tuttavia, ciò non significa che non verrà eseguita una conversione del tipo.  Il metodo <xref:System.Data.DataRowExtensions.SetField%2A> espone il comportamento [!INCLUDE[ado_whidbey_long](../../../../includes/ado-whidbey-long-md.md)] della classe <xref:System.Data.DataRow>.  È possibile eseguire una conversione del tipo tramite l'oggetto <xref:System.Data.DataRow> e salvare quindi il valore convertito nell'oggetto <xref:System.Data.DataRow>.  
  
## Vedere anche  
 <xref:System.Data.DataRowExtensions>