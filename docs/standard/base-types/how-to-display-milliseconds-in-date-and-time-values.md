---
title: "Procedura: visualizzare i millisecondi nei valori data e ora | Microsoft Docs"
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
  - "date [.NET Framework], millisecondi"
  - "metodo DateTime.ToString"
  - "visualizzazione di dati relativi a data e ora"
  - "millisecondi [.NET Framework]"
  - "ora [.NET Framework], millisecondi"
ms.assetid: ae1a0610-90b9-4877-8eb6-4e30bc5e00cf
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: visualizzare i millisecondi nei valori data e ora
I metodi di formattazione di data e ora predefiniti, come <xref:System.DateTime.ToString?displayProperty=fullName>, includono le ore, i minuti e i secondi di un valore di ora ma ne escludono il componente millisecondi.  In questo argomento viene illustrato come includere un componente millisecondi di una data e un'ora nelle stringhe di data e ora formattate.  
  
### Per visualizzare il componente millisecondi di un valore DateTime  
  
1.  Se si sta lavorando alla rappresentazione di stringa di una data, convertirla in un valore <xref:System.DateTime> o in un valore <xref:System.DateTimeOffset> utilizzando il metodo statico <xref:System.DateTime.Parse%28System.String%29?displayProperty=fullName> o <xref:System.DateTimeOffset.Parse%28System.String%29?displayProperty=fullName>.  
  
2.  Per estrarre la rappresentazione di stringa del componente millisecondi di un'ora, chiamare il metodo <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName> o <xref:System.DateTimeOffset.ToString%2A> del valore di data e ora e passare il modello di formato personalizzato `fff` o `FFF` da solo o con altri identificatori di formato personalizzato come parametro `format`.  
  
## Esempio  
 Nell'esempio il componente millisecondi di un valore <xref:System.DateTime> e <xref:System.DateTimeOffset> viene visualizzato nella console, sia da solo che incluso in una stringa di data e ora più lunga.  
  
 [!code-csharp[Formatting.HowTo.Millisecond#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#1)]
 [!code-vb[Formatting.HowTo.Millisecond#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#1)]  
  
 Il modello di formato `fff` include gli zeri finali nei millisecondi.  Il modello di formato `FFF` non li visualizza.  Nell'esempio riportato di seguito viene illustrata questa differenza.  
  
 [!code-csharp[Formatting.HowTo.Millisecond#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#2)]
 [!code-vb[Formatting.HowTo.Millisecond#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#2)]  
  
 La definizione di un identificatore di formato personalizzato completo che includa il componente millisecondi di una data e ora pone il problema di definire un formato specificato a livello di codice \(hard\-coded\) che potrebbe non corrispondere alla disposizione degli elementi relativi all'ora specificata dalle impostazioni cultura correnti dell'applicazione.  Un'alternativa migliore consiste nel recuperare uno dei modelli di visualizzazione della data\/ora definiti dall'oggetto <xref:System.Globalization.DateTimeFormatInfo> delle impostazioni cultura correnti e modificarlo in modo da includere i millisecondi.  Nell'esempio viene illustrato anche questo tipo di approccio.  Viene recuperato il modello di data e ora completo delle impostazioni cultura correnti dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=fullName> e viene quindi inserito il modello personalizzato `.ffff` dopo il modello dei secondi.  Notare che nell'esempio viene utilizzata un'espressione regolare per eseguire questa operazione in una sola chiamata al metodo.  
  
 È anche possibile utilizzare un identificatore di formato personalizzato per visualizzare una parte frazionaria di secondi diversa dai millisecondi.  L'identificatore di formato personalizzato `f` o `F` consente di visualizzare ad esempio i decimi di secondo, l'identificatore di formato personalizzato `ff` o `FF` i centesimi di secondo e l'identificatore di formato personalizzato `ffff` o `FFFF` i decimillesimi di secondo.  Le parti frazionarie di un millisecondo vengono troncate anziché arrotondate nella stringa restituita.  Tali identificatori di formato vengono utilizzati nell'esempio riportato di seguito.  
  
 [!code-csharp[Formatting.HowTo.Millisecond#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#3)]
 [!code-vb[Formatting.HowTo.Millisecond#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#3)]  
  
> [!NOTE]
>  È possibile visualizzare piccolissime unità di secondo frazionarie, come decimillesimi di secondo o centomillesimi di secondo.  Questi valori tuttavia potrebbero non essere significativi.  La precisione dei valori di data e ora dipende dalla risoluzione dell'orologio di sistema.  In Windows NT 3.5 e versioni successive e nei sistemi operativi [!INCLUDE[windowsver](../../../includes/windowsver-md.md)] la risoluzione dell'orologio è di circa 10\-15 millisecondi.  
  
## Compilazione del codice  
 Compilare il codice alla riga di comando utilizzando csc.exe o vb.exe.  Per compilare il codice in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], inserirlo in un modello di progetto di applicazione console.  
  
## Vedere anche  
 <xref:System.Globalization.DateTimeFormatInfo>   
 [Stringhe di formato di data e ora personalizzato](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)