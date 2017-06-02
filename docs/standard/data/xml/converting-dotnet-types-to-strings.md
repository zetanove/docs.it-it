---
title: "Conversione dei tipi di .NET Framework in stringhe | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: dc2e2b65-f623-4dc3-938b-d2a054d6832c
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Conversione dei tipi di .NET Framework in stringhe
Per convertire un tipo .NET Framework in una stringa, usare il metodo **ToString**,  che restituisce una rappresentazione di stringa del tipo passato.  Nella tabella seguente sono elencati i tipi .NET Framework che restituiscono una stringa in un formato corrispondente alle specifiche XML Schema \(XSD\).  
  
|Tipo .NET Framework|Tipo di stringa restituito|  
|-------------------------|--------------------------------|  
|Boolean|"true", "false"|  
|Single.PositiveInfinity|"INF"|  
|Single.NegativeInfinity|"\-INF"|  
|Double.PositiveInfinity|"INF"|  
|Double.NegativeInfinity|"\-INF"|  
|DateTime|Il formato è yyyy\-MM\-ddTHH:mm:sszzzzzz e i relativi subset.|  
|TimeSpan|Il formato è PnYnMnTnHnMnSad esempio, `P2Y10M15DT10H30M20S` corrisponde a una durata di 2 anni, 10 mesi, 15 giorni, 10 ore, 30 minuti e 20 secondi.|  
  
## Vedere anche  
 [Conversione dei tipi di dati XML](../../../../docs/standard/data/xml/conversion-of-xml-data-types.md)   
 [Conversione delle stringhe in tipi di dati di .NET Framework](../../../../docs/standard/data/xml/converting-strings-to-dotnet-data-types.md)