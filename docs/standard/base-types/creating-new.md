---
title: "Creazione di nuove stringhe in .NET Framework | Microsoft Docs"
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
  - "Concat (metodo)"
  - "CopyTo (metodo)"
  - "Format (metodo)"
  - "Insert (metodo)"
  - "Join (metodo)"
  - "stringhe [.NET Framework], creazione"
ms.assetid: 06fdf123-2fac-4459-8904-eb48ab908a30
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Creazione di nuove stringhe in .NET Framework
[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] consente di creare stringhe tramite una semplice assegnazione, oltre a eseguire l'overload del costruttore di classe per supportare la creazione di stringhe utilizzando una serie di parametri diversi.  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fornisce inoltre diversi metodi nella classe <xref:System.String?displayProperty=fullName> per creare nuovi oggetti stringa tramite la combinazione di più stringhe, matrici di stringhe o oggetti.  
  
## Creazione di stringhe tramite assegnazione  
 Il modo più semplice per creare un nuovo oggetto <xref:System.String> consiste nell'assegnare un valore letterale stringa a un oggetto <xref:System.String>.  
  
## Creazione di stringhe tramite un costruttore di classe  
 È possibile utilizzare overload del costruttore di classe <xref:System.String> per creare stringhe da matrici di caratteri.  È anche possibile creare una nuova stringa duplicando un determinato carattere per un numero specificato di volte.  
  
## Metodi che restituiscono stringhe  
 Nella tabella seguente sono elencati diversi metodi utili che restituiscono nuovi oggetti stringa.  
  
|Nome del metodo|Utilizzo|  
|---------------------|--------------|  
|<xref:System.String.Format%2A?displayProperty=fullName>|Da un insieme di oggetti di input viene compilata una stringa formattata.|  
|<xref:System.String.Concat%2A?displayProperty=fullName>|Vengono compilate stringhe da due o più stringhe.|  
|<xref:System.String.Join%2A?displayProperty=fullName>|Una nuova stringa viene compilata combinando una matrice di stringhe.|  
|<xref:System.String.Insert%2A?displayProperty=fullName>|Una nuova stringa viene compilata inserendo una stringa in corrispondenza dell'indice specificato di una stringa esistente.|  
|<xref:System.String.CopyTo%2A?displayProperty=fullName>|I caratteri di una stringa specificati vengono copiati in una posizione specificata all'interno di una matrice di caratteri.|  
  
### Format  
 È possibile utilizzare il metodo **String.Format** per creare stringhe formattate e concatenare stringhe che rappresentano più oggetti.  Qualsiasi oggetto venga passato a questo metodo viene automaticamente convertito in una stringa.  Se, ad esempio, l'applicazione deve visualizzare un valore **Int32** e un valore **DateTime**, è possibile costruire con facilità una stringa che rappresenti tali valori utilizzando il metodo **Format**.  Per ulteriori informazioni sulle convenzioni di formattazione utilizzate con questo metodo, vedere la sezione relativa alla [formattazione composita](../../../docs/standard/base-types/composite-formatting.md).  
  
 Nell'esempio di codice che segue il metodo **Format** viene utilizzato per creare una stringa che utilizza una variabile integer.  
  
 [!code-csharp[Strings.Creating#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#1)]
 [!code-vb[Strings.Creating#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#1)]  
  
 In questo esempio<xref:System.DateTime.Now%2A?displayProperty=fullName> visualizza l'ora e la data correnti nel modo specificato dalle impostazioni cultura associate al thread corrente.  
  
### Concat  
 Il metodo **String.Concat** può essere utilizzato per creare facilmente un nuovo oggetto stringa da due o più oggetti esistenti.  Esso fornisce una modalità di concatenamento delle stringhe indipendente dal linguaggio.  Il metodo accetta qualsiasi classe che derivi da **System.Object**.  Nell'esempio di codice che segue viene creata una stringa da due oggetti stringa esistenti e da un carattere di separazione.  
  
 [!code-csharp[Strings.Creating#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#2)]
 [!code-vb[Strings.Creating#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#2)]  
  
### Join  
 Il metodo **String.Join** consente di creare una nuova stringa da una matrice di stringhe e da una stringa di separazione.  Questo metodo è utile per concatenare più stringhe, creando un elenco, eventualmente separato da virgole.  
  
 Nell'esempio di codice seguente viene utilizzato uno spazio per eseguire l'associazione di una matrice di stringhe.  
  
 [!code-csharp[Strings.Creating#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#3)]
 [!code-vb[Strings.Creating#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#3)]  
  
### Insert  
 Il metodo **String.Insert** consente di creare una nuova stringa inserendo una stringa in una posizione specificata all'interno di un'altra stringa.  In questo metodo viene utilizzato un indice a base zero.  Nell'esempio di codice che segue viene inserita una stringa in corrispondenza della quinta posizione di indice di `MyString` e viene creata una nuova stringa con tale valore.  
  
 [!code-csharp[Strings.Creating#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#4)]
 [!code-vb[Strings.Creating#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#4)]  
  
### CopyTo  
 Il metodo **String.CopyTo** consente di copiare parti di una stringa in una matrice di caratteri.  È possibile specificare sia l'indice iniziale della stringa sia il numero dei caratteri da copiare.  Il metodo contiene l'indice di origine, una matrice di caratteri, l'indice di destinazione e il numero dei caratteri da copiare.  Tutti gli indici sono a base zero.  
  
 Nell'esempio di codice riportato di seguito viene utilizzato il metodo **CopyTo** per copiare nella prima posizione di indice di una matrice di caratteri i caratteri della parola "Hello" di un oggetto stringa.  
  
 [!code-csharp[Strings.Creating#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#5)]
 [!code-vb[Strings.Creating#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#5)]  
  
## Vedere anche  
 [Operazioni di base su stringhe](../../../docs/standard/base-types/basic-string-operations.md)   
 [Formattazione composita](../../../docs/standard/base-types/composite-formatting.md)