---
title: "Linguaggio di espressioni regolari - Riferimento rapido | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "VS.RegularExpressionBuilder"
helpviewer_keywords: 
  - "espressioni regolari di .NET Framework, elementi di linguaggio"
  - "scheda di riferimento grafico"
  - "analisi di testo con espressioni regolari, elementi di linguaggio"
  - "corrispondenza al modello con espressioni regolari, elementi di linguaggio"
  - "regex (scheda di riferimento grafico)"
  - "espressioni regolari [.NET Framework]"
  - "espressioni regolari, elementi di linguaggio"
  - "ricerca con espressioni regolari, elementi di linguaggio"
ms.assetid: 930653a6-95d2-4697-9d5a-52d11bb6fd4c
caps.latest.revision: 56
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 56
---
# Linguaggio di espressioni regolari - Riferimento rapido
<a name="top"></a> Un'espressione regolare è un modello per il quale il motore delle espressioni regolari tenta di trovare una corrispondenza nel testo di input. Un modello è costituito da uno o più i valori letterali carattere, operatori o costrutti.  Per una breve introduzione, vedere [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md).  
  
 In ogni sezione di questa guida di riferimento rapido viene elencata una categoria specifica di caratteri, operatori e costrutti che è possibile usare per definire le espressioni regolari:  
  
 [Escape di caratteri](#character_escapes)  
 [Classi di caratteri](#character_classes)  
 [Ancoraggi](#atomic_zerowidth_assertions)  
 [Costrutti di raggruppamento](#grouping_constructs)  
 [Quantificatori](#quantifiers)  
 [Costrutti di backreference](#backreference_constructs)  
 [Costrutti di alternanza](#alternation_constructs)  
 [Sostituzioni](#substitutions)  
 [Opzioni di espressioni regolari](#options)  
 [Costrutti vari](#miscellaneous_constructs)  
  
 Queste informazioni sono disponibili in due formati scaricabili e stampabili come riferimento:  
  
 [Download in formato Word \(.docx\)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)  
[Download in formato PDF \(.pdf\)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)  
  
<a name="character_escapes"></a>   
## Caratteri di escape  
 Il carattere barra rovesciata \(\\\) in un'espressione regolare indica che il carattere successivo è un carattere speciale \(come illustrato nella tabella seguente\) oppure deve essere interpretato letteralmente. Per altre informazioni, vedere [Caratteri di escape](../../../docs/standard/base-types/character-escapes-in-regular-expressions.md).  
  
|Caratteri di escape|Descrizione|Criterio|Corrispondenze|  
|-------------------------|-----------------|--------------|--------------------|  
|`\a`|Trova la corrispondenza di un carattere di controllo del segnale acustico di avviso, \\u0007.|`\a`|"\\u0007" in "Error\!" \+ '\\u0007'|  
|`\b`|In una classe di caratteri, trova la corrispondenza di un carattere backspace, \\u0008.|`[\b]{3,}`|"\\b\\b\\b\\b" in "\\b\\b\\b\\b"|  
|`\t`|Trova la corrispondenza di un carattere di tabulazione, \\u0009.|`(\w+)\t`|"item1\\t", "item2\\t" in "item1\\titem2\\t"|  
|`\r`|Trova la corrispondenza di un carattere di ritorno a capo, \\u000D. \(`\r` non equivale al carattere di nuova riga, `\n`\).|`\r\n(\w+)`|"\\r\\nThese" in "\\r\\nThese are\\ntwo lines."|  
|`\v`|Trova la corrispondenza di un carattere di tabulazione verticale, \\u000B.|`[\v]{2,}`|"\\v\\v\\v" in "\\v\\v\\v"|  
|`\f`|Trova la corrispondenza di un carattere di avanzamento carta, \\u000C.|`[\f]{2,}`|"\\f\\f\\f" in "\\f\\f\\f"|  
|`\n`|Trova la corrispondenza di una nuova riga, \\u000A.|`\r\n(\w+)`|"\\r\\nThese" in "\\r\\nThese are\\ntwo lines."|  
|`\e`|Trova la corrispondenza di un carattere di escape, \\u001B.|`\e`|"\\x001B" in "\\x001B"|  
|`\` *nnn*|Usa la rappresentazione ottale per specificare un carattere \(*nnn* è costituito da un massimo di tre cifre\).|`\w\040\w`|"a b", "c d" in<br /><br /> "a bc d"|  
|`\x` *nn*|Usa la rappresentazione esadecimale per specificare un carattere \(*nn* è costituito da esattamente due cifre\).|`\w\x20\w`|"a b", "c d" in<br /><br /> "a bc d"|  
|`\c` *X*<br /><br /> `\c` *x*|Trova la corrispondenza con il carattere di controllo ASCII specificato da *X* o *x*, dove *X* o *x* è la lettera del carattere di controllo.|`\cC`|"\\x0003" in "\\x0003" \(Ctrl\-C\)|  
|`\u` *nnnn*|Trova la corrispondenza di un carattere Unicode usando una rappresentazione esadecimale \(esattamente quattro cifre, come rappresentate da *nnnn*\).|`\w\u0020\w`|"a b", "c d" in<br /><br /> "a bc d"|  
|`\`|Quando è seguito da un carattere non riconosciuto come carattere di escape, in questa e in altre tabelle del presente argomento, trova la corrispondenza di tale carattere. Ad esempio, `\*` corrisponde a `\x2A` e `\.` corrisponde a `\x2E`. Questo consente al motore delle espressioni regolari di distinguere tra elementi del linguaggio \(ad esempio, \* o ?\) e i valori letterali del carattere \(rappresentati da `\*` o `\?`\).|`\d+[\+-x\*]\d+`|"2\+2" e "3\*9" in "\(2\+2\) \* 3\*9"|  
  
 [Torna all'inizio](#top)  
  
<a name="character_classes"></a>   
## Classi di caratteri  
 Una classe di caratteri trova la corrispondenza con uno qualsiasi di un set di caratteri. Le classi di caratteri includono gli elementi del linguaggio elencati nella tabella seguente. Per altre informazioni, vedere [Classi di caratteri](../../../docs/standard/base-types/character-classes-in-regular-expressions.md).  
  
|Classe di caratteri|Descrizione|Criterio|Corrispondenze|  
|-------------------------|-----------------|--------------|--------------------|  
|`[` *gruppo\_caratteri* `]`|Trova la corrispondenza con qualsiasi carattere singolo in *gruppo\_caratteri*. Per impostazione predefinita, viene effettuata la distinzione tra maiuscole e minuscole.|`[ae]`|"a" in "gray"<br /><br /> "a", "e" in "lane"|  
|`[^` *gruppo\_caratteri* `]`|Negazione: corrisponde a qualsiasi carattere singolo non incluso in *gruppo\_caratteri*. Per impostazione predefinita, i caratteri in *gruppo\_caratteri* rilevano la distinzione tra maiuscole e minuscole.|`[^aei]`|"r", "g", "n" in "reign"|  
|`[` *primo* `-` *last* `]`|Intervallo di caratteri: trova la corrispondenza di qualsiasi carattere singolo nell'intervallo da *primo* a *ultimo*.|`[A-Z]`|"A", "B" in "AB123"|  
|`.`|Carattere jolly: trova la corrispondenza di qualsiasi carattere singolo ad eccezione di "\\n".<br /><br /> Per confrontare un carattere punto di valore letterale \(. o `\u002E`\), è necessario farlo precedere da un carattere di escape \(`\.`\).|`a.e`|"ave" in "nave"<br /><br /> "ate" in "water"|  
|`\p{` *nome* `}`|Trova la corrispondenza con qualsiasi carattere singolo incluso nel blocco denominato o nella categoria generale Unicode specificato in *nome*.|`\p{Lu}`<br /><br /> `\p{IsCyrillic}`|"C", "L" in "City Lights"<br /><br /> "Д", "Ж" in "ДЖem"|  
|`\P{` *nome* `}`|Trova la corrispondenza di qualsiasi carattere singolo non incluso nel blocco denominato o nella categoria generale Unicode specificato in *nome*.|`\P{Lu}`<br /><br /> `\P{IsCyrillic}`|"i", "t", "y" in "City"<br /><br /> "e", "m" in "ДЖem"|  
|`\w`|Trova la corrispondenza di qualsiasi carattere alfabetico.|`\w`|"I", "D", "A", "1", "3" in "ID A1.3"|  
|`\W`|Trova la corrispondenza di qualsiasi carattere non alfabetico.|`\W`|" ", "." in "ID A1.3"|  
|`\s`|Trova la corrispondenza di qualsiasi carattere di spazio.|`\w\s`|"D " in "ID A1.3"|  
|`\S`|Trova la corrispondenza di qualsiasi carattere diverso da uno spazio.|`\s\S`|" \_" in "int \_\_ctr"|  
|`\d`|Trova la corrispondenza di qualsiasi cifra decimale.|`\d`|"4" in "4 \= IV"|  
|`\D`|Trova la corrispondenza con qualsiasi carattere diverso da una cifra decimale.|`\D`|" ", "\=", " ", "I", "V" in "4 \= IV"|  
  
 [Torna all'inizio](#top)  
  
<a name="atomic_zerowidth_assertions"></a>   
## Punti di ancoraggio  
 Gli ancoraggi, o asserzioni atomiche di larghezza zero, determinano l'esito della ricerca di una corrispondenza in base alla posizione corrente nella stringa, ma non comportano l'avanzamento del motore nella stringa o l'utilizzo di caratteri. I metacaratteri elencati nella tabella seguente sono ancoraggi. Per altre informazioni, vedere [Ancoraggi](../../../docs/standard/base-types/anchors-in-regular-expressions.md).  
  
|Asserzione|Descrizione|Criterio|Corrispondenze|  
|----------------|-----------------|--------------|--------------------|  
|`^`|La corrispondenza deve iniziare all'inizio della stringa o della riga.|`^\d{3}`|"901" in<br /><br /> "901\-333\-"|  
|`$`|La corrispondenza deve verificarsi alla fine della stringa o prima di `\n` alla fine della riga o della stringa.|`-\d{3}$`|"\-333" in<br /><br /> "\-901\-333"|  
|`\A`|La corrispondenza deve verificarsi all'inizio della stringa.|`\A\d{3}`|"901" in<br /><br /> "901\-333\-"|  
|`\Z`|La corrispondenza deve verificarsi alla fine della stringa o prima di `\n` alla fine della stringa.|`-\d{3}\Z`|"\-333" in<br /><br /> "\-901\-333"|  
|`\z`|La corrispondenza deve verificarsi alla fine della stringa.|`-\d{3}\z`|"\-333" in<br /><br /> "\-901\-333"|  
|`\G`|La corrispondenza deve verificarsi nel punto in cui è terminata la corrispondenza precedente.|`\G\(\d\)`|"\(1\)", "\(3\)", "\(5\)" in "\(1\)\(3\)\(5\)\[7\]\(9\)"|  
|`\b`|La corrispondenza deve verificarsi sul limite tra un carattere `\w` \(alfanumerico\) e un carattere `\W` \(non alfanumerico\).|`\b\w+\s\w+\b`|"them theme", "them them" in "them theme them them"|  
|`\B`|La corrispondenza non deve verificarsi su un limite `\b`.|`\Bend\w*\b`|"ends", "ender" in "end sends endure lender"|  
  
 [Torna all'inizio](#top)  
  
<a name="grouping_constructs"></a>   
## Costrutti di raggruppamento  
 I costrutti di raggruppamento delineano sottoespressioni di un'espressione regolare e in genere acquisiscono sottostringhe di una stringa di input. I costrutti di raggruppamento includono gli elementi del linguaggio elencati nella tabella seguente. Per altre informazioni, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
|Costrutto di raggruppamento|Descrizione|Criterio|Corrispondenze|  
|---------------------------------|-----------------|--------------|--------------------|  
|`(` *sottoespressione* `)`|Acquisisce la sottoespressione corrispondente e le assegna un numero ordinale in base uno.|`(\w)\1`|"ee" in "deep"|  
|`(?<` *nome* `>` *sottoespressione*`)`|Acquisisce la sottoespressione corrispondente in un gruppo denominato.|`(?<double>\w)\k<double>`|"ee" in "deep"|  
|`(?<` *nome1* `-` *nome2* `>` *sottoespressione*`)`|Definisce una definizione di gruppo di bilanciamento Per altre informazioni, vedere la sezione "Definizioni di gruppo di bilanciamento" in [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).|`(((?'Open'\()[^\(\)]*)+((?'Close-Open'\))[^\(\)]*)+)*(?(Open)(?!))$`|"\(\(1\-3\)\*\(3\-1\)\)" in "3\+2^\(\(1\-3\)\*\(3\-1\)\)"|  
|`(?:` *sottoespressione*`)`|Definisce un gruppo di non acquisizione.|`Write(?:Line)?`|"WriteLine" in "Console.WriteLine\(\)"<br /><br /> "Write" in "Console.Write\(value\)"|  
|`(?imnsx-imnsx:` *sottoespressione*`)`|Applica o disabilita le opzioni specificate in *sottoespressione*. Per altre informazioni, vedere [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).|`A\d{2}(?i:\w+)\b`|"A12xl", "A12XL" in "A12xl A12XL a12xl"|  
|`(?=` *sottoespressione*`)`|Asserzione lookahead positiva di larghezza zero.|`\w+(?=\.)`|"is", "ran" e "out" in "He is. The dog ran. The sun is out."|  
|`(?!` *sottoespressione*`)`|Asserzione lookahead negativa di larghezza zero.|`\b(?!un)\w+\b`|"sure", "used" in "unsure sure unity used"|  
|`(?<=` *sottoespressione*`)`|Asserzione lookbehind positiva di larghezza zero.|`(?<=19)\d{2}\b`|"99", "50", "05" in "1851 1999 1950 1905 2003"|  
|`(?<!` *sottoespressione*`)`|Asserzione lookbehind negativa di larghezza zero.|`(?<!19)\d{2}\b`|"51", "03" in "1851 1999 1950 1905 2003"|  
|`(?>` *sottoespressione*`)`|Sottoespressione non di backtracking \(o "greedy"\).|`[13579](?>A+B+)`|"1ABB", "3ABB" e "5AB" in "1ABB 3ABBC 5AB 5AC"|  
  
 [Torna all'inizio](#top)  
  
<a name="quantifiers"></a>   
## Quantificatori  
 Un quantificatore specifica il numero di istanze dell'elemento precedente, che può essere un carattere, un gruppo o una classe di caratteri, che devono essere presenti nella stringa di input affinché venga trovata una corrispondenza. I quantificatori includono gli elementi del linguaggio elencati nella tabella seguente. Per altre informazioni, vedere [Quantificatori](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md).  
  
|Quantificatore|Descrizione|Criterio|Corrispondenze|  
|--------------------|-----------------|--------------|--------------------|  
|`*`|Trova la corrispondenza dell'elemento precedente zero o più volte.|`\d*\.\d`|".0", "19.9", "219.9"|  
|`+`|Trova la corrispondenza dell'elemento precedente una o più volte.|`"be+"`|"bee" in "been", "be" in "bent"|  
|`?`|Trova la corrispondenza con l'elemento precedente zero volte o una volta soltanto.|`"rai?n"`|"ran", "rain"|  
|`{` *n* `}`|Trova la corrispondenza con l'elemento precedente esattamente *n* volte.|`",\d{3}"`|",043" in "1,043.6", ",876", ",543" e ",210" in "9,876,543,210"|  
|`{` *n* `,}`|Trova la corrispondenza con l'elemento precedente almeno *n* volte.|`"\d{2,}"`|"166", "29", "1930"|  
|`{` *n* `,` *m* `}`|Trova la corrispondenza con l'elemento precedente almeno *n* volte, ma non più di *m* volte.|`"\d{3,5}"`|"166", "17668"<br /><br /> "19302" in "193024"|  
|`*?`|Trova la corrispondenza dell'elemento precedente zero o più volte, ma il minor numero di volte possibile.|`\d*?\.\d`|".0", "19.9", "219.9"|  
|`+?`|Trova la corrispondenza dell'elemento precedente una o più volte, ma il minor numero di volte possibile.|`"be+?"`|"be" in "been", "be" in "bent"|  
|`??`|Trova la corrispondenza dell'elemento precedente zero volte o una volta, ma il minor numero di volte possibile.|`"rai??n"`|"ran", "rain"|  
|`{` *n* `}?`|Trova la corrispondenza con l'elemento precedente esattamente *n* volte.|`",\d{3}?"`|",043" in "1,043.6", ",876", ",543" e ",210" in "9,876,543,210"|  
|`{` *n* `,}?`|Trova la corrispondenza dell'elemento precedente almeno *n* volte, ma il minor numero di volte possibile.|`"\d{2,}?"`|"166", "29", "1930"|  
|`{` *n* `,` *m* `}?`|Trova la corrispondenza con l'elemento precedente tra *n* e *m* volte, ma il minor numero di volte possibile.|`"\d{3,5}?"`|"166", "17668"<br /><br /> "193", "024" in "193024"|  
  
 [Torna all'inizio](#top)  
  
<a name="backreference_constructs"></a>   
## Costrutti di backreference  
 Un backreference consente a una sottoespressione di cui è stata trovata la corrispondenza in precedenza di essere identificata successivamente nella stessa espressione regolare. Nella tabella seguente sono elencati i costrutti di backreference supportati dalle espressioni regolari in .NET Framework. Per altre informazioni, vedere [Costrutti di backreference](../../../docs/standard/base-types/backreference-constructs-in-regular-expressions.md).  
  
|Costrutto di backreference|Descrizione|Criterio|Corrispondenze|  
|--------------------------------|-----------------|--------------|--------------------|  
|`\` *numero*|Backreference. Trova la corrispondenza del valore di una sottoespressione numerata.|`(\w)\1`|"ee" in "seek"|  
|`\k<` *nome* `>`|Backreference denominato. Trova la corrispondenza del valore di un'espressione denominata.|`(?<char>\w)\k<char>`|"ee" in "seek"|  
  
 [Torna all'inizio](#top)  
  
<a name="alternation_constructs"></a>   
## Costrutti di alternanza  
 I costrutti di alternanza modificano un'espressione regolare per abilitare la corrispondenza di tipo either\/or. Questi costrutti includono gli elementi del linguaggio elencati nella tabella seguente. Per altre informazioni, vedere [Costrutti di alternanza](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md).  
  
|Costrutto di alternanza|Descrizione|Criterio|Corrispondenze|  
|-----------------------------|-----------------|--------------|--------------------|  
|`&#124;`|Trova la corrispondenza di qualsiasi un elemento separato dal carattere di barra verticale.|`th(e&#124;is&#124;at)`|"the", "this" in "this is the day. "|  
|`(?(` *espressione* `)` *sì* `&#124;` *no* `)`|Corrisponde a *yes* se il criterio di espressione regolare definito da *expression* corrisponde. In caso contrario, corrisponde alla parte *no* facoltativa.*espressione* è interpretata come asserzione di larghezza zero.|`(?(A)A\d{2}\b&#124;\b\d{3}\b)`|"A10", "910" in "A10 C103 910"|  
|`(?(` *nome* `)` *sì* `&#124;` *no* `)`|Corrisponde a *yes* se *nome*, un gruppo di acquisizione denominato o numerato, dispone di una corrispondenza.In caso contrario, corrisponde al *no* facoltativo.|`(?<quoted>")?(?(quoted).+?"&#124;\S+\s)`|Dogs.jpg, "Yiska playing.jpg" in "Dogs.jpg "Yiska playing.jpg""|  
  
 [Torna all'inizio](#top)  
  
<a name="substitutions"></a>   
## Sostituzioni  
 Le sostituzioni sono elementi del linguaggio di espressioni regolari supportati nei modelli di sostituzione. Per altre informazioni, vedere [Sostituzioni](../../../docs/standard/base-types/substitutions-in-regular-expressions.md). I metacaratteri elencati nella tabella seguente sono asserzioni atomiche di larghezza zero.  
  
|Carattere|Descrizione|Criterio|Modello di sostituzione|Stringa di input|Stringa di risultato|  
|---------------|-----------------|--------------|-----------------------------|----------------------|--------------------------|  
|`$` *numero*|Sostituisce la sottostringa corrispondente al gruppo *numero*.|`\b(\w+)(\s)(\w+)\b`|`$3$2$1`|"one two"|"two one"|  
|`${` *nome* `}`|Sostituisce la sottostringa corrispondente al gruppo denominato *nome*.|`\b(?<word1>\w+)(\s)(?<word2>\w+)\b`|`${word2} ${word1}`|"one two"|"two one"|  
|`$$`|Sostituisce un valore letterale "$".|`\b(\d+)\s?USD`|`$$$1`|"103 USD"|"$103"|  
|`$&`|Sostituisce una copia dell'intera corrispondenza.|`\$?\d*\.?\d+`|`**$&**`|"$1.30"|"\*\*$1.30\*\*"|  
|`$``|Sostituisce tutto il testo della stringa di input prima della corrispondenza.|`B+`|`$``|"AABBCC"|"AAAACC"|  
|`$'`|Sostituisce tutto il testo della stringa di input successiva alla corrispondenza.|`B+`|`$'`|"AABBCC"|"AACCCC"|  
|`$+`|Sostituisce l'ultimo gruppo acquisito.|`B+(C+)`|`$+`|"AABBCCDD"|AACCDD|  
|`$_`|Sostituisce l'intera stringa di input.|`B+`|`$_`|"AABBCC"|"AAAABBCCCC"|  
  
 [Torna all'inizio](#top)  
  
<a name="options"></a>   
## Opzioni di espressioni regolari  
 È possibile specificare opzioni che controllano il modo in cui il motore delle espressioni regolari interpreta un criterio di espressione regolare. Molte di queste opzioni possono essere specificate inline \(nel criterio di espressione regolare\) o come uno o più costanti <xref:System.Text.RegularExpressions.RegexOptions>. Questa guida di riferimento rapida elenca solo le opzioni inline. Per altre informazioni sulle opzioni inline e <xref:System.Text.RegularExpressions.RegexOptions>, vedere l'articolo [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).  
  
 È possibile specificare un'opzione inline in due modi:  
  
-   Usando il [costrutto vario](../../../docs/standard/base-types/miscellaneous-constructs-in-regular-expressions.md) `(?imnsx-imnsx)`, dove un segno meno \(\-\) prima di un'opzione o di un set di opzioni consente di disattivare tali opzioni. Ad esempio, `(?i-mn)` attiva la non corrispondenza tra maiuscole e minuscole \(`i`\), disattiva la modalità su più righe \(`m`\) e disattiva le acquisizioni del gruppo senza nome \(`n`\). L'opzione si applica al criterio di espressione regolare dal punto in cui l'opzione viene definita e diventa effettiva sia alla fine del criterio sia al punto in cui un altro costrutto annulla l'opzione.  
  
-   Usando il [costrutto di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md) `(?imnsx-imnsx:`*sottoespressione*`)`, che definisce le opzioni solo per il gruppo specificato.  
  
 Il motore delle espressioni regolari di .NET Framework supporta le seguenti opzioni inline.  
  
|Opzione|Descrizione|Criterio|Corrispondenze|  
|-------------|-----------------|--------------|--------------------|  
|`i`|Usa la corrispondenza che non fa distinzione tra maiuscole e minuscole.|`\b(?i)a(?-i)a\w+\b`|"aardvark", "aaaAuto" in "aardvark AAAuto aaaAuto Adam breakfast"|  
|`m`|Usare la modalità multiriga.`^` e `$` corrispondono all'inizio e alla fine di una riga, anziché all'inizio e alla fine della stringa di input.|Ad esempio, vedere la sezione "Modalità multiriga" in [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).||  
|`n`|Non acquisire gruppi senza nome.|Per un esempio, vedere la sezione "Solo acquisizioni esplicite" in [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).||  
|`s`|Usare la modalità a riga singola.|Per un esempio, vedere la sezione "Modalità a riga singola" in [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).||  
|`x`|Ignorare gli spazi vuoti non di escape nel criterio di espressione regolare.|`\b(?x) \d+ \s \w+`|"1 aardvark", "2 cats" in "1 aardvark 2 cats IV centurions"|  
  
 [Torna all'inizio](#top)  
  
<a name="miscellaneous_constructs"></a>   
## Costrutti vari  
 I costrutti vari consentono di modificare un criterio di espressione regolare o forniscono informazioni su di esso. Nella tabella seguente sono elencati i costrutti vari supportati da .NET Framework. Per altre informazioni, vedere [Costrutti vari](../../../docs/standard/base-types/miscellaneous-constructs-in-regular-expressions.md).  
  
|Costrutto|Definizione|Esempio|  
|---------------|-----------------|-------------|  
|`(?imnsx-imnsx)`|Imposta o disabilita opzioni come la distinzione tra maiuscole e minuscole nella parte centrale di un modello. Per altre informazioni, vedere [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).|`\bA(?i)b\w+\b` trova la corrispondenza di "ABA", "Able" in "ABA Able Act"|  
|`(?#` *commento*`)`|Commento inline. Il commento termina in corrispondenza della prima parentesi chiusa.|`\bA(?#Matches words starting with A)\w+\b`|  
|`#` \[fino alla fine della riga\]|Commento in modalità X. Il commento inizia da un carattere `#` senza codice di escape e continua fino alla fine della riga.|`(?x)\bA\w+\b#Matches words starting with A`|  
  
## Vedere anche  
 <xref:System.Text.RegularExpressions?displayProperty=fullName>   
 <xref:System.Text.RegularExpressions.Regex>   
 [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)   
 [Classi di espressioni regolari](../../../docs/standard/base-types/the-regular-expression-object-model.md)   
 [Esempi di espressioni regolari](../../../docs/standard/base-types/regular-expression-examples.md)   
 [Espressioni regolari \- Guida di riferimento rapido \(download in formato Word\)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)   
 [Espressioni regolari \- Guida di riferimento rapido \(download in formato PDF\)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)