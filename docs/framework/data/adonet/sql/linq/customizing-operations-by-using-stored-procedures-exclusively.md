---
title: "Personalizzazione delle operazioni tramite l&#39;utilizzo esclusivo di stored procedure | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 441e8ef3-998c-4d12-8825-ce66a178f90f
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Personalizzazione delle operazioni tramite l&#39;utilizzo esclusivo di stored procedure
L'accesso ai dati usando solo stored procedure costituisce uno scenario comune.  
  
## Esempio  
  
### Descrizione  
 È possibile modificare l'esempio fornito in [Personalizzazione delle operazioni tramite l'utilizzo di stored procedure](../../../../../../docs/framework/data/adonet/sql/linq/customizing-operations-by-using-stored-procedures.md) sostituendo anche la prima query, che causa l'esecuzione di SQL dinamico, con una chiamata al metodo che esegue il wrapping di un stored procedure.  
  
 Si supponga che il metodo sia `CustomersByCity`, come nell'esempio seguente.  
  
### Codice  
 [!code-csharp[DLinqOverrideDefaultSproc#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefaultSproc/cs/northwind.cs#4)]
 [!code-vb[DLinqOverrideDefaultSproc#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefaultSproc/vb/northwind.vb#4)]  
  
 Il codice seguente viene eseguito senza SQL dinamico.  
  
 [!code-csharp[DLinqOverrideDefaultSproc#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefaultSproc/cs/Program.cs#5)]
 [!code-vb[DLinqOverrideDefaultSproc#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefaultSproc/vb/Module1.vb#5)]  
  
## Vedere anche  
 [Responsabilità dello sviluppatore nell'eseguire l'override del comportamento predefinito](../../../../../../docs/framework/data/adonet/sql/linq/responsibilities-of-the-developer-in-overriding-default-behavior.md)