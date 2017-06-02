---
title: "Stringhe di formato numerico personalizzato | Microsoft Docs"
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
  - "stringhe di formato numerico personalizzate"
  - "identificatori di formato, stringhe di formato numerico personalizzate"
  - "identificatori di formato, numeric"
  - "stringhe di formato"
  - "formattazione [.NET Framework], numeri"
  - "formattazione dei numeri [.NET Framework]"
  - "numeri [.NET Framework], formattazione"
  - "stringhe di formato numerico [.NET Framework]"
ms.assetid: 6f74fd32-6c6b-48ed-8241-3c2b86dea5f4
caps.latest.revision: 54
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 54
---
# Stringhe di formato numerico personalizzato
È possibile creare una stringa di formato numerico personalizzata costituita da uno o più identificatori numerici personalizzati, per definire la formattazione dei dati numerici. Viene considerata stringa di formato numerico personalizzata qualsiasi stringa di formato che non rientri nella categoria di [stringa di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md).  
  
 Le stringhe di formato numerico personalizzate sono supportate da alcuni overload del metodo `ToString` di tutti i tipi numerici. È ad esempio possibile fornire una stringa di formato numerico ai metodi <xref:System.Int32.ToString%28System.String%29> e <xref:System.Int32.ToString%28System.String%2CSystem.IFormatProvider%29> del tipo <xref:System.Int32>. Le stringhe di formato numerico personalizzate sono supportate anche dalla [funzionalità di formattazione composta](../../../docs/standard/base-types/composite-formatting.md) di .NET Framework usata da alcuni metodi `Write` e `WriteLine` delle classi <xref:System.Console> e <xref:System.IO.StreamWriter>, dal metodo <xref:System.String.Format%2A?displayProperty=fullName> e dal metodo <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=fullName>.  
  
> [!TIP]
>  È possibile scaricare l'[utilità di formattazione](http://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d), un'applicazione che consente di applicare stringhe di formato a valori numerici o di data e ora e di visualizzare la stringa di risultato.  
  
