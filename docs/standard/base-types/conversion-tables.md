---
title: "Tabelle di conversione dei tipi in .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "conversioni verso un tipo di dati più grande"
  - "conversioni verso un tipo di dati più piccolo"
  - "conversione dei tipi, tabella"
  - "conversione dei tipi, conversione verso un tipo di dati più grande"
  - "conversione dei tipi, conversione verso un tipo di dati più piccolo"
  - "tipi di base, conversione"
  - "tabelle [.NET Framework], conversione dei tipi"
  - "tipi di dati [.NET Framework], conversione"
ms.assetid: 0ea65c59-85eb-4a52-94ca-c36d3bd13058
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Tabelle di conversione dei tipi in .NET Framework
Si parla di conversione di ampliamento quando un valore di un certo tipo viene convertito in un altro tipo di dimensioni identiche o maggiori.  Si parla di conversione di restrizione quando un valore di un certo tipo viene convertito in un valore di un altro tipo di dimensioni inferiori.  Nelle tabelle riportate in questa sezione sono illustrate le caratteristiche di entrambi i tipi di conversione.  
  
## Conversioni di ampliamento  
 Nella tabella riportata di seguito sono elencate le conversioni di ampliamento che possono essere eseguite senza alcuna perdita di informazioni.  
  
|Type|Conversione senza perdita di dati in|  
|----------|------------------------------------------|  
|<xref:System.Byte>|<xref:System.UInt16>, <xref:System.Int16>, <xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.SByte>|<xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int16>|<xref:System.Int32>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.UInt16>|<xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Char>|<xref:System.UInt16>, <xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int32>|<xref:System.Int64>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.UInt32>|<xref:System.Int64>, <xref:System.UInt64>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int64>|<xref:System.Decimal>|  
|<xref:System.UInt64>|<xref:System.Decimal>|  
|<xref:System.Single>|<xref:System.Double>|  
  
 Alcune conversioni di ampliamento verso <xref:System.Single> o <xref:System.Double> possono provocare una perdita di precisione.  Nella tabella seguente sono elencate le conversioni di ampliamento che possono generare una perdita di informazioni.  
  
|Type|Conversione in|  
|----------|--------------------|  
|<xref:System.Int32>|<xref:System.Single>|  
|<xref:System.UInt32>|<xref:System.Single>|  
|<xref:System.Int64>|<xref:System.Single>, <xref:System.Double>|  
|<xref:System.UInt64>|<xref:System.Single>, <xref:System.Double>|  
|<xref:System.Decimal>|<xref:System.Single>, <xref:System.Double>|  
  
## Conversioni di restrizione  
 Una conversione di restrizione verso <xref:System.Single> o <xref:System.Double> può provocare una perdita di informazioni.  Se il tipo di destinazione non è in grado di rappresentare in modo appropriato l'ordine di grandezza dell'origine, il tipo risultante viene impostato sulla costante `PositiveInfinity` o `NegativeInfinity`.  `PositiveInfinity` è il risultato della divisione di un numero positivo per zero e viene restituito anche quando il valore di un tipo <xref:System.Single> o <xref:System.Double> supera il valore del campo `MaxValue`.  `NegativeInfinity` è il risultato della divisione di un numero negativo per zero e viene restituito anche quando il valore di un tipo <xref:System.Single> o <xref:System.Double> è minore del valore del campo `MinValue`.  Una conversione da un tipo <xref:System.Double> a un tipo <xref:System.Single> potrebbe avere come risultato un valore `PositiveInfinity` o `NegativeInfinity`.  
  
 Una conversione di restrizione può generare una perdita di informazioni anche per altri tipi di dati.  Viene tuttavia generato un evento <xref:System.OverflowException> se il valore di un tipo da convertire non rientra nell'intervallo specificato dai campi `MaxValue` e `MinValue` del tipo di destinazione e il processo di conversione viene controllato dal runtime in modo da assicurare che il valore del tipo di destinazione non superi `MaxValue` o `MinValue`.  Le conversioni eseguite mediante la classe <xref:System.Convert?displayProperty=fullName> vengono sempre controllate in questo modo.  
  
 Nella tabella seguente sono elencate le conversioni che generano un evento <xref:System.OverflowException> utilizzando la classe <xref:System.Convert?displayProperty=fullName> o qualsiasi conversione controllata se il valore del tipo convertito non rientra nell'intervallo specificato per il tipo risultante.  
  
|Type|Conversione in|  
|----------|--------------------|  
|<xref:System.Byte>|<xref:System.SByte>|  
|<xref:System.SByte>|<xref:System.Byte>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64>|  
|<xref:System.Int16>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.UInt16>|  
|<xref:System.UInt16>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>|  
|<xref:System.Int32>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>,<xref:System.UInt32>|  
|<xref:System.UInt32>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>|  
|<xref:System.Int64>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>,<xref:System.UInt32>,<xref:System.UInt64>|  
|<xref:System.UInt64>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>|  
|<xref:System.Decimal>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
|<xref:System.Single>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
|<xref:System.Double>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
  
## Vedere anche  
 <xref:System.Convert?displayProperty=fullName>   
 [Conversione di tipi in .NET Framework](../../../docs/standard/base-types/type-conversion.md)