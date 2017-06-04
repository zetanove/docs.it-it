---
title: "Procedura: visualizzare SQL generato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 626492c0-5ee3-4675-88e8-8c40379510b6
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: visualizzare SQL generato
È possibile visualizzare il codice SQL generato per le query e modificare l'elaborazione usando la proprietà <xref:System.Data.Linq.DataContext.Log%2A>.  Questo approccio può essere utile per comprendere la funzionalità di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] e per eseguire il debug di problemi specifici.  
  
## Esempio  
 Nell'esempio riportato di seguito viene usata la proprietà <xref:System.Data.Linq.DataContext.Log%2A> per visualizzare il codice SQL nella finestra della console prima di eseguirlo.  È possibile usare questa proprietà con comandi di query, inserimento, aggiornamento ed eliminazione.  
  
 Le righe nella finestra della console sono le stesse che vengono visualizzate quando si esegue il codice [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] o C\# seguente.  
  
```  
SELECT [t0].[CustomerID], [t0].[CompanyName], [t0].[ContactName], [t0].[ContactT  
itle], [t0].[Address], [t0].[City], [t0].[Region], [t0].[PostalCode], [t0].[Coun  
try], [t0].[Phone], [t0].[Fax]  
FROM [dbo].[Customers] AS [t0]  
WHERE [t0].[City] = @p0  
-- @p0: Input String (Size = 6; Prec = 0; Scale = 0) [London]  
-- Context: SqlProvider(Sql2005) Model: AttributedMetaModel Build: 3.5.20810.0  
```  
  
```  
AROUT  
BSBEV  
CONSH  
EASTC  
NORTS  
SEVES  
```  
  
 [!code-csharp[DLinqDebuggingSupport#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqDebuggingSupport/cs/Program.cs#1)]
 [!code-vb[DLinqDebuggingSupport#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqDebuggingSupport/vb/Module1.vb#1)]  
  
## Vedere anche  
 [Supporto per il debug](../../../../../../docs/framework/data/adonet/sql/linq/debugging-support.md)