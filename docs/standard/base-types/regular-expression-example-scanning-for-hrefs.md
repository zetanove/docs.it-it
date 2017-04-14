---
title: "Esempio di espressione regolare: ricerca di HREF | Microsoft Docs"
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
  - "ricerca con espressioni regolari, esempi"
  - "analisi di testo con espressioni regolari, esempi"
  - "espressioni regolari, esempi"
  - "espressioni regolari di .NET Framework, esempi"
  - "espressioni regolari [.NET Framework], esempi"
  - "corrispondenza al modello con espressioni regolari, esempi"
ms.assetid: fae2c15b-7adf-4b15-b118-58eb3906994f
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# Esempio di espressione regolare: ricerca di HREF
Nell'esempio riportato di seguito viene cercata una stringa di input e vengono visualizzati tutti i valori href\="…" e le relative posizioni nella stringa.  
  
## Oggetto Regex  
 Poiché il metodo `DumpHRefs` può essere chiamato più volte dal codice utente, viene utilizzato il metodo <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=fullName> `static` \(`Shared` in Visual Basic\).  In questo modo il motore delle espressioni regolari è in grado di memorizzare l'espressione regolare nella cache ed è possibile evitare il sovraccarico associato alla creazione di un'istanza di un nuovo oggetto <xref:System.Text.RegularExpressions.Regex> ogni volta che il metodo viene chiamato.  Viene quindi utilizzato un oggetto <xref:System.Text.RegularExpressions.Match> per scorrere tutte le corrispondenze nella stringa.  
  
 [!code-csharp[RegularExpressions.Examples.HREF#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.HREF/cs/example.cs#1)]
 [!code-vb[RegularExpressions.Examples.HREF#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.HREF/vb/example.vb#1)]  
  
 Nell'esempio seguente viene illustrata una chiamata al metodo `DumpHRefs`.  
  
 [!code-csharp[RegularExpressions.Examples.HREF#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.HREF/cs/example.cs#2)]
 [!code-vb[RegularExpressions.Examples.HREF#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.HREF/vb/example.vb#2)]  
  
 Il modello di espressione regolare `href\s*=\s*(?:["'](?<1>[^"']*)["']|(?<1>\S+))` viene interpretato come illustrato nella tabella seguente.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`href`|Trova la corrispondenza della stringa letterale "href".  La corrispondenza prevede la distinzione tra maiuscole e minuscole.|  
|`\s*`|Trovare la corrispondenza di zero o più spazi vuoti.|  
|`=`|Trovare la corrispondenza del segno di uguale.|  
|`\s*`|Trovare la corrispondenza di zero o più spazi vuoti.|  
|`(?:["'](?<1>[^"']*)"&#124;(?<1>\S+))`|Trovare la corrispondenza di uno dei caratteri seguenti senza assegnare il risultato a un gruppo acquisito:<br /><br /> -   Una virgoletta o un apostrofo, seguito da zero o più occorrenze di qualsiasi carattere diverso dalla virgoletta o dall'apostrofo, seguito da una virgoletta o un apostrofo.  Il gruppo denominato `1` è incluso in questo modello.<br />-   Uno o più caratteri diversi da uno spazio vuoto.  Il gruppo denominato `1` è incluso in questo modello.|  
|`(?<1>[^"']*)`|Assegnare zero o più occorrenze di qualsiasi carattere diverso da una virgoletta o un apostrofo al gruppo di acquisizione denominato `1`.|  
|`"(?<1>\S+)`|Assegnare uno o più caratteri diversi da uno spazio vuoto al gruppo di acquisizione denominato `1`.|  
  
## Classe di risultati Match  
 I risultati di una ricerca vengono archiviati nella classe <xref:System.Text.RegularExpressions.Match>, che consente l'accesso a tutte le sottostringhe estratte dalla ricerca.  Tale classe memorizza inoltre la stringa cercata e l'espressione regolare utilizzata, al fine di poter chiamare il metodo <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=fullName> per eseguire un'ulteriore ricerca a partire dal punto in cui è terminata l'ultima.  
  
## Catture denominate in modo esplicito  
 Nelle espressioni regolari tradizionali, le parentesi di cattura vengono numerate automaticamente in sequenza.  Ne conseguono due problemi.  Se innanzitutto un'espressione regolare viene modificata per effetto dell'inserimento o della rimozione di una coppia di parentesi, in osservanza della nuova numerazione è necessario riscrivere tutto il codice che fa riferimento alle catture numerate.  In secondo luogo, poiché spesso vengono utilizzate diverse coppie di parentesi per fornire due espressioni alternative che individuano corrispondenze altrettanto valide, può risultare difficile determinare quale delle due espressioni ha effettivamente restituito un risultato.  
  
 Per risolvere questi problemi, la classe <xref:System.Text.RegularExpressions.Regex> supporta la sintassi `(?<name>…)` per l'acquisizione di una corrispondenza in uno slot specificato, che è possibile denominare tramite una stringa o un valore intero, che può essere richiamato più rapidamente.  Le corrispondenze alternative della stessa stringa possono essere pertanto indirizzate tutte allo stesso comparto.  In caso di conflitto, l'ultima corrispondenza inserita in un comparto è quella corretta. È comunque disponibile un elenco completo delle diverse corrispondenze relative a un singolo comparto.  Per ulteriori informazioni, vedere la raccolta <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=fullName>.  
  
## Vedere anche  
 [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)