<a name="table"></a> Nella tabella seguente vengono descritti gli identificatori di formato numerico personalizzati e viene visualizzato l'output di esempio prodotto da ogni identificatore di formato. Vedere la sezione [Note](#NotesCustomFormatting) per informazioni aggiuntive sull'utilizzo di stringhe di formato numerico personalizzate e la sezione [Esempio](#example) per un'illustrazione completa dell'utilizzo.  
  
|Identificatore di formato|Nome|Descrizione|Esempi|  
|-------------------------------|----------|-----------------|------------|  
|"0"|Segnaposto zero|Sostituisce lo zero con la cifra corrispondente, se disponibile; in caso contrario, lo zero viene visualizzato nella stringa di risultato.<br /><br /> Ulteriori informazioni: [Identificatore personalizzato "0"](#Specifier0).|1234.5678 \("00000"\) \-\> 01235<br /><br /> 0.45678 \("0.00", en\-US\) \-\> 0.46<br /><br /> 0.45678 \("0.00", fr\-FR\) \-\> 0,46|  
|"\#"|Segnaposto per cifre|Sostituisce il simbolo "\#" con la cifra corrispondente, se disponibile; in caso contrario, nella stringa di risultato non viene visualizzata nessuna cifra.<br /><br /> Si noti che nella stringa di risultato non viene visualizzata nessuna cifra se la cifra corrispondente nella stringa di input equivale a uno 0 non significativo. Ad esempio, 0003 \("\#\#\#\#"\) \-\> 3.<br /><br /> Ulteriori informazioni: [Identificatore personalizzato "\#"](#SpecifierD).|1234.5678 \("\#\#\#\#\#"\) \-\> 1235<br /><br /> 0.45678 \("\#.\#\#", en\-US\) \-\> .46<br /><br /> 0.45678 \("\#.\#\#", fr\-FR\) \-\> ,46|  
|"."|Separatore decimale|Determina la posizione del separatore decimale nella stringa di risultato.<br /><br /> Altre informazioni: ["." Identificatore personalizzato](#SpecifierPt).|0.45678 \("0.00", en\-US\) \-\> 0.46<br /><br /> 0.45678 \("0.00", fr\-FR\) \-\> 0,46|  
|","|Separatore di gruppi e rappresentazione in scala dei numeri|Viene usato sia come separatore di gruppi che come identificatore di rappresentazione in scala dei numeri. Come separatore di gruppi, inserisce un carattere separatore di gruppi localizzato tra ogni gruppo. Come identificatore di rappresentazione in scala dei numeri, divide un numero per 1000 per ogni virgola specificata.<br /><br /> Ulteriori informazioni: [Identificatore personalizzato ","](#SpecifierTh).|Identificatore del separatore di gruppi:<br /><br /> 2147483647 \("\#\#,\#", en\-US\) \-\> 2,147,483,647<br /><br /> 2147483647 \("\#\#,\#", es\-ES\) \-\> 2.147.483.647<br /><br /> Identificatore di rappresentazione in scala:<br /><br /> 2147483647 \("\#,\#,,", en\-US\) \-\> 2,147<br /><br /> 2147483647 \("\#,\#,,", es\-ES\) \-\> 2.147|  
|"%"|Segnaposto percentuale|Moltiplica un numero per 100 e inserisce un simbolo di percentuale localizzato nella stringa di risultato.<br /><br /> Ulteriori informazioni: [Identificatore personalizzato "%"](#SpecifierPct).|0.3697 \("%\#0.00", en\-US\) \-\> %36.97<br /><br /> 0.3697 \("%\#0.00", el\-GR\) \-\> %36,97<br /><br /> 0.3697 \("\#\#.0 %", en\-US\) \-\> 37.0 %<br /><br /> 0.3697 \("\#\#.0 %", el\-GR\) \-\> 37,0 %|  
|"‰"|Segnaposto per mille|Moltiplica un numero per 1000 e inserisce un simbolo di per mille localizzato nella stringa di risultato.<br /><br /> Ulteriori informazioni: [Identificatore personalizzato "‰"](#SpecifierPerMille).|0.03697 \("\#0.00‰", en\-US\) \-\> 36.97‰<br /><br /> 0.03697 \("\#0.00‰", ru\-RU\) \-\> 36,97‰|  
|"E0"<br /><br /> "E\+0"<br /><br /> "E\-0"<br /><br /> "e0"<br /><br /> "e\+0"<br /><br /> "e\-0"|Notazione esponenziale|Se è seguito da almeno uno 0 \(zero\), formatta il risultato usando la notazione esponenziale. L'utilizzo di "E" o "e" indica se il simbolo dell'esponente nella stringa di risultato deve essere, rispettivamente, maiuscolo o minuscolo. Il numero di zeri che seguono il carattere "E" o "e" determina il numero minimo di cifre nell'esponente. Un segno più \(\+\) indica che l'esponente è sempre preceduto da un carattere di segno. Un segno meno \(\-\) indica che solo gli esponenti negativi sono preceduti da un carattere di segno.<br /><br /> Ulteriori informazioni: [Identificatori personalizzati "E" e "e"](#SpecifierExponent).|987654 \("\#0.0e0"\) \-\> 98.8e4<br /><br /> 1503.92311 \("0.0\#\#e\+00"\) \-\> 1.504e\+03<br /><br /> 1.8901385E\-16 \("0.0e\+00"\) \-\> 1.9e\-16|  
|\\|Carattere di escape|Fa in modo che il carattere successivo venga interpretato come valore letterale anziché come identificatore di formato personalizzato.<br /><br /> Ulteriori informazioni: [Carattere di escape "\\"](#SpecifierEscape).|987654 \("\\\#\#\#00\\\#"\) \-\> \#987654\#|  
|'*string*'<br /><br /> "*string*"|Delimitatore di stringa letterale|Indica che i caratteri contenuti devono essere copiati nella stringa di risultato senza essere modificati.|68 \("\# ' gradi'"\) \-\> 68 gradi<br /><br /> 68 \("\# ' gradi'"\) \-\> 68 gradi|  
|;|Separatore di sezione|Definisce le sezioni con stringhe di formato separate per numeri positivi, negativi e zero.<br /><br /> Ulteriori informazioni: [Separatore di sezione ";"](#SectionSeparator).|12.345 \("\#0.0\#;\(\#0.0\#\);\-\\0\-"\) \-\> 12.35<br /><br /> 0 \("\#0.0\#;\(\#0.0\#\);\-\\0\-"\) \-\> \-0\-<br /><br /> \-12.345 \("\#0.0\#;\(\#0.0\#\);\-\\0\-"\) \-\> \(12.35\)<br /><br /> 12.345 \("\#0.0\#;\(\#0.0\#\)"\) \-\> 12.35<br /><br /> 0 \("\#0.0\#;\(\#0.0\#\)"\) \-\> 0.0<br /><br /> \-12.345 \("\#0.0\#;\(\#0.0\#\)"\) \-\> \(12.35\)|  
|Altro|Tutti gli altri caratteri|Il carattere viene copiato nella stringa di risultato senza alcuna modifica.|68 \("\# °"\) \-\> 68 °|  
  
 Nelle sezioni seguenti vengono fornite informazioni dettagliate su ognuno degli identificatori di formato numerico personalizzati.  
  
<a name="Specifier0"></a>   
## Identificatore personalizzato "0"  
 L'identificatore di formato personalizzato "0" serve come simbolo di segnaposto zero. Se nel valore da formattare è presente una cifra nella posizione in cui nella stringa di formato si trova lo zero, tale cifra viene copiata nella stringa di risultato. In caso contrario, nella stringa di risultato viene visualizzato uno zero. La posizione dello zero più a sinistra prima del separatore decimale e quella dello zero più a destra dopo il separatore decimale determinano l'intervallo di cifre sempre presenti nella stringa di risultato.  
  
 L'identificatore "00" determina l'arrotondamento del valore alla cifra più vicina prima del decimale, in cui viene sempre usato l'arrotondamento a un valore diverso da zero. La formattazione di 34,5 con "00", ad esempio, restituisce come risultato il valore 35.  
  
 Nell'esempio seguente vengono visualizzati diversi valori formattati usando stringhe di formato personalizzate che includono segnaposto zero.  
  
 [!code-cpp[Formatting.Numeric.Custom#1](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#1)]
 [!code-csharp[Formatting.Numeric.Custom#1](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#1)]
 [!code-vb[Formatting.Numeric.Custom#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#1)]  
  
 [Torna alla tabella](#table)  
  
<a name="SpecifierD"></a>   
## Identificatore personalizzato "\#"  
 L'identificatore di formato personalizzato "\#" serve come simbolo di segnaposto per cifre. Se il valore da formattare ha una cifra nella posizione in cui si trova il simbolo "\#" nella stringa di formato, tale cifra viene copiata nella stringa di risultato. In caso contrario, nella stringa di risultato non viene memorizzato alcun valore in tale posizione.  
  
 Si noti che questo identificatore non visualizza mai uno zero, che non è una cifra significativa, anche se lo zero è l'unica cifra della stringa. Viene visualizzato zero solo se si tratta di una cifra significativa nel numero da visualizzare.  
  
 La stringa di formato "\#\#" determina l'arrotondamento del valore alla cifra più vicina prima del decimale, in cui viene sempre usato l'arrotondamento a un valore diverso da zero. La formattazione di 34,5 con "\#\#", ad esempio, restituisce come risultato il valore 35.  
  
 Nell'esempio seguente vengono visualizzati diversi valori formattati usando stringhe di formato personalizzate che includono segnaposto per cifre.  
  
 [!code-cpp[Formatting.Numeric.Custom#2](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#2)]
 [!code-csharp[Formatting.Numeric.Custom#2](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#2)]
 [!code-vb[Formatting.Numeric.Custom#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#2)]  
  
 Per restituire una stringa di risultato in cui le cifre mancanti o gli zeri iniziali vengono sostituiti da spazi, usare la [funzionalità di formattazione composita](../../../docs/standard/base-types/composite-formatting.md) e specificare una lunghezza di campo, come illustrato nell'esempio seguente.  
  
 [!code-cpp[Formatting.Numeric.Custom#12](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/SpaceOrDigit1.cpp#12)]
 [!code-csharp[Formatting.Numeric.Custom#12](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/SpaceOrDigit1.cs#12)]
 [!code-vb[Formatting.Numeric.Custom#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/SpaceOrDigit1.vb#12)]  
  
 [Torna alla tabella](#table)  
  
<a name="SpecifierPt"></a>   
## Identificatore personalizzato "."  
 L'identificatore di formato personalizzato "." inserisce un separatore decimale localizzato nella stringa di risultato. Il primo carattere punto nella stringa di formato determina la posizione del separatore decimale nel valore formattato. Eventuali punti aggiuntivi vengono ignorati.  
  
 Il carattere effettivamente usato come separatore decimale nella stringa di risultato non è sempre un punto, ma viene determinato dalla proprietà <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A> dell'oggetto <xref:System.Globalization.NumberFormatInfo> che controlla la formattazione.  
  
 Nell'esempio seguente viene usato l'identificatore di formato "." per definire la posizione del separatore decimale in alcune stringhe di risultato.  
  
 [!code-cpp[Formatting.Numeric.Custom#3](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#3)]
 [!code-csharp[Formatting.Numeric.Custom#3](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#3)]
 [!code-vb[Formatting.Numeric.Custom#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#3)]  
  
 [Torna alla tabella](#table)  
  
<a name="SpecifierTh"></a>   
## Identificatore personalizzato ","  
 Il carattere "," viene usato sia come separatore di gruppi che come identificatore di rappresentazione in scala dei numeri.  
  
-   Separatore di gruppi: se vengono specificate una o più virgole tra due segnaposto per cifre \(0 o \#\) che formattano le cifre integrali di un numero, viene inserito un carattere di separazione di gruppi tra ogni gruppo di numeri nella parte integrale dell'output.  
  
     Le proprietà <xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator%2A> e <xref:System.Globalization.NumberFormatInfo.NumberGroupSizes%2A> dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente determinano il carattere usato come separatore di gruppi di numeri e la dimensione di ogni gruppo di numeri. Se ad esempio vengono usate la stringa "\#, \#" e le impostazioni cultura invarianti per formattare il numero 1000, l'output sarà "1,000".  
  
-   Identificatore di rappresentazione in scala dei numeri: se vengono specificate una o più virgole immediatamente a sinistra del separatore decimale esplicito o implicito, il numero da formattare viene diviso per 1000 per ogni virgola presente. Se ad esempio viene usata la stringa "0" per formattare il numero 100 milioni, l'output sarà "100".  
  
 È possibile usare gli identificatori del separatore di gruppi e di rappresentazione in scala dei numeri nella stessa stringa di formato. Se ad esempio vengono usate la stringa "\#,0,," e le impostazioni cultura invarianti per formattare il numero un miliardo, l'output sarà "1,000".  
  
 Nell'esempio seguente viene illustrato l'utilizzo della virgola come separatore di gruppi.  
  
 [!code-cpp[Formatting.Numeric.Custom#4](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#4)]
 [!code-csharp[Formatting.Numeric.Custom#4](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#4)]
 [!code-vb[Formatting.Numeric.Custom#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#4)]  
  
 Nell'esempio seguente viene illustrato l'utilizzo della virgola come identificatore di rappresentazione in scala.  
  
 [!code-cpp[Formatting.Numeric.Custom#5](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#5)]
 [!code-csharp[Formatting.Numeric.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#5)]
 [!code-vb[Formatting.Numeric.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#5)]  
  
 [Torna alla tabella](#table)  
  
<a name="SpecifierPct"></a>   
## Identificatore personalizzato "%"  
 La presenza di un segno di percentuale \("%"\) in una stringa di formato fa sì che un numero venga moltiplicato per 100 prima di essere formattato. Il simbolo di percentuale localizzato viene inserito nel numero stesso nella posizione in cui è stato inserito il segno % nella stringa di formato. Il carattere percentuale usato è definito dalla proprietà <xref:System.Globalization.NumberFormatInfo.PercentSymbol%2A> dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente.  
  
 Nell'esempio seguente vengono definite diverse stringhe di formato personalizzate che includono l'identificatore personalizzato "%".  
  
 [!code-cpp[Formatting.Numeric.Custom#6](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#6)]
 [!code-csharp[Formatting.Numeric.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#6)]
 [!code-vb[Formatting.Numeric.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#6)]  
  
 [Torna alla tabella](#table)  
  
<a name="SpecifierPerMille"></a>   
## Identificatore personalizzato "‰"  
 Un carattere per mille \(‰ or \\u2030\) in una stringa di formato fa sì che un numero venga moltiplicato per 1000 prima di essere formattato. Il simbolo per mille appropriato viene inserito nella stringa restituita nella posizione in cui è stato inserito il simbolo ‰ nella stringa di formato. Il carattere per mille usato viene definito dalla proprietà <xref:System.Globalization.NumberFormatInfo.PerMilleSymbol%2A?displayProperty=fullName> dell'oggetto che fornisce informazioni di formattazione specifiche delle impostazioni cultura.  
  
 Nell'esempio seguente viene definita una stringa di formato personalizzata che include l'identificatore personalizzato "‰".  
  
 [!code-cpp[Formatting.Numeric.Custom#9](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#9)]
 [!code-csharp[Formatting.Numeric.Custom#9](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#9)]
 [!code-vb[Formatting.Numeric.Custom#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#9)]  
  
 [Torna alla tabella](#table)  
  
<a name="SpecifierExponent"></a>   
## Identificatori personalizzati "E" e "e"  
 Se nella stringa di formato è presente una delle stringhe "E", "E\+", "E\-", "e", "e\+" o "e\-" immediatamente seguita da almeno uno zero, il numero viene formattato usando la notazione scientifica con una "E" o "e" inserita tra il numero e l'esponente. Il numero di zeri che seguono l'indicatore della notazione scientifica determina il numero minimo di cifre da visualizzare nell'output per l'esponente. I formati "E\+" ed "e\+" indicano che l'esponente deve essere sempre preceduto da un segno più o meno. I formati "E", "E\-", "e" ed "e\-" indicano che solo gli esponenti negativi devono essere preceduti da un carattere di segno.  
  
 Nell'esempio seguente vengono formattati alcuni valori numerici usando gli identificatori per notazione scientifica.  
  
 [!code-cpp[Formatting.Numeric.Custom#7](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#7)]
 [!code-csharp[Formatting.Numeric.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#7)]
 [!code-vb[Formatting.Numeric.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#7)]  
  
 [Torna alla tabella](#table)  
  
<a name="SpecifierEscape"></a>   
## Carattere di escape "\\"  
 I simboli "\#", "0", ".", ",", "%" e "‰" in una stringa di formato vengono interpretati come identificatori di formato anziché come caratteri letterali. A seconda della posizione in una stringa di formato personalizzata, anche la "E" maiuscola e minuscola nonché i simboli \+ e \- possono essere interpretati come identificatori di formato.  
  
 Per impedire che un carattere venga interpretato come un identificatore di formato, è possibile anteporvi una barra rovesciata \(\\\), che rappresenta il carattere di escape. Il carattere di escape indica che il carattere seguente è un valore letterale carattere che deve essere incluso nella stringa di risultato senza modifiche.  
  
 Per includere una barra rovesciata in una stringa dei risultati, è necessario aggiungere un carattere di escape facendolo quindi precedere da un'altra barra rovesciata \(`\\`\).  
  
> [!NOTE]
>  Alcuni compilatori, ad esempio i compilatori C\+\+ e C\#, possono anche interpretare un singolo carattere barra rovesciata come carattere di escape. Per assicurarsi che una stringa venga interpretata correttamente quando viene eseguita la formattazione, è possibile usare il carattere del valore letterale stringa letterale \(carattere @\) prima della stringa in C\# o aggiungere un altro carattere barra rovesciata prima di ogni barra rovesciata in C\# e C\+\+. Nell'esempio C\# seguente vengono illustrati entrambi gli approcci.  
  
 Nell'esempio seguente viene usato il carattere di escape per impedire che durante l'operazione di formattazione i caratteri "\#", "0" e "\\" vengano interpretati come caratteri di escape o identificatori di formato. Negli esempi C\# viene usata una barra rovesciata aggiuntiva per garantire che la barra rovesciata venga interpretata come carattere letterale.  
  
 [!code-cpp[Formatting.Numeric.Custom#11](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/escape1.cpp#11)]
 [!code-csharp[Formatting.Numeric.Custom#11](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/escape1.cs#11)]
 [!code-vb[Formatting.Numeric.Custom#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/escape1.vb#11)]  
  
 [Torna alla tabella](#table)  
  
<a name="SectionSeparator"></a>   
## Separatore di sezione ";"  
 Il punto e virgola \(;\) è un identificatore di formato condizionale che applica una formattazione diversa a un numero, a seconda del fatto che il suo valore sia positivo, negativo o zero. A tale scopo, una stringa di formato personalizzata può contenere un massimo di tre sezioni separate da punti e virgola. Queste sezioni sono descritte nella tabella seguente.  
  
|Numero di sezioni|Descrizione|  
|-----------------------|-----------------|  
|Una|La stringa di formato viene applicata a tutti i valori.|  
|Due|La prima sezione viene applicata ai valori positivi e agli zeri, la seconda ai valori negativi.<br /><br /> Se il numero da formattare è negativo, ma diventa zero dopo l'arrotondamento in base al formato della seconda sezione, lo zero risultante viene formattato in base alla prima sezione.|  
|Tre|La prima sezione viene applicata ai valori positivi, la seconda ai valori negativi e la terza agli zeri.<br /><br /> È possibile che la seconda sezione venga lasciata vuota, ovvero senza alcun valore tra i punti e virgola. In questo caso la prima sezione viene applicata a tutti i valori diversi da zero.<br /><br /> Se il numero da formattare è diverso da zero, ma diventa zero dopo l'arrotondamento in base al formato della prima o della seconda sezione, lo zero risultante viene formattato in base alla terza sezione.|  
  
 Con i separatori di sezione, quando viene formattato il valore finale viene ignorata qualsiasi formattazione preesistente associata a un numero. Quando vengono usati separatori di sezione, ad esempio, i numeri negativi vengono sempre visualizzati senza segno meno. Se si desidera che il valore formattato finale disponga di un segno meno, è opportuno includere il segno meno in modo esplicito nell'ambito dell'identificatore di formato personalizzato.  
  
 Nell'esempio seguente viene usato l'identificatore di formato ";" per formattare numeri positivi, negativi e zero in modo diverso.  
  
 [!code-cpp[Formatting.Numeric.Custom#8](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#8)]
 [!code-csharp[Formatting.Numeric.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#8)]
 [!code-vb[Formatting.Numeric.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#8)]  
  
 [Torna alla tabella](#table)  
  
<a name="NotesCustomFormatting"></a>   
## Note  
  
### Valori infiniti a virgola mobile e NaN  
 Indipendentemente dalla stringa di formato, se il valore di un tipo a virgola mobile <xref:System.Single> o <xref:System.Double> è un numero infinito positivo, un numero infinito negativo o un valore NaN \(Not a Number, non un numero\), la stringa formattata corrisponde al valore della proprietà <xref:System.Globalization.NumberFormatInfo.PositiveInfinitySymbol%2A>, <xref:System.Globalization.NumberFormatInfo.NegativeInfinitySymbol%2A> o <xref:System.Globalization.NumberFormatInfo.NaNSymbol%2A> corrispondente specificata dall'oggetto <xref:System.Globalization.NumberFormatInfo> attualmente applicabile.  
  
### Impostazioni del Pannello di controllo  
 Le impostazioni di **Opzioni internazionali e della lingua** nel Pannello di controllo influiscono sulla stringa risultato prodotta da un'operazione di formattazione. Queste impostazioni vengono usate per inizializzare l'oggetto <xref:System.Globalization.NumberFormatInfo> associato alle impostazioni cultura del thread corrente, che fornisce i valori usati per definire la formattazione. Computer con impostazioni diverse generano stringhe di risultato diverse.  
  
 Se inoltre viene usato il costruttore <xref:System.Globalization.CultureInfo.%23ctor%28System.String%29?displayProperty=fullName> per creare un'istanza di un nuovo oggetto <xref:System.Globalization.CultureInfo> che rappresenta le stesse impostazioni cultura delle impostazioni cultura del sistema correnti, le eventuali personalizzazioni definite tramite **Opzioni internazionali e della lingua** nel Pannello di controllo verranno applicate al nuovo oggetto <xref:System.Globalization.CultureInfo>. È possibile usare il costruttore di <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName> per creare un oggetto <xref:System.Globalization.CultureInfo> che non rifletta le personalizzazioni di un sistema.  
  
### Arrotondamento e stringhe di formato a virgola fissa  
 Per le stringhe di formato a virgola fissa, ovvero stringhe di formato non contenenti caratteri di formato in notazione scientifica, i numeri vengono arrotondati al numero di posizioni decimali corrispondente al numero di segnaposto per cifre a destra del separatore decimale. Se la stringa di formato non contiene alcun separatore decimale, il numero viene arrotondato all'intero più vicino. Se le cifre del numero sono più numerose dei segnaposto per le cifre riportati a sinistra del separatore decimale, le cifre eccedenti vengono copiate nella stringa di risultato immediatamente prima del primo segnaposto per le cifre.  
  
 [Torna alla tabella](#table)  
  
<a name="example"></a>   
## Esempio  
 Nell'esempio seguente vengono illustrate due stringhe di formato numerico personalizzate. In entrambi i casi il segnaposto per le cifre \(`#`\) consente di visualizzare i dati numerici e tutti gli altri caratteri vengono copiati nella stringa di risultato.  
  
 [!code-cpp[Formatting.Numeric.Custom#10](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/example1.cpp#10)]
 [!code-csharp[Formatting.Numeric.Custom#10](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/example1.cs#10)]
 [!code-vb[Formatting.Numeric.Custom#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/example1.vb#10)]  
  
 [Torna alla tabella](#table)  
  
## Vedere anche  
 <xref:System.Globalization.NumberFormatInfo>   
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)   
 [Stringhe di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md)   
 [Procedura: aggiungere zeri iniziali a un numero](../../../docs/standard/base-types/how-to-pad-a-number-with-leading-zeros.md)   
 [Esempio: Utilità di formattazione in .NET Framework 4](http://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d)