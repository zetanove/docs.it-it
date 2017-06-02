---
title: "Funzionalit&#224; non supportata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e480cfb5-697e-42c8-bed5-9264c945c4f9
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Funzionalit&#224; non supportata
In LINQ to SQL non è possibile esporre la funzionalità SQL seguente tramite la conversione di costrutti CLR \(Common Language Runtime\) e .NET Framework esistenti:  
  
-   `STDDEV`  
  
-   `LIKE`  
  
     Sebbene `LIKE` non sia supportato tramite conversione diretta, una funzionalità analoga esiste nella classe <xref:System.Data.Linq.SqlClient.SqlMethods>.  Per altre informazioni, vedere [M:System.Data.Linq.SqlClient.SqlMethods.Like\(System.String,System.String](assetId:///M:System.Data.Linq.SqlClient.SqlMethods.Like(System.String,System.String?qualifyHint=True&autoUpgrade=True).  
  
-   `DATEDIFF`  
  
     LINQ to SQL dispone di un supporto limitato per `DATEDIFF`.  Una funzionalità analoga è presente nella classe [SqlMethods](assetId:///T:System.Data.Linq.SqlClient.SqlMethods?qualifyHint=False&autoUpgrade=True).  
  
-   `ROUND`  
  
     LINQ to SQL dispone di un supporto limitato per `ROUND`.  Per altre informazioni, vedere [Metodi System.Math](../Topic/System.Math%20Methods.md).  
  
## Vedere anche  
 [Tipi di dati e funzioni](../Topic/Data%20Types%20and%20Functions.md)