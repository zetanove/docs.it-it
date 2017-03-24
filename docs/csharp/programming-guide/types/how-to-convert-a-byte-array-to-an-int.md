---
title: "Procedura: convertire una matrice di byte in un Integer (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "matrici di byte [C#], conversione a int"
  - "conversioni [C#], matrice di byte a int"
ms.assetid: d6ac20e2-448e-4aea-99b9-faf04c6f1e79
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# Procedura: convertire una matrice di byte in un Integer (Guida per programmatori C#)
In questo esempio viene illustrato come utilizzare la classe <xref:System.BitConverter> per convertire una matrice di byte in un valore [int](../../../csharp/language-reference/keywords/int.md) e nuovamente in una matrice di byte.  Può essere necessario, ad esempio, convertire un valore in byte in un tipo di dati incorporato dopo avere letto i byte dalla rete.  Oltre al metodo [ToInt32\(Byte\<xref:System.BitConverter.ToInt32%28System.Byte%5B%5D%2CSystem.Int32%29> dell'esempio, nella tabella riportata di seguito sono elencati i metodi nella classe <xref:System.BitConverter> che convertono i byte \(da una matrice di byte\) in altri tipi incorporati.  
  
|Tipo restituito|Metodo|  
|---------------------|------------|  
|`bool`|[ToBoolean\(Byte\<xref:System.BitConverter.ToBoolean%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`char`|[ToChar\(Byte\<xref:System.BitConverter.ToChar%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`double`|[ToDouble\(Byte\<xref:System.BitConverter.ToDouble%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`short`|[ToInt16\(Byte\<xref:System.BitConverter.ToInt16%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`int`|[ToInt32\(Byte\<xref:System.BitConverter.ToInt32%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`long`|[ToInt64\(Byte\<xref:System.BitConverter.ToInt64%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`float`|[ToSingle\(Byte\<xref:System.BitConverter.ToSingle%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`ushort`|[ToUInt16\(Byte\<xref:System.BitConverter.ToUInt16%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`uint`|[ToUInt32\(Byte\<xref:System.BitConverter.ToUInt32%28System.Byte%5B%5D%2CSystem.Int32%29>|  
|`ulong`|[ToUInt64\(Byte\<xref:System.BitConverter.ToUInt64%28System.Byte%5B%5D%2CSystem.Int32%29>|  
  
## Esempio  
 In questo esempio viene inizializzata una matrice di byte, viene convertita la matrice se l'architettura del computer è little\-endian \(byte meno significativo archiviato per primo\), quindi viene chiamato il metodo [ToInt32\(Byte\<xref:System.BitConverter.ToInt32%28System.Byte%5B%5D%2CSystem.Int32%29> per convertire quattro byte nella matrice in un valore `int`.  Il secondo argomento nel metodo [ToInt32\(Byte\<xref:System.BitConverter.ToInt32%28System.Byte%5B%5D%2CSystem.Int32%29> specifica l'indice di inizio della matrice di byte.  
  
> [!NOTE]
>  L'output può variare a seconda del tipo di architettura del computer \(little\-endian o big\-endian\).  
  
 [!code-cs[csProgGuideTypes#22](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-byte-array-to-an-int_1.cs)]  
  
## Esempio  
 In questo esempio il metodo <xref:System.BitConverter.GetBytes%28System.Int32%29> della classe <xref:System.BitConverter> viene chiamato per convertire un valore `int` in una matrice di byte.  
  
> [!NOTE]
>  L'output può variare a seconda del tipo di architettura del computer \(little\-endian o big\-endian\).  
  
 [!code-cs[csProgGuideTypes#23](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-byte-array-to-an-int_2.cs)]  
  
## Vedere anche  
 <xref:System.BitConverter>   
 <xref:System.BitConverter.IsLittleEndian>   
 [Tipi](../../../csharp/programming-guide/types/index.md)