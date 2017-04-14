---
title: "Procedura: rilevare e risolvere gli invii in conflitto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 91e27206-01fb-4c7a-8afc-1383a6ac5067
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: rilevare e risolvere gli invii in conflitto
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sono disponibili molte risorse per rilevare e risolvere i conflitti causati dalle modifiche apportate al database da più utenti.  Per altre informazioni, vedere [Procedura: gestire i conflitti di modifiche](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato un blocco `try`\/`catch` che rileva un'eccezione <xref:System.Data.Linq.ChangeConflictException>.  Le informazioni sull'entità e sul membro per ogni conflitto sono visualizzate nella finestra della console.  
  
> [!NOTE]
>  Per supportare il recupero delle informazioni, è necessario includere la direttiva `using System.Reflection` \(`Imports System.Reflection` in Visual Basic\).  Per altre informazioni, vedere <xref:System.Reflection>.  
  
 [!code-csharp[DLinqSubmittingChanges#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#2)]
 [!code-vb[DLinqSubmittingChanges#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#2)]  
  
## Vedere anche  
 [Scrittura e invio di modifiche di dati](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)   
 [Procedura: gestire i conflitti di modifiche](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)