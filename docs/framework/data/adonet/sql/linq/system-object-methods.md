---
title: "Metodi System.Object | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5397fca0-689e-443e-802f-e1cbdc866427
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Metodi System.Object
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sono supportati i metodi <xref:System.Object> seguenti.  
  
|||  
|-|-|  
|<xref:System.Object.Equals%28System.Object%29?displayProperty=fullName>|<xref:System.Object.Equals%28System.Object%2CSystem.Object%29?displayProperty=fullName>|  
|<xref:System.Object.ToString?displayProperty=fullName>||  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non sono supportati i metodi <xref:System.Object> riportati di seguito.  
  
|||  
|-|-|  
|<xref:System.Object.GetHashCode?displayProperty=fullName>|<xref:System.Object.ReferenceEquals%28System.Object%2CSystem.Object%29?displayProperty=fullName>|  
|<xref:System.Object.MemberwiseClone?displayProperty=fullName>|<xref:System.Object.GetType?displayProperty=fullName>|  
|<xref:System.Object.ToString?displayProperty=fullName> per i tipi binari, ad esempio `BINARY`, `VARBINARY`, `IMAGE` e `TIMESTAMP`.||  
  
## Differenze rispetto a .NET  
 Nell'output di <xref:System.Object.ToString?displayProperty=fullName> per i valori double viene usato il valore SQL`CONVERT`\(NVARCHAR\(30\), @x, 2\) in SQL.  In SQL vengono sempre usate 16 cifre e la notazione scientifica in questo caso, ad esempio "0.000000000000000e\+000" per 0.  Di conseguenza, la conversione di <xref:System.Object.ToString?displayProperty=fullName> non genera la stessa stringa di <xref:System.Convert.ToString%2A?displayProperty=fullName> in .NET Framework.  
  
## Vedere anche  
 [Tipi di dati e funzioni](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)