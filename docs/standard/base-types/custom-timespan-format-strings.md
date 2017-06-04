---
title: "Stringhe di formato TimeSpan personalizzate | Microsoft Docs"
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
  - "stringhe di formato di intervallo di tempo personalizzate"
  - "stringhe di formato TimeSpan personalizzate"
  - "identificatori di formato, intervallo di tempo personalizzato"
  - "stringhe di formato"
  - "formattazione [.NET Framework], ora"
  - "formattazione [.NET Framework], intervallo di tempo"
ms.assetid: a63ebf55-7269-416b-b4f5-286f6c03bf0e
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Stringhe di formato TimeSpan personalizzate
Una stringa di formato <xref:System.TimeSpan> definisce la rappresentazione di stringa di un valore <xref:System.TimeSpan> risultante da un'operazione di formattazione.  Una stringa di formato personalizzata è costituita da uno o più identificatori di formato <xref:System.TimeSpan> personalizzati unitamente a un numero qualsiasi di caratteri letterali.  Qualsiasi stringa diversa da una [stringa di formato TimeSpan standard](../../../docs/standard/base-types/standard-timespan-format-strings.md) viene interpretata come stringa di formato <xref:System.TimeSpan> personalizzata.  
  
> [!IMPORTANT]
>  Gli identificatori di formato <xref:System.TimeSpan> personalizzati non includono simboli di separatori segnaposto, ad esempio i simboli per separare i giorni dalle ore, le ore dai minuti o i secondi dai secondi frazionari.  È necessario includere questi simboli nella stringa di formato personalizzata come valori letterali stringa.  Ad esempio, `"dd\.hh\:mm"` definisce un punto \(.\) come separatore tra giorni e ore e i due punti \(:\) come separatore tra ore e minuti.  
>   
>  Inoltre, gli identificatori di formato <xref:System.TimeSpan> personalizzati, non includono un simbolo di segno che consenta di distinguere tra intervalli di tempo negativi e positivi.  Per includere un simbolo di segno, è necessario creare una stringa di formato tramite la logica condizionale.  La sezione [Altri caratteri](#Other) include un esempio.  
  
 Le rappresentazioni di stringa di valori <xref:System.TimeSpan> vengono prodotte dalle chiamate agli overload del metodo <xref:System.TimeSpan.ToString%2A?displayProperty=fullName> e dai metodi che supportano la formattazione composita, ad esempio <xref:System.String.Format%2A?displayProperty=fullName>.  Per ulteriori informazioni, vedere [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md) e [Formattazione composita](../../../docs/standard/base-types/composite-formatting.md).  Nell'esempio seguente viene illustrato l'utilizzo delle stringhe di formato personalizzate nelle operazioni di formattazione.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customformatexample1.cs#1)]
 [!code-vb[Conceptual.TimeSpan.Custom#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customformatexample1.vb#1)]  
  
 Le stringhe di formato <xref:System.TimeSpan> personalizzate vengono inoltre utilizzate dai metodi <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> e <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> per definire il formato obbligatorio delle stringhe di input per le operazioni di analisi. L'analisi converte la rappresentazione di stringa di un valore in tale valore. Nell'esempio seguente viene illustrato l'utilizzo delle stringhe di formato standard nelle operazioni di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customparseexample1.cs#2)]
 [!code-vb[Conceptual.TimeSpan.Custom#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customparseexample1.vb#2)]  
  
<a name="table"></a> Nella tabella seguente vengono descritti gli identificatori di formato di data e ora personalizzati.  
  
|Identificatore di formato|Descrizione|Esempio|  
|-------------------------------|-----------------|-------------|  
|"d", "%d"|Numero di giorni interi nell'intervallo di tempo.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "d"](#dSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `%d` \-\-\> "6"<br /><br /> `d\.hh\:mm` \-\-\> "6.14:32"|  
|"dd"\-"dddddddd"|Numero di giorni interi dell'intervallo di tempo, completato da zeri iniziali se necessario.<br /><br /> Ulteriori informazioni: [Identificatori di formato personalizzato "dd"\-"dddddddd"](#ddSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `ddd` \-\-\> "006"<br /><br /> `dd\.hh\:mm` \-\-\> "06.14:32"|  
|"h", "%h"|Numero di ore intere nell'intervallo di tempo non conteggiate come parte di giorni.  Le ore indicate da una sola cifra non hanno uno zero iniziale.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "h"](#hSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `%h` \-\-\> "14"<br /><br /> `hh\:mm` \-\-\> "14:32"|  
|"hh"|Numero di ore intere nell'intervallo di tempo non conteggiate come parte di giorni.  Alle ore indicate da una sola cifra viene aggiunto uno zero iniziale.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "hh"](#hhSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `hh` \-\-\> "14"<br /><br /> `new TimeSpan(6, 8, 32, 17, 685):`<br /><br /> `hh` \-\-\> 08|  
|"m", "%m"|Numero di minuti interi nell'intervallo di tempo non inclusi come parte di ore o giorni.  I minuti indicati da una sola cifra non hanno uno zero iniziale.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "m"](#mSpecifier).|`new TimeSpan(6, 14, 8, 17, 685):`<br /><br /> `%m` \-\-\> "8"<br /><br /> `h\:m` \-\-\> "14:8"|  
|"mm"|Numero di minuti interi nell'intervallo di tempo non inclusi come parte di ore o giorni.  Ai minuti indicati da una sola cifra viene aggiunto uno zero iniziale.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "mm"](#mmSpecifier).|`new TimeSpan(6, 14, 8, 17, 685):`<br /><br /> `mm` \-\-\> "08"<br /><br /> `new TimeSpan(6, 8, 5, 17, 685):`<br /><br /> `d\.hh\:mm\:ss` \-\-\> 6.08:05:17|  
|"s", "%s"|Numero di secondi interi nell'intervallo di tempo non inclusi come parte di ore, giorni o minuti.  I secondi indicati da una sola cifra non hanno uno zero iniziale.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "s"](#sSpecifier).|`TimeSpan.FromSeconds(12.965)`:<br /><br /> `%s` \-\-\> 12<br /><br /> `s\.fff` \-\-\> 12.965|  
|"ss"|Numero di secondi interi nell'intervallo di tempo non inclusi come parte di ore, giorni o minuti.  Ai secondi indicati da una sola cifra viene aggiunto uno zero iniziale.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "ss"](#ssSpecifier).|`TimeSpan.FromSeconds(6.965)`:<br /><br /> `ss` \-\-\> 06<br /><br /> `ss\.fff` \-\-\> 06.965|  
|"f", "%f"|Decimi di secondo in un intervallo di tempo.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "f"](#fSpecifier).|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `f` \-\-\> 8<br /><br /> `ss\.f` \-\-\> 06.8|  
|"ff"|Centesimi di secondo in un intervallo di tempo.<br /><br /> Ulteriori informazioni:[Identificatore di formato personalizzato "ff"](#ffSpecifier).|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `ff` \-\-\> 89<br /><br /> `ss\.ff` \-\-\> 06.89|  
|"fff"|Millisecondi in un intervallo di tempo.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "fff"](#f3Specifier).|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `fff` \-\-\> 895<br /><br /> `ss\.fff` \-\-\> 06.895|  
|"ffff"|Decimillesimi di secondo in un intervallo di tempo.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "ffff"](#f4Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `ffff` \-\-\> 8954<br /><br /> `ss\.ffff` \-\-\> 06.8954|  
|"fffff"|Centomillesimi di secondo in un intervallo di tempo.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "fffff"](#f5Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `fffff` \-\-\> 89543<br /><br /> `ss\.fffff` \-\-\> 06.89543|  
|"ffffff"|Milionesimi di secondo in un intervallo di tempo.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "ffffff"](#f6Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `ffffff` \-\-\> 895432<br /><br /> `ss\.ffffff` \-\-\> 06.895432|  
|"fffffff"|Decimilionesimi di secondo \(o segni di graduazione frazionari\) in un intervallo di tempo.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "fffffff"](#f7Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `fffffff` \-\-\> 8954321<br /><br /> `ss\.fffffff` \-\-\> 06.8954321|  
|"F", "%F"|Decimi di secondo in un intervallo di tempo.  Se la cifra è zero, non viene prodotta alcuna visualizzazione.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "F"](#F_Specifier).|`TimeSpan.Parse("00:00:06.32")`:<br /><br /> `%F`: 3<br /><br /> `TimeSpan.Parse("0:0:3.091")`:<br /><br /> `ss\.F`: 03.|  
|"FF"|Centesimi di secondo in un intervallo di tempo.  Gli zeri finali frazionari o i numeri con due zeri non vengono inclusi.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "FF"](#FF_Specifier).|`TimeSpan.Parse("00:00:06.329")`:<br /><br /> `FF`: 32<br /><br /> `TimeSpan.Parse("0:0:3.101")`:<br /><br /> `ss\.FF`: 03.1|  
|"FFF"|Millisecondi in un intervallo di tempo.  Gli zeri finali frazionari non vengono inclusi.<br /><br /> Ulteriori informazioni:|`TimeSpan.Parse("00:00:06.3291")`:<br /><br /> `FFF`: 329<br /><br /> `TimeSpan.Parse("0:0:3.1009")`:<br /><br /> `ss\.FFF`: 03.1|  
|"FFFF"|Decimillesimi di secondo in un intervallo di tempo.  Gli zeri finali frazionari non vengono inclusi.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "FFFF"](#F4_Specifier).|`TimeSpan.Parse("00:00:06.32917")`:<br /><br /> `FFFFF`: 3291<br /><br /> `TimeSpan.Parse("0:0:3.10009")`:<br /><br /> `ss\.FFFF`: 03.1|  
|"FFFFF"|Centomillesimi di secondo in un intervallo di tempo.  Gli zeri finali frazionari non vengono inclusi.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "FFFFF"](#F5_Specifier).|`TimeSpan.Parse("00:00:06.329179")`:<br /><br /> `FFFFF`: 32917<br /><br /> `TimeSpan.Parse("0:0:3.100009")`:<br /><br /> `ss\.FFFFF`: 03.1|  
|"FFFFFF"|Milionesimi di secondo in un intervallo di tempo.  Gli zeri finali frazionari non vengono visualizzati.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "FFFFFF"](#F6_Specifier).|`TimeSpan.Parse("00:00:06.3291791")`:<br /><br /> `FFFFFF`: 329179<br /><br /> `TimeSpan.Parse("0:0:3.1000009")`:<br /><br /> `ss\.FFFFFF`: 03.1|  
|"FFFFFFF"|Decimilionesimi di secondo in un intervallo di tempo.  Gli zeri finali frazionari o i numeri con sette zeri non vengono visualizzati.<br /><br /> Ulteriori informazioni: [Identificatore di formato personalizzato "FFFFFFF"](#F7_Specifier).|`TimeSpan.Parse("00:00:06.3291791")`:<br /><br /> `FFFFFF`: 3291791<br /><br /> `TimeSpan.Parse("0:0:3.1900000")`:<br /><br /> `ss\.FFFFFF`: 03.19|  
|*'string*'|Delimitatore di stringa letterale.<br /><br /> Ulteriori informazioni: [Altri caratteri](#Other).|`new TimeSpan(14, 32, 17):`<br /><br /> `hh':'mm':'ss` \-\-\> "14:32:17"|  
|\\|Carattere di escape.<br /><br /> Ulteriori informazioni:[Altri caratteri](#Other).|`new TimeSpan(14, 32, 17):`<br /><br /> `hh\:mm\:ss` \-\-\> "14:32:17"|  
|Qualsiasi altro carattere|Qualsiasi altro carattere senza codice di escape viene interpretato come identificatore di formato personalizzato.<br /><br /> Ulteriori informazioni: [Altri caratteri](#Other).|`new TimeSpan(14, 32, 17):`<br /><br /> `hh\:mm\:ss` \-\-\> "14:32:17"|  
  
<a name="dSpecifier"></a>   
## Identificatore di formato personalizzato "d"  
 L'identificatore di formato personalizzato "d" restituisce il valore della proprietà <xref:System.TimeSpan.Days%2A?displayProperty=fullName> che rappresenta il numero di giorni interi nell'intervallo di tempo.  L'output restituito corrisponde al numero completo di giorni in un valore <xref:System.TimeSpan>, anche se il valore è costituito da più di una cifra.  Se il valore della proprietà <xref:System.TimeSpan.Days%2A?displayProperty=fullName> è zero, l'output dell'identificatore è "0".  
  
 Se l'identificatore di formato personalizzato "d" viene utilizzato da solo, specificare "%d" per evitare che venga interpretato erroneamente come stringa di formato standard.  Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#3)]
 [!code-vb[Conceptual.TimeSpan.Custom#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#3)]  
  
 Nell'esempio seguente viene illustrato l'utilizzo dell'identificatore di formato personalizzato "d".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#4)]
 [!code-vb[Conceptual.TimeSpan.Custom#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#4)]  
  
 [Torna alla tabella](#table)  
  
<a name="ddSpecifier"></a>   
## Identificatori di formato personalizzati "dd"\-"dddddddd"  
 Gli identificatori di formato personalizzati "dd", "ddd", "dddd", "ddddd", "dddddd", "ddddddd" e "dddddddd" restituiscono il valore della proprietà <xref:System.TimeSpan.Days%2A?displayProperty=fullName> che rappresenta il numero di giorni interi nell'intervallo di tempo.  
  
 La stringa di output include un numero minimo di cifre specificato dal numero di caratteri "d" presenti nell'identificatore di formato e viene completata con zeri iniziali se necessario.  Se le cifre nel numero di giorni superano il numero di caratteri "d" dell'identificatore di formato, nella stringa di risultato viene restituito il numero completo di giorni.  
  
 Nell'esempio seguente vengono utilizzati questi identificatori di formato per visualizzare la rappresentazione di stringa di due valori <xref:System.TimeSpan>.  Il valore del componente giorni del primo intervallo di tempo è zero, mentre il valore del componente giorni del secondo intervallo è 365.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#5)]
 [!code-vb[Conceptual.TimeSpan.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#5)]  
  
 [Torna alla tabella](#table)  
  
<a name="hSpecifier"></a>   
## Identificatore di formato personalizzato "h"  
 L'identificatore di formato personalizzato "h" restituisce il valore della proprietà <xref:System.TimeSpan.Hours%2A?displayProperty=fullName>, che rappresenta il numero di ore intere nell'intervallo di tempo non conteggiate come parte del relativo componente giorno.  Se il valore della proprietà <xref:System.TimeSpan.Hours%2A?displayProperty=fullName> è compreso tra 0 e 9 restituisce un valore di stringa a una cifra; se il valore della proprietà <xref:System.TimeSpan.Hours%2A?displayProperty=fullName> è compreso tra 10 e 23 restituisce un valore di stringa a due cifre.  
  
 Se l'identificatore di formato personalizzato "h" viene utilizzato da solo, specificare "%h" per evitare che venga interpretato erroneamente come stringa di formato standard.  Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#6)]
 [!code-vb[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#6)]  
  
 Normalmente, in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni.  Utilizzare invece l'identificatore di formato personalizzato "%h" per interpretare la stringa numerica come numero di ore.  Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#8)]
 [!code-vb[Conceptual.TimeSpan.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#8)]  
  
 Nell'esempio seguente viene illustrato l'utilizzo dell'identificatore di formato personalizzato "h".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#7)]
 [!code-vb[Conceptual.TimeSpan.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#7)]  
  
 [Torna alla tabella](#table)  
  
<a name="hhSpecifier"></a>   
## Identificatore di formato personalizzato "hh"  
 L'identificatore di formato personalizzato "hh" restituisce il valore della proprietà <xref:System.TimeSpan.Hours%2A?displayProperty=fullName>, che rappresenta il numero di ore intere nell'intervallo di tempo non conteggiate come parte del relativo componente giorno.  Per valori compresi tra 0 e 9, la stringa di output include uno zero iniziale.  
  
 Normalmente, in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni.  Utilizzare invece l'identificatore di formato personalizzato "hh" per interpretare la stringa numerica come numero di ore.  Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#9)]
 [!code-vb[Conceptual.TimeSpan.Custom#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#9)]  
  
 Nell'esempio seguente viene illustrato l'utilizzo dell'identificatore di formato personalizzato "hh".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#10)]
 [!code-vb[Conceptual.TimeSpan.Custom#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#10)]  
  
 [Torna alla tabella](#table)  
  
<a name="mSpecifier"></a>   
## Identificatore di formato personalizzato "m"  
 L'identificatore di formato personalizzato "m" restituisce il valore della proprietà <xref:System.TimeSpan.Minutes%2A?displayProperty=fullName>, che rappresenta il numero di minuti interi nell'intervallo di tempo non conteggiati come parte del relativo componente giorno.  Se il valore della proprietà <xref:System.TimeSpan.Minutes%2A?displayProperty=fullName> è compreso tra 0 e 9 restituisce un valore di stringa a una cifra; se il valore della proprietà <xref:System.TimeSpan.Minutes%2A?displayProperty=fullName> è compreso tra 10 e 59 restituisce un valore di stringa a due cifre.  
  
 Se l'identificatore di formato personalizzato "m" viene utilizzato da solo, specificare "%m" per evitare che venga interpretato erroneamente come stringa di formato standard.  Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#6)]
 [!code-vb[Conceptual.TimeSpan.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#6)]  
  
 Normalmente, in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni.  Utilizzare invece l'identificatore di formato personalizzato "%m" per interpretare la stringa numerica come numero di minuti.  Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#11)]
 [!code-vb[Conceptual.TimeSpan.Custom#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#11)]  
  
 Nell'esempio seguente viene illustrato l'utilizzo dell'identificatore di formato personalizzato "m".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#12)]
 [!code-vb[Conceptual.TimeSpan.Custom#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#12)]  
  
 [Torna alla tabella](#table)  
  
<a name="mmSpecifier"></a>   
## Identificatore di formato personalizzato "mm"  
 L'identificatore di formato personalizzato "mm" restituisce il valore della proprietà <xref:System.TimeSpan.Minutes%2A?displayProperty=fullName>, che rappresenta il numero di minuti interi nell'intervallo di tempo non inclusi come parte del relativo componente giorni o ore.  Per valori compresi tra 0 e 9, la stringa di output include uno zero iniziale.  
  
 Normalmente, in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni.  Utilizzare invece l'identificatore di formato personalizzato "mm" per interpretare la stringa numerica come numero di minuti.  Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#13)]
 [!code-vb[Conceptual.TimeSpan.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#13)]  
  
 Nell'esempio seguente viene illustrato l'utilizzo dell'identificatore di formato personalizzato "mm".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#14)]
 [!code-vb[Conceptual.TimeSpan.Custom#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#14)]  
  
 [Torna alla tabella](#table)  
  
<a name="sSpecifier"></a>   
## Identificatore di formato personalizzato "s"  
 L'identificatore di formato personalizzato "s" restituisce il valore della proprietà <xref:System.TimeSpan.Seconds%2A?displayProperty=fullName>, che rappresenta il numero di secondi interi nell'intervallo di tempo non inclusi come parte del relativo componente giorni, ore o minuti.  Se il valore della proprietà <xref:System.TimeSpan.Seconds%2A?displayProperty=fullName> è compreso tra 0 e 9 restituisce un valore di stringa a una cifra; se il valore della proprietà <xref:System.TimeSpan.Seconds%2A?displayProperty=fullName> è compreso tra 10 e 59 restituisce un valore di stringa a due cifre.  
  
 Se l'identificatore di formato personalizzato "s" viene utilizzato da solo, specificare "%s" per evitare che venga interpretato erroneamente come stringa di formato standard.  Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#15)]
 [!code-vb[Conceptual.TimeSpan.Custom#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#15)]  
  
 Normalmente, in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni.  Utilizzare invece l'identificatore di formato personalizzato "%s" per interpretare la stringa numerica come numero di secondi.  Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#17)]
 [!code-vb[Conceptual.TimeSpan.Custom#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#17)]  
  
 Nell'esempio seguente viene illustrato l'utilizzo dell'identificatore di formato personalizzato "s".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#16)]
 [!code-vb[Conceptual.TimeSpan.Custom#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#16)]  
  
 [Torna alla tabella](#table)  
  
<a name="ssSpecifier"></a>   
## Identificatore di formato personalizzato "ss"  
 L'identificatore di formato personalizzato "ss" restituisce il valore della proprietà <xref:System.TimeSpan.Seconds%2A?displayProperty=fullName>, che rappresenta il numero di secondi interi nell'intervallo di tempo non inclusi come parte del relativo componente giorni, ore o minuti.  Per valori compresi tra 0 e 9, la stringa di output include uno zero iniziale.  
  
 Normalmente, in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni.  Utilizzare invece l'identificatore di formato personalizzato "ss" per interpretare la stringa numerica come numero di secondi.  Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#18)]
 [!code-vb[Conceptual.TimeSpan.Custom#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#18)]  
  
 Nell'esempio seguente viene illustrato l'utilizzo dell'identificatore di formato personalizzato "ss".  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#19)]
 [!code-vb[Conceptual.TimeSpan.Custom#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#19)]  
  
 [Torna alla tabella](#table)  
  
<a name="fSpecifier"></a>   
## Identificatore di formato personalizzato "f"  
 L'identificatore di formato personalizzato "f" restituisce i decimi di secondo in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la stringa di input deve contenere esattamente una cifra frazionaria.  
  
 Se l'identificatore di formato personalizzato "f" viene utilizzato da solo, specificare "%f" per evitare che venga interpretato erroneamente come stringa di formato standard.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "f" per visualizzare i decimi di secondo in un valore <xref:System.TimeSpan>. "f" viene utilizzato prima come unico identificatore di formato, quindi viene utilizzato in combinazione con l'identificatore "s" in una stringa di formato personalizzata.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="ffSpecifier"></a>   
## Identificatore di formato personalizzato "ff"  
 L'identificatore di formato personalizzato "ff" restituisce i centesimi di secondo in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la stringa di input deve contenere esattamente due cifre frazionarie.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "ff" per visualizzare i centesimi di secondo in un valore <xref:System.TimeSpan>. "ff" viene utilizzato prima come unico identificatore di formato, quindi viene utilizzato in combinazione con l'identificatore "s" in una stringa di formato personalizzata.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="f3Specifier"></a>   
## Identificatore di formato personalizzato "fff"  
 L'identificatore di formato personalizzato "ff" \(con tre caratteri "f"\) restituisce i millisecondi in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la stringa di input deve contenere esattamente tre cifre frazionarie.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "fff" per visualizzare i millisecondi in un valore <xref:System.TimeSpan>. "fff" viene utilizzato prima come unico identificatore di formato, quindi viene utilizzato in combinazione con l'identificatore "s" in una stringa di formato personalizzata.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="f4Specifier"></a>   
## Identificatore di formato personalizzato "ffff"  
 L'identificatore di formato personalizzato "ffff" \(con quattro caratteri "f"\) restituisce i decimillesimi di secondo in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la stringa di input deve contenere esattamente quattro cifre frazionarie.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "ffff" per visualizzare i decimillesimi di secondo in un valore <xref:System.TimeSpan>. "ffff" viene utilizzato prima come unico identificatore di formato, quindi viene utilizzato in combinazione con l'identificatore "s" in una stringa di formato personalizzata.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="f5Specifier"></a>   
## Identificatore di formato personalizzato "fffff"  
 L'identificatore di formato personalizzato "fffff" \(con cinque caratteri "f"\) restituisce i centomillesimi di secondo in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la stringa di input deve contenere esattamente cinque cifre frazionarie.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "fffff" per visualizzare i centomillesimi di secondo in un valore <xref:System.TimeSpan>. "fffff" viene utilizzato prima come unico identificatore di formato, quindi viene utilizzato in combinazione con l'identificatore "s" in una stringa di formato personalizzata.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="f6Specifier"></a>   
## Identificatore di formato personalizzato "ffffff"  
 L'identificatore di formato personalizzato "ffffff" \(con sei caratteri "f"\) restituisce i milionesimi di secondo in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la stringa di input deve contenere esattamente sei cifre frazionarie.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "ffffff" per visualizzare i milionesimi di secondo in un valore <xref:System.TimeSpan>.  Viene utilizzato prima come unico identificatore di formato, quindi viene utilizzato in combinazione con l'identificatore "s" in una stringa di formato personalizzata.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="f7Specifier"></a>   
## Identificatore di formato personalizzato "fffffff"  
 L'identificatore di formato personalizzato "fffffff" \(con sette caratteri "f"\) restituisce i decimilionesimi di secondo \(o il numero frazionario di segni di graduazione\) in un intervallo di tempo.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la stringa di input deve contenere esattamente sette cifre frazionarie.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "fffffff" per visualizzare il numero frazionario di segni di graduazione in un valore <xref:System.TimeSpan>.  Viene utilizzato prima come unico identificatore di formato, quindi viene utilizzato in combinazione con l'identificatore "s" in una stringa di formato personalizzata.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
 [!code-vb[Conceptual.TimeSpan.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]  
  
 [Torna alla tabella](#table)  
  
<a name="F_Specifier"></a>   
## Identificatore di formato personalizzato "F"  
 L'identificatore di formato personalizzato "F" restituisce i decimi di secondo in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  Se il valore dei decimi di secondo dell'intervallo di tempo è zero, non viene incluso nella stringa del risultato.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la presenza dei decimi della cifra dei secondi è facoltativa.  
  
 Se l'identificatore di formato personalizzato "F" viene utilizzato da solo, specificare "%F" per evitare che venga interpretato erroneamente come stringa di formato standard.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "F" per visualizzare i decimi di secondo in un valore <xref:System.TimeSpan>.  Questo identificatore di formato personalizzato viene inoltre utilizzato in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#21)]
 [!code-vb[Conceptual.TimeSpan.Custom#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#21)]  
  
 [Torna alla tabella](#table)  
  
<a name="FF_Specifier"></a>   
## Identificatore di formato personalizzato "FF"  
 L'identificatore di formato personalizzato "FF" restituisce i centesimi di secondo in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la presenza dei decimi e dei centesimi della cifra dei secondi è facoltativa.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "FF" per visualizzare i centesimi di secondo in un valore <xref:System.TimeSpan>.  Questo identificatore di formato personalizzato viene inoltre utilizzato in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#22)]
 [!code-vb[Conceptual.TimeSpan.Custom#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#22)]  
  
 [Torna alla tabella](#table)  
  
<a name="F3_Specifier"></a>   
## Identificatore di formato personalizzato "FFF"  
 L'identificatore di formato personalizzato "FFF" \(con tre caratteri "F"\) restituisce i millisecondi in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la presenza dei decimi, dei centesimi e dei millesimi della cifra dei secondi è facoltativa.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "FFF" per visualizzare i millesimi di secondo in un valore <xref:System.TimeSpan>.  Questo identificatore di formato personalizzato viene inoltre utilizzato in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#23)]
 [!code-vb[Conceptual.TimeSpan.Custom#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#23)]  
  
 [Torna alla tabella](#table)  
  
<a name="F4_Specifier"></a>   
## Identificatore di formato personalizzato "FFFF"  
 L'identificatore di formato personalizzato "FFFF" \(con quattro caratteri "F"\) restituisce i decimillesimi di secondo in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la presenza dei decimi, dei centesimi, dei millesimi e dei decimillesimi della cifra dei secondi è facoltativa.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "FFFF" per visualizzare i decimillesimi di secondo in un valore <xref:System.TimeSpan>.  L'identificatore di formato personalizzato "FFFF" viene inoltre utilizzato in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#24](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#24)]
 [!code-vb[Conceptual.TimeSpan.Custom#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#24)]  
  
 [Torna alla tabella](#table)  
  
<a name="F5_Specifier"></a>   
## Identificatore di formato personalizzato "FFFFF"  
 L'identificatore di formato personalizzato "FFFFF" \(con cinque caratteri "F"\) restituisce i centomillesimi di secondo in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la presenza dei decimi, dei centesimi, dei millesimi, dei decimillesimi e dei centomillesimi della cifra dei secondi è facoltativa.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "FFFFF" per visualizzare i centomillesimi di secondo in un valore <xref:System.TimeSpan>.  L'identificatore di formato personalizzato "FFFFF" viene inoltre utilizzato in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#25](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#25)]
 [!code-vb[Conceptual.TimeSpan.Custom#25](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#25)]  
  
 [Torna alla tabella](#table)  
  
<a name="F6_Specifier"></a>   
## Identificatore di formato personalizzato "FFFFFF"  
 L'identificatore di formato personalizzato "FFFFFF" \(con sei caratteri "F"\) restituisce i milionesimi di secondo in un intervallo di tempo.  In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata.  Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la presenza dei decimi, dei centesimi, dei millesimi, dei decimillesimi, dei centomillesimi e dei milionesimi della cifra dei secondi è facoltativa.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "FFFFFF" per visualizzare i milionesimi di secondo in un valore <xref:System.TimeSpan>.  Questo identificatore di formato personalizzato viene inoltre utilizzato in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#26](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#26)]
 [!code-vb[Conceptual.TimeSpan.Custom#26](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#26)]  
  
 [Torna alla tabella](#table)  
  
<a name="F7_Specifier"></a>   
## Identificatore di formato personalizzato "FFFFFFF"  
 L'identificatore di formato personalizzato "FFFFFFF" \(con sette caratteri "F"\) restituisce i decimilionesimi di secondo \(o il numero frazionario di segni di graduazione\) in un intervallo di tempo.  Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato.  In un'operazione di analisi che chiama il metodo <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName> o <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName> la presenza delle sette cifre frazionarie nella stringa di input è facoltativa.  
  
 Nell'esempio seguente viene utilizzato l'identificatore di formato personalizzato "FFFFFFF" per visualizzare le parti frazionarie di un secondo in un valore <xref:System.TimeSpan>.  Questo identificatore di formato personalizzato viene inoltre utilizzato in un'operazione di analisi.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#27](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#27)]
 [!code-vb[Conceptual.TimeSpan.Custom#27](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#27)]  
  
 [Torna alla tabella](#table)  
  
<a name="Other"></a>   
## Altri caratteri  
 Qualsiasi altro carattere senza codice di escape in una stringa di formato, incluso un carattere di spazio vuoto, viene interpretato come identificatore di formato personalizzato.  Nella maggior parte dei casi la presenza di qualsiasi altro carattere senza codice di escape restituisce un oggetto <xref:System.FormatException>.  
  
 È possibile includere un carattere letterale in una stringa di formato in due modi:  
  
-   Racchiuderlo tra virgolette singole \(delimitatore di stringa letterale\).  
  
-   Inserire prima del carattere una barra rovesciata \("\\"\), interpretata come carattere di escape.  In C\#, pertanto, la stringa di formato deve essere racchiusa tra virgolette e preceduta da @ o il carattere letterale deve essere preceduto da una barra rovesciata aggiuntiva.  
  
     In alcuni casi, potrebbe essere necessario utilizzare la logica condizionale per includere un letterale forzato in una stringa di formato.  Nell'esempio seguente viene utilizzata la logica condizionale per includere un simbolo di segno per intervalli di tempo negativi.  
  
     [!code-csharp[Conceptual.TimeSpan.Custom#29](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/negativevalues1.cs#29)]
     [!code-vb[Conceptual.TimeSpan.Custom#29](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/negativevalues1.vb#29)]  
  
 In .NET Framework non viene definita una grammatica per i separatori negli intervalli di tempo.  I separatori tra giorni e ore, ore e minuti, minuti e secondi e secondi e frazioni di secondo devono pertanto essere trattati come valori letterali carattere in una stringa di formato.  
  
 Nell'esempio seguente vengono utilizzati sia il carattere di escape sia la virgoletta singola per definire una stringa di formato personalizzata che include la parola "minuti" nella stringa di output.  
  
 [!code-csharp[Conceptual.TimeSpan.Custom#28](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/literal1.cs#28)]
 [!code-vb[Conceptual.TimeSpan.Custom#28](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/literal1.vb#28)]  
  
 [Torna alla tabella](#table)  
  
## Vedere anche  
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)   
 [Stringhe di formato TimeSpan standard](../../../docs/standard/base-types/standard-timespan-format-strings.md)