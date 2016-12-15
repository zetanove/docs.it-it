---
title: "Procedura: convertire una matrice di byte in un Integer (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "matrici di byte [C#], conversione a int"
  - "conversioni [C#], matrice di byte a int"
ms.assetid: d6ac20e2-448e-4aea-99b9-faf04c6f1e79
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: convertire una matrice di byte in un Integer (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In questo esempio viene illustrato come utilizzare la classe <xref:System.BitConverter> per convertire una matrice di byte in un valore [int](../../../csharp/language-reference/keywords/int.md) e nuovamente in una matrice di byte.  Può essere necessario, ad esempio, convertire un valore in byte in un tipo di dati incorporato dopo avere letto i byte dalla rete.  Oltre al metodo [ToInt32\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToInt32(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False) dell'esempio, nella tabella riportata di seguito sono elencati i metodi nella classe <xref:System.BitConverter> che convertono i byte \(da una matrice di byte\) in altri tipi incorporati.  
  
|Tipo restituito|Metodo|  
|---------------------|------------|  
|`bool`|[ToBoolean\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToBoolean(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False)|  
|`char`|[ToChar\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToChar(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False)|  
|`double`|[ToDouble\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToDouble(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False)|  
|`short`|[ToInt16\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToInt16(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False)|  
|`int`|[ToInt32\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToInt32(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False)|  
|`long`|[ToInt64\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToInt64(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False)|  
|`float`|[ToSingle\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToSingle(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False)|  
|`ushort`|[ToUInt16\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToUInt16(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False)|  
|`uint`|[ToUInt32\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToUInt32(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False)|  
|`ulong`|[ToUInt64\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToUInt64(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False)|  
  
## Esempio  
 In questo esempio viene inizializzata una matrice di byte, viene convertita la matrice se l'architettura del computer è little\-endian \(byte meno significativo archiviato per primo\), quindi viene chiamato il metodo [ToInt32\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToInt32(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False) per convertire quattro byte nella matrice in un valore `int`.  Il secondo argomento nel metodo [ToInt32\(Byte\[\], Int32\)](assetId:///M:System.BitConverter.ToInt32(System.Byte[],System.Int32)?qualifyHint=False&autoUpgrade=False) specifica l'indice di inizio della matrice di byte.  
  
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