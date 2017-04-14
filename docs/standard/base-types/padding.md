---
title: "Aggiunta di spaziatura interna alle stringhe in .NET Framework | Microsoft Docs"
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
  - "aggiunta di spaziatura interna alle stringhe"
  - "PadLeft (metodo)"
  - "PadRight (metodo)"
  - "stringhe [.NET Framework], spaziatura"
  - "spazio vuoto"
ms.assetid: 84a9f142-3244-4c90-ba02-21af9bbaff71
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Aggiunta di spaziatura interna alle stringhe in .NET Framework
Utilizzare uno dei metodi della classe <xref:System.String> seguenti per creare una nuova stringa costituita da una stringa originale a cui vengono aggiunti caratteri iniziali o finali fino a ottenere una lunghezza totale specificata.  Il carattere di spaziatura interna può essere costituito da spazi o da un carattere specifico e di conseguenza può essere allineato a destra o a sinistra.  
  
|Nome del metodo|Utilizzo|  
|---------------------|--------------|  
|<xref:System.String.PadLeft%2A?displayProperty=fullName>|Aggiunge a una stringa caratteri iniziali fino a raggiungere una lunghezza totale specificata.|  
|<xref:System.String.PadRight%2A?displayProperty=fullName>|Aggiunge a una stringa caratteri finali fino a raggiungere una lunghezza totale specificata.|  
  
## PadLeft  
 Il metodo <xref:System.String.PadLeft%2A?displayProperty=fullName> crea una nuova stringa concatenando una stringa originale con un numero di caratteri di spaziatura iniziali sufficienti per ottenere una lunghezza totale specificata.  Il metodo <xref:System.String.PadLeft%28System.Int32%29?displayProperty=fullName> utilizza spazi come caratteri di spaziatura interna e il metodo <xref:System.String.PadLeft%28System.Int32%2CSystem.Char%29?displayProperty=fullName> consente di specificare un carattere di spaziatura interna personalizzato.  
  
 Nell'esempio di codice riportato di seguito viene utilizzato il metodo <xref:System.String.PadLeft%2A> per creare una nuova stringa di venti caratteri di lunghezza.  Nella console verrà visualizzato "`--------Hello World!`".  
  
 [!code-cpp[Conceptual.String.BasicOps#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#3)]
 [!code-csharp[Conceptual.String.BasicOps#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#3)]
 [!code-vb[Conceptual.String.BasicOps#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#3)]  
  
## PadRight  
 Il metodo <xref:System.String.PadRight%2A?displayProperty=fullName> crea una nuova stringa concatenando una stringa originale con un numero di caratteri di spaziatura finali sufficienti per ottenere una lunghezza totale specificata.  Il metodo <xref:System.String.PadRight%28System.Int32%29?displayProperty=fullName> utilizza spazi come caratteri di spaziatura interna e il metodo <xref:System.String.PadRight%28System.Int32%2CSystem.Char%29?displayProperty=fullName> consente di specificare un carattere di spaziatura interna personalizzato.  
  
 Nell'esempio di codice riportato di seguito viene utilizzato il metodo <xref:System.String.PadRight%2A> per creare una nuova stringa di venti caratteri di lunghezza.  Nella console verrà visualizzato "`Hello World!--------`".  
  
 [!code-cpp[Conceptual.String.BasicOps#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#4)]
 [!code-csharp[Conceptual.String.BasicOps#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#4)]
 [!code-vb[Conceptual.String.BasicOps#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#4)]  
  
## Vedere anche  
 [Operazioni di base su stringhe](../../../docs/standard/base-types/basic-string-operations.md)