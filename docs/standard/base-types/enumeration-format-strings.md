---
title: "Stringhe di formato di enumerazione | Microsoft Docs"
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
  - "stringhe di formato di enumerazione"
  - "identificatori di formato, stringhe di formato di enumerazione"
  - "formattazione [.NET Framework], enumerazione"
ms.assetid: dd1ff672-1052-42cf-8666-4924fb6cd1a1
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Stringhe di formato di enumerazione
È possibile utilizzare il metodo <xref:System.Enum.ToString%2A?displayProperty=fullName> per creare un nuovo oggetto stringa che rappresenti il valore numerico, esadecimale o stringa di un membro di enumerazione.  Questo metodo accetta una delle stringhe di formattazione di enumerazione per specificare il valore che si desidera venga restituito.  
  
 Nella tabella che segue sono elencate le stringhe di formattazione di enumerazione e i valori da esse restituiti.  In questi identificatori di formato la distinzione tra maiuscole e minuscole non è rilevante.  
  
|Stringa di formato|Risultato|  
|------------------------|---------------|  
|G o g|Visualizza la voce di enumerazione sotto forma di valore di stringa, se possibile. In caso contrario, visualizza l'Integer dell'istanza corrente.  Se l'enumerazione viene definita con l'attributo **Flags** impostato, i valori di stringa di ciascuna voce valida saranno concatenati tra loro, separati da virgole.  Se l'attributo **Flags** non è impostato, un valore non valido verrà visualizzato sotto forma di voce numerica.  Nell'esempio riportato di seguito viene illustrato l'identificatore di formato G.<br /><br /> [!code-csharp[Formatting.Enum#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#1)]
 [!code-vb[Formatting.Enum#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#1)]|  
|F o f|Visualizza la voce di enumerazione sotto forma di valore di stringa, se possibile.  Se è possibile visualizzare interamente il valore come una sommatoria delle voci dell'enumerazione \(anche se l'attributo **Flags** non è presente\), i valori di stringa di ciascuna voce valida verranno concatenati tra loro, separati da virgole.  Se non è possibile determinare completamente il valore sulla base delle voci di enumerazione, il valore verrà formattato sotto forma di valore integer.  Nell'esempio riportato di seguito viene illustrato l'identificatore di formato F.<br /><br /> [!code-csharp[Formatting.Enum#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#2)]
 [!code-vb[Formatting.Enum#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#2)]|  
|D o d|Visualizza la voce di enumerazione sotto forma di un valore integer nella più breve rappresentazione possibile.  Nell'esempio riportato di seguito viene illustrato l'identificatore di formato D.<br /><br /> [!code-csharp[Formatting.Enum#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#3)]
 [!code-vb[Formatting.Enum#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#3)]|  
|X o x|Visualizza la voce di enumerazione sotto forma di un valore esadecimale.  Se necessario, il valore viene rappresentato con l'aggiunta di un numero di zeri iniziali sufficiente a raggiungere la lunghezza minima di otto cifre.  Nell'esempio riportato di seguito viene illustrato l'identificatore di formato X.<br /><br /> [!code-csharp[Formatting.Enum#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#4)]
 [!code-vb[Formatting.Enum#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#4)]|  
  
## Esempio  
 Nell'esempio riportato di seguito viene definita un'enumerazione denominata `Colors` costituita dalle tre voci `Red`, `Blue` e `Green`.  
  
 [!code-csharp[Formatting.Enum#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#5)]
 [!code-vb[Formatting.Enum#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#5)]  
  
 Al completamento della definizione dell'enumerazione sarà possibile dichiararne un'istanza nel seguente modo:  
  
 [!code-csharp[Formatting.Enum#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#6)]
 [!code-vb[Formatting.Enum#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#6)]  
  
 È quindi possibile utilizzare il metodo `Color.ToString(System.String)` per visualizzare il valore di enumerazione in modi diversi, a seconda dell'identificatore di formato passato.  
  
 [!code-csharp[Formatting.Enum#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#7)]
 [!code-vb[Formatting.Enum#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#7)]  
  
## Vedere anche  
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)