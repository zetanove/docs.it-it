---
title: "Procedura: definire e utilizzare provider di formati numerici personalizzati | Microsoft Docs"
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
  - "stringhe di formato personalizzate"
  - "stringhe di formato numerico personalizzate"
  - "visualizzazione di dati relativi a data e ora"
  - "provider di formato [.NET Framework]"
  - "formattazione [.NET Framework], numeri"
  - "numeri (formattazione) [.NET Framework]"
  - "numeri [.NET Framework], stringhe di formato numerico personalizzate"
  - "stringhe di formato numerico [.NET Framework]"
ms.assetid: a281bfbf-6596-45ed-a2d6-3782d535ada2
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: definire e utilizzare provider di formati numerici personalizzati
[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] offre un ampio controllo sulla rappresentazione di stringa dei valori numerici.  e supporta le funzionalità seguenti per la personalizzazione del formato dei valori numerici:  
  
-   Stringhe di formato numerico standard che forniscono un insieme predefinito di formati per la conversione dei numeri nella rispettiva rappresentazione di stringa.  È possibile utilizzarle con qualsiasi metodo di formattazione numerica, come <xref:System.Decimal.ToString%28System.String%29?displayProperty=fullName> che include un parametro `format`.  Per informazioni dettagliate, vedere [Stringhe di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md).  
  
-   Stringhe di formato numerico personalizzate che forniscono un insieme di simboli che possono essere combinati per definire identificatori di formato numerico personalizzati.  È anche possibile utilizzarle con qualsiasi metodo di formattazione numerica, come <xref:System.Decimal.ToString%28System.String%29?displayProperty=fullName> che include un parametro `format`.  Per informazioni dettagliate, vedere [Stringhe di formato numerico personalizzato](../../../docs/standard/base-types/custom-numeric-format-strings.md).  
  
-   Oggetti <xref:System.Globalization.CultureInfo> o <xref:System.Globalization.NumberFormatInfo> personalizzati che definiscono i simboli e i modelli di formato utilizzati per la visualizzazione delle rappresentazioni di stringa di valori numerici.  È possibile utilizzarli con qualsiasi metodo di formattazione numerica, come <xref:System.Int32.ToString%2A> che include un parametro `provider`.  In genere, il parametro `provider` viene utilizzato per specificare informazioni di formattazione specifiche delle impostazioni cultura.  
  
 In alcuni casi, ad esempio quando un'applicazione deve visualizzare un numero di account formattato, un numero di identificazione o un codice postale, queste tre tecniche non sono adatte.  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] consente anche di definire un oggetto di formattazione che non è né un oggetto <xref:System.Globalization.CultureInfo> né un oggetto <xref:System.Globalization.NumberFormatInfo> e consente di determinare la modalità di formattazione di un valore numerico.  In questo argomento sono contenute istruzioni dettagliate per l'implementazione di tale oggetto ed è inoltre riportato un esempio di formattazione di numeri di telefono.  
  
### Per definire un provider di formato personalizzato  
  
1.  Definire una classe che implementa le interfacce <xref:System.IFormatProvider> e <xref:System.ICustomFormatter>.  
  
2.  Implementare il metodo <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName>.  <xref:System.IFormatProvider.GetFormat%2A> è un metodo di callback che viene richiamato dal metodo di formattazione \(ad esempio dal metodo [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName>\) per recuperare l'oggetto responsabile della formattazione personalizzata.  Una tipica implementazione di <xref:System.IFormatProvider.GetFormat%2A> effettua le operazioni seguenti:  
  
    1.  Determina se l'oggetto <xref:System.Type> passato come parametro di metodo rappresenta un'interfaccia <xref:System.ICustomFormatter>.  
  
    2.  Se il parametro rappresenta l'interfaccia <xref:System.ICustomFormatter>, <xref:System.IFormatProvider.GetFormat%2A> restituisce un oggetto che implementa l'interfaccia <xref:System.ICustomFormatter> che è responsabile della formattazione personalizzata.  In genere, l'oggetto di formattazione personalizzata restituisce se stesso.  
  
    3.  Se il parametro non rappresenta l'interfaccia <xref:System.ICustomFormatter>, <xref:System.IFormatProvider.GetFormat%2A> restituisce `null`.  
  
3.  Implementare il metodo <xref:System.ICustomFormatter.Format%2A>.  Questo metodo viene chiamato dal metodo [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> ed è responsabile della restituzione della rappresentazione di stringa di un numero.  L'implementazione del metodo in genere implica le attività seguenti:  
  
    1.  Facoltativamente, assicurarsi che il metodo sia correttamente destinato a fornire servizi di formattazione esaminando il parametro `provider`.  Per la formattazione degli oggetti che implementano entrambi i metodi <xref:System.IFormatProvider> e <xref:System.ICustomFormatter>, questa operazione richiede il test del parametro `provider` per verificare l'uguaglianza con l'oggetto di formattazione corrente.  
  
    2.  Determinare se l'oggetto di formattazione deve supportare identificatori di formato personalizzati. \(Ad esempio, un identificatore di formato "N" potrebbe indicare che un numero di telefono degli Stati Uniti deve essere restituito in formato NANP e una "I" potrebbe indicare l'output in formato ITU\-T Recommendation E.123.\) Se si utilizzano identificatori di formato, il metodo deve gestire l'identificatore di formato specifico.  Quest'ultimo viene passato al metodo nel parametro `format`.  Se non è disponibile alcun identificatore, il valore del parametro `format` è <xref:System.String.Empty?displayProperty=fullName>.  
  
    3.  Recuperare il valore numerico passato al metodo come parametro `arg`.  Eseguire le eventuali modifiche necessarie per convertirlo nella relativa rappresentazione di stringa.  
  
    4.  Restituire la rappresentazione di stringa del parametro `arg`.  
  
### Per utilizzare un oggetto di formattazione numerica personalizzata  
  
1.  Creare una nuova istanza della classe di formattazione personalizzata.  
  
2.  Chiamare il metodo di formattazione [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName>, passando l'oggetto di formattazione personalizzata, l'identificatore di formattazione \(o <xref:System.String.Empty?displayProperty=fullName> se non viene utilizzato alcun identificatore\) e il valore numerico da formattare.  
  
## Esempio  
 Nell'esempio seguente viene definito un provider di formato numerico personalizzato denominato `TelephoneFormatter` che converte un numero che rappresenta un numero telefonico degli Stati Uniti nel suo formato NANP oppure E.123.  Il metodo gestisce due identificatori di formato, "N" \(che restituisce il formato NANP\) e "I" \(che restituisce il formato E.123 internazionale\)."  
  
 [!code-csharp[Formatting.HowTo.NumericValue#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.NumericValue/cs/Telephone1.cs#1)]
 [!code-vb[Formatting.HowTo.NumericValue#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.NumericValue/vb/Telephone1.vb#1)]  
  
 Il provider di formato numerico personalizzato può essere utilizzato solo con il metodo [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName>.  Gli altri overload dei metodi di formattazione numerica \(ad esempio `ToString`\) che hanno un parametro di tipo <xref:System.IFormatProvider> passano all'implementazione <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName> un oggetto <xref:System.Type> che rappresenta il tipo <xref:System.Globalization.NumberFormatInfo>.  In cambio, prevedono che il metodo restituisca un oggetto <xref:System.Globalization.NumberFormatInfo>.  In caso contrario, il provider di formato numerico personalizzato viene ignorato e al suo posto viene utilizzato l'oggetto <xref:System.Globalization.NumberFormatInfo> relativo alle impostazioni cultura correnti.  Nell'esempio il metodo `TelephoneFormatter.GetFormat` gestisce la possibilità che possa essere passato erroneamente a un metodo di formattazione numerica esaminando il parametro del metodo e restituendo `null` se rappresenta un tipo diverso da <xref:System.ICustomFormatter>.  
  
 Se un provider di formato numerico personalizzato supporta un insieme di identificatori di formato, assicurarsi di specificare un comportamento predefinito nel caso in cui non venga fornito alcun identificatore di formato nell'elemento di formato utilizzato nella chiamata al metodo [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName>.  Nell'esempio "N" è l'identificatore di formato predefinito.  È pertanto possibile convertire un numero in un numero di telefono formattato mediante la specifica di un identificatore di formato esplicito.  Nell'esempio riportato di seguito viene illustrata questa chiamata al metodo.  
  
 [!code-csharp[Formatting.HowTo.NumericValue#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.NumericValue/cs/Telephone1.cs#2)]
 [!code-vb[Formatting.HowTo.NumericValue#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.NumericValue/vb/Telephone1.vb#2)]  
  
 L'esecuzione della conversione è possibile anche in assenza di identificatori di formato.  Nell'esempio riportato di seguito viene illustrata questa chiamata al metodo.  
  
 [!code-csharp[Formatting.HowTo.NumericValue#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.NumericValue/cs/Telephone1.cs#3)]
 [!code-vb[Formatting.HowTo.NumericValue#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.NumericValue/vb/Telephone1.vb#3)]  
  
 Se non è definito alcun identificatore di formato predefinito, l'implementazione del metodo <xref:System.ICustomFormatter.Format%2A?displayProperty=fullName> deve includere elementi di codice come quelli riportati di seguito in modo da consentire a .NET Framework di fornire la formattazione non supportata dal proprio codice.  
  
 [!code-csharp[System.ICustomFormatter.Format#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.ICustomFormatter.Format/cs/format.cs#1)]
 [!code-vb[System.ICustomFormatter.Format#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.ICustomFormatter.Format/vb/Format.vb#1)]  
  
 In questo esempio il metodo che implementa <xref:System.ICustomFormatter.Format%2A?displayProperty=fullName> è destinato a essere utilizzato come metodo di callback per il metodo [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName>.  Tale metodo esamina dunque il parametro `formatProvider` per determinare se contiene un riferimento all'oggetto `TelephoneFormatter` corrente.  Il metodo può tuttavia essere chiamato anche direttamente dal codice.  In questo caso è possibile utilizzare il parametro `formatProvider` per specificare un oggetto <xref:System.Globalization.CultureInfo> o <xref:System.Globalization.NumberFormatInfo> che fornisce informazioni di formattazione specifiche delle impostazioni cultura.  
  
## Compilazione del codice  
 Compilare il codice alla riga di comando utilizzando csc.exe o vb.exe.  Per compilare il codice in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], inserirlo in un modello di progetto di applicazione console.  
  
## Vedere anche  
 [Esecuzione di operazioni di formattazione](../../../docs/standard/base-types/performing-formatting-operations.md)