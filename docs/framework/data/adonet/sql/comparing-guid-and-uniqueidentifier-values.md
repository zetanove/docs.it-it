---
title: "Confronto di valori GUID e uniqueidentifier (ADO.NET) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Confronto di valori GUID e uniqueidentifier (ADO.NET)
Il tipo di dati identificatore univoco globale \(GUID, Globally Unique IDentifier\) in SQL Server è rappresentato dal tipo di dati `uniqueidentifier`, il quale archivia un valore binario di 16 byte.  Un GUID è un numero binario usato principalmente come identificatore univoco in una rete di più computer su più siti.  I GUID possono essere generati chiamando la funzione NEWID Transact\-SQL e sono assolutamente univoci.  Per altre informazioni, vedere "Utilizzo del tipo di dati uniqueidentifier" nella documentazione online di SQL Server.  
  
## Uso di valori SqlGuid  
 I valori GUID sono lunghi e poco chiari, di conseguenza il significato per l'utente resta vago.  Se si usano GUID generati in modo casuale per valori chiave e se si inserisce un numero elevato di righe, si otterranno I\/O casuali negli indici che potrebbero compromettere le prestazioni.  I GUID, inoltre, sono di dimensioni relativamente grandi rispetto ad altri tipi di dati.  In generale, si consiglia di usare i GUID solo per scenari molto ristretti per i quali non è adatto alcun altro tipo di dati.  
  
### Confronto di valori GUID  
 Con i valori `uniqueidentifier` è possibile usare operatori di confronto.  Tuttavia, l'ordinamento non viene implementato confrontando gli schemi di bit dei due valori.  Le uniche operazioni consentite su un valore `uniqueidentifier` sono i confronti \(\=, \<\>, \<, \>, \<\=, \>\=\) e la ricerca di NULL \(IS NULL e IS NOT NULL\).  Non è consentito alcun altro operatore aritmetico.  
  
 Sia il tipo <xref:System.Guid> che il tipo <xref:System.Data.SqlTypes.SqlGuid> dispongono di un metodo `CompareTo` per confrontare valori GUID diversi.  Tuttavia, `System.Guid.CompareTo` e `SqlTypes.SqlGuid.CompareTo` sono implementati in modo diverso.  <xref:System.Data.SqlTypes.SqlGuid> implementa `CompareTo` usando il comportamento di SQL Server in cui gli ultimi sei byte di un valore sono i più importanti.  <xref:System.Guid> valuta tutti i 16 byte.  Nell'esempio seguente è illustrata questa differenza di comportamento.  La prima sezione del codice visualizza valori <xref:System.Guid> non ordinati, mentre la seconda sezione mostra i valori <xref:System.Guid> ordinati.  La terza sezione visualizza i valori <xref:System.Data.SqlTypes.SqlGuid> ordinati.  L'output viene visualizzato sotto il listato di codice.  
  
 [!code-csharp[DataWorks SqlTypes.Guid#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.Guid/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.Guid#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.Guid/VB/source.vb#1)]  
  
 I risultati ottenuti dall'esempio sono seguenti.  
  
```  
Unsorted Guids:  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
  
Sorted Guids:  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
  
Sorted SqlGuids:  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
```  
  
## Vedere anche  
 [Tipi di dati SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)