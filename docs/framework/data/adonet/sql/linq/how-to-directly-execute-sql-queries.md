---
title: "Procedura: eseguire direttamente query SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e491b9bf-741a-4296-9f51-76c25ddf6a82
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: eseguire direttamente query SQL
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] le query create vengono convertite in query SQL con parametri, in formato testo, e inviate al server SQL per l'elaborazione.  
  
 Non è possibile eseguire in SQL la varietà di metodi eventualmente disponibili localmente per l'applicazione,  pertanto [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tenta di convertire questi metodi locali nelle operazioni e funzioni equivalenti disponibili nell'ambiente SQL.  Per la maggior parte dei metodi e degli operatori nei tipi [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] incorporati sono disponibili conversioni dirette in comandi SQL.  Alcuni possono essere prodotti dalle funzioni disponibili.  Quelli che non possono essere prodotti generano eccezioni in fase di esecuzione.  Per altre informazioni, vedere [Mapping di tipi SQL\-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md).  
  
 Nei casi in cui una query [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fosse insufficiente per un'attività specializzata, è possibile usare il metodo <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> per eseguire una query SQL, quindi convertire direttamente il risultato della query in oggetti.  
  
## Esempio  
 Nell'esempio seguente si supponga che i dati per la classe `Customer` siano distribuiti in due tabelle \(customer1 e customer2\).  La query consente di restituire una sequenza di oggetti `Customer`.  
  
 [!code-csharp[DLinqQuerying#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#4)]
 [!code-vb[DLinqQuerying#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#4)]  
  
 A condizione che i nomi di colonna nei risultati tabulari corrispondano alle proprietà di colonna della classe di entità, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] verranno creati oggetti da qualsiasi query SQL.  
  
## Esempio  
 Il metodo <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> accetta anche parametri.  Per eseguire una query con parametri, usare codice analogo al seguente:  
  
 [!code-csharp[DLinqQuerying#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#5)]
 [!code-vb[DLinqQuerying#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#5)]  
  
 I parametri sono espressi nel testo della query usando la stessa notazione con parentesi graffe usata da `Console.WriteLine()` e `String.Format()`.  `String.Format()` viene infatti chiamato nella stringa di query specificata, sostituendo i parametri tra parentesi graffe con nomi di parametro generati, ad esempio @p0, @p1 …, @p\(n\).  
  
## Vedere anche  
 [Informazioni complementari](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)   
 [Esecuzione di query nel database](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)