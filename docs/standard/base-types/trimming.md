---
title: "Eliminazione di spazi iniziali e finali e rimozione di caratteri dalle stringhe in .NET Framework | Microsoft Docs"
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
  - "Remove (metodo)"
  - "rimozione di caratteri"
  - "stringhe [.NET Framework], rimozione di caratteri"
  - "Trim (metodo)"
  - "TrimEnd (metodo)"
  - "caratteri di rimozione spazi"
  - "TrimStart (metodo)"
ms.assetid: ab248dab-70d4-4413-81c6-542d153fd195
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Eliminazione di spazi iniziali e finali e rimozione di caratteri dalle stringhe in .NET Framework
Quando si suddivide una frase in parole singole è possibile che prima o dopo le parole rimangano spazi vuoti.  In questo caso è possibile utilizzare uno dei metodi della classe **System.String** per rimuovere spazi o altri caratteri da una posizione specificata all'interno della stringa.  Nella tabella che segue sono descritti i metodi disponibili per l'eliminazione degli spazi iniziali e finali.  
  
|Nome del metodo|Utilizzo|  
|---------------------|--------------|  
|<xref:System.String.Trim%2A?displayProperty=fullName>|Rimuove gli spazi vuoti o i caratteri specificati in un array di caratteri dall'inizio e alla fine di una stringa.|  
|<xref:System.String.TrimEnd%2A?displayProperty=fullName>|Consente di rimuovere i caratteri specificati in una matrice di caratteri dalla fine di una stringa.|  
|<xref:System.String.TrimStart%2A?displayProperty=fullName>|Consente di rimuovere i caratteri specificati in una matrice di caratteri dall'inizio di una stringa.|  
|<xref:System.String.Remove%2A?displayProperty=fullName>|Consente di rimuovere un numero specificato di caratteri da una posizione di indice specificata in una stringa.|  
  
## Trim  
 È possibile rimuovere facilmente gli spazi vuoti da entrambe le estremità di una stringa utilizzando il metodo <xref:System.String.Trim%2A?displayProperty=fullName>, come illustrato nell'esempio di codice che segue.  
  
 [!code-cpp[Conceptual.String.BasicOps#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#17)]
 [!code-csharp[Conceptual.String.BasicOps#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#17)]
 [!code-vb[Conceptual.String.BasicOps#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#17)]  
  
 È anche possibile rimuovere i caratteri specificati in un array di caratteri all'inizio e alla fine di una stringa.  L'esempio seguente consente di rimuovere gli spazi vuoti, i punti e gli asterischi.  
  
 [!code-csharp[Conceptual.String.BasicOps#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trim2.cs#22)]
 [!code-vb[Conceptual.String.BasicOps#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trim2.vb#22)]  
  
## TrimEnd  
 Il metodo **String.TrimEnd** consente di rimuovere caratteri dalla fine di una stringa, creando un nuovo oggetto stringa.  Una matrice di caratteri viene passata al metodo per specificare i caratteri da rimuovere.  L'ordine degli elementi nella matrice di caratteri non ha effetto sull'eliminazione degli spazi iniziali e finali.  L'eliminazione di spazi iniziali e finali ha termine quando viene individuato un carattere non specificato nella matrice.  
  
 Nell'esempio che segue vengono rimosse le ultime lettere di una stringa utilizzando il metodo **TrimEnd**.  La posizione dei caratteri `'r'` e `'W'` è invertita, per indicare che l'ordine dei caratteri nella matrice è ininfluente.  Si noti che viene rimossa l'ultima parola di `MyString` più una parte della prima.  
  
 [!code-cpp[Conceptual.String.BasicOps#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#18)]
 [!code-csharp[Conceptual.String.BasicOps#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#18)]
 [!code-vb[Conceptual.String.BasicOps#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#18)]  
  
 Nella console verrà visualizzato `He`.  
  
 Nell'esempio che segue viene rimossa l'ultima parola di una stringa utilizzando il metodo **TrimEnd**.  La parola `Hello` è preceduta nel codice da una virgola e, poiché questo segno di punteggiatura non è specificato nella matrice di caratteri di cui eliminare gli spazi iniziali e finali, il codice termina in corrispondenza della virgola.  
  
 [!code-cpp[Conceptual.String.BasicOps#19](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#19)]
 [!code-csharp[Conceptual.String.BasicOps#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#19)]
 [!code-vb[Conceptual.String.BasicOps#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#19)]  
  
 Nella console verrà visualizzato `Hello,`.  
  
## TrimStart  
 Il metodo **String.TrimStart** è analogo a **String.TrimEnd**, fatta eccezione per il fatto che consente di creare una nuova stringa rimuovendo i caratteri dall'inizio di un oggetto stringa esistente.  Una matrice di caratteri viene passata al metodo **TrimStart** per specificare i caratteri da rimuovere.  Come per il metodo **TrimEnd**, l'ordine degli elementi nella matrice di caratteri non ha effetto sull'eliminazione di spazi iniziali e finali.  L'eliminazione di spazi iniziali e finali ha termine quando viene individuato un carattere non specificato nella matrice.  
  
 Nell'esempio che segue viene rimossa la prima parola di una stringa.  La posizione dei caratteri `'l'` e `'H'` è invertita, per indicare che l'ordine dei caratteri nella matrice è ininfluente.  
  
 [!code-cpp[Conceptual.String.BasicOps#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#20)]
 [!code-csharp[Conceptual.String.BasicOps#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#20)]
 [!code-vb[Conceptual.String.BasicOps#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#20)]  
  
 Nella console verrà visualizzato `World!`.  
  
## Rimozione  
 Il metodo <xref:System.String.Remove%2A?displayProperty=fullName> consente di rimuovere un numero specificato di caratteri a partire da una posizione specificata da una stringa esistente.  Il metodo presuppone un indice a base zero.  
  
 Nell'esempio che segue vengono rimossi da una stringa dieci caratteri, a partire dalla quinta posizione di un indice a base zero della stringa.  
  
 [!code-cpp[Conceptual.String.BasicOps#21](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#21)]
 [!code-csharp[Conceptual.String.BasicOps#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#21)]
 [!code-vb[Conceptual.String.BasicOps#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#21)]  
  
 È anche possibile rimuovere da una stringa un carattere o una sottostringa specificati chiamando il metodo <xref:System.String.Replace%28System.String%2CSystem.String%29?displayProperty=fullName> e specificando una stringa vuota \(<xref:System.String.Empty?displayProperty=fullName>\) come sostituzione.  L'esempio seguente consente di rimuovere tutte le virgole da una stringa.  
  
 [!code-csharp[Conceptual.String.BasicOps#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/replace1.cs#23)]
 [!code-vb[Conceptual.String.BasicOps#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/replace1.vb#23)]  
  
## Vedere anche  
 [Operazioni di base su stringhe](../../../docs/standard/base-types/basic-string-operations.md)