---
title: Linguaggio di espressioni regolari - Riferimento rapido
description: Linguaggio di espressioni regolari - Riferimento rapido
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 8c5dee8c-7bc7-4e6e-aff1-986965c4d98e
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: ff1eef78985f9b5b428f3b696fb267b59f3cb283

---

# <a name="regular-expression-language-quick-reference"></a>Linguaggio di espressioni regolari - Riferimento rapido

Un'espressione regolare è un modello per il quale il motore delle espressioni regolari tenta di trovare una corrispondenza nel testo di input. Un modello è costituito da uno o più i valori letterali carattere, operatori o costrutti. Per una breve introduzione, vedere [Espressioni regolari di .NET](regular-expressions.md). 

In ogni sezione di questa guida di riferimento rapido viene elencata una categoria specifica di caratteri, operatori e costrutti che è possibile usare per definire le espressioni regolari: 

* [Caratteri di escape](#character-escapes)

* [Classi di caratteri](#character-classes)
      
* [Punti di ancoraggio](#anchors)
    
* [Costrutti di raggruppamento](#grouping-constructs)
      
* [Quantificatori](#quantifiers)
    
* [Costrutti di backreference](#backreference-constructs)
      
* [Costrutti di alternanza](#alternation-constructs)
     
* [Sostituzioni](#substitutions)
      
* [Opzioni di espressioni regolari](#regular-expression-options)
      
* [Costrutti vari](#miscellaneous-constructs)

Queste informazioni sono disponibili in due formati scaricabili e stampabili come riferimento: 

* [Download in formato Word (.docx)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)
    
* [Download in formato PDF (.pdf)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)
    
## <a name="character-escapes"></a>Caratteri di escape

Il carattere barra rovesciata (\)) in un'espressione regolare indica che il carattere successivo è un carattere speciale (come illustrato nella tabella seguente) oppure deve essere interpretato letteralmente. Per altre informazioni, vedere [Caratteri di escape nelle espressioni regolari](escapes.md). 

Caratteri di escape | Descrizione | Criterio | Corrispondenze
----------------- | ----------- | ------- | -------
**\a** | Trova la corrispondenza di un carattere di controllo del segnale acustico di avviso, \u0007. | `\a` | "\u0007" in "Error!" + '\u0007'
**\b** | In una classe di caratteri, trova la corrispondenza di un carattere backspace, \u0008. | `[\b]{3,}` | "\b\b\b\b" in "\b\b\b\b"
**\t** | Trova la corrispondenza di un carattere di tabulazione, \u0009. | `(\w+)\t` | "item1\t", "item2\t" in "item1\titem2\t"
**\r** | Trova la corrispondenza di un carattere di ritorno a capo, \u000D. **\r** non equivale al carattere di nuova riga **\n**. | `\r\n(\w+)` | "\r\nThese" in "\r\nThese are\ntwo lines."
**\v** | Trova la corrispondenza di un carattere di tabulazione verticale, \u000B. | `[\v]{2,}` | "\v\v\v" in "\v\v\v"
**\f** | Trova la corrispondenza di un carattere di avanzamento carta, \u000C. | `[\f]{2,}` | "\f\f\f" in "\f\f\f" 
**\n** | Trova la corrispondenza di una nuova riga, \u000A. | `\r\n(\w+)` | "\r\nThese" in "\r\nThese are\ntwo lines."
**\e** | Trova la corrispondenza di un carattere di escape, \u001B. | `\e` | "\x001B" in "\x001B"
**\**_nnn_ | Usa la rappresentazione ottale per specificare un carattere (*nnn* è costituito da un massimo di tre cifre). | `\w\040\w` | "a b", "c d" in "a bc d"
**\x**_nn_ | Usa la rappresentazione esadecimale per specificare un carattere (*nn* è costituito da esattamente due cifre). | `\w\x20\w` | "a b", "c d" in "a bc d"
**\c**_X_ o **\c**_x_ | Trova la corrispondenza con il carattere di controllo ASCII specificato da *X* o *x*, dove *X* o *x* è la lettera del carattere di controllo. | `\cC` | "\x0003" in "\x0003" (Ctrl-C) 
**\u**_nnnn_ | Trova la corrispondenza di un carattere Unicode usando una rappresentazione esadecimale (esattamente quattro cifre, come rappresentate da *nnnn*). | `\w\u0020\w` | "a b", "c d" in "a bc d"
**\\** | Quando è seguito da un carattere non riconosciuto come carattere di escape, in questa e in altre tabelle del presente argomento, trova la corrispondenza di tale carattere. Ad esempio, __\*__ equivale a **\x2A** e **\.** equivale a **\x2E**. Questo consente al motore delle espressioni regolari di distinguere tra elementi del linguaggio, ad esempio `*` o `?`, e valori letterali carattere, rappresentati da `\*` o `\?)`. | `\d+[\+-x\*]\d+` | "2+2" e "3*9" in "(2+2) * 3*9"
 
## <a name="character-classes"></a>Classi di caratteri

Una classe di caratteri trova la corrispondenza con uno qualsiasi di un set di caratteri. Le classi di caratteri includono gli elementi del linguaggio elencati nella tabella seguente. Per altre informazioni, vedere [Classi di caratteri nelle espressioni regolari](classes.md).

Classe di caratteri | Descrizione | Criterio | Corrispondenze
--------------- | ----------- | ------- | ------- 
__[__*character_group*__]__ | Trova la corrispondenza con qualsiasi carattere in un elenco di singoli caratteri. Per impostazione predefinita, viene effettuata la distinzione tra maiuscole e minuscole. | `[ae]` | "a" in "gray", "a", "e" in "lane"
__[^__*character_group*__]__ | Negazione: corrisponde a qualsiasi carattere singolo non incluso in *character_group*. Per impostazione predefinita, per i caratteri in *character_group* si fa distinzione tra maiuscole e minuscole. | `[^aei]` |  "r", "g", "n" in "reign"
__[__*first-last*__]__ | Intervallo di caratteri: trova la corrispondenza di qualsiasi carattere singolo nell'intervallo dal *primo* all'*ultimo*. | `[A-Z]` | "A", "B" in "AB123"
**.** | Carattere jolly: trova la corrispondenza di qualsiasi carattere singolo ad eccezione di "\n". Per confrontare un carattere punto di valore letterale (. o \u002E), è necessario farlo precedere da un carattere di escape (\.). | `a.e` |  "ave" in "nave", "ate" in "water"
__\p{__*nome*__}__ | Trova la corrispondenza con qualsiasi carattere singolo incluso nel blocco denominato o nella categoria generale Unicode specificato da *nome*. | `\p{Lu}`, `\p{IsCyrillic}` | "C", "L" in "City Lights", "?", "?" in "??em"
__\P{__*nome*__}__ | Trova la corrispondenza con qualsiasi carattere singolo non incluso nel blocco denominato o nella categoria generale Unicode specificato da *nome*. | `\P{Lu}`, `\P{IsCyrillic}` |` "i", "t", "y" in "City", "e", "m" in "??em"
**\w** | Trova la corrispondenza di qualsiasi carattere alfabetico. | `\w` | "I", "D", "A", "1", "3" in "ID A1.3" 
**\W** | Trova la corrispondenza di qualsiasi carattere non alfabetico. | `\W` | " ", "." in "ID A1.3"
**\s** | Trova la corrispondenza di qualsiasi carattere di spazio. | `\w\s` | "D " in "ID A1.3"
**\S** | Trova la corrispondenza di qualsiasi carattere diverso da uno spazio. | `\s\S` | " _" in "int __ctr" 
**\d** | Trova la corrispondenza di qualsiasi cifra decimale. | `\d` | "4" in "4 = IV" 
**\D** | Trova la corrispondenza con qualsiasi carattere diverso da una cifra decimale. | `\D` | " ", "=", " ", "I", "V" in "4 = IV" 

## <a name="anchors"></a>Punti di ancoraggio

Gli ancoraggi, o asserzioni atomiche di larghezza zero, determinano l'esito della ricerca di una corrispondenza in base alla posizione corrente nella stringa, ma non comportano l'avanzamento del motore nella stringa o l'utilizzo di caratteri. I metacaratteri elencati nella tabella seguente sono ancoraggi. Per altre informazioni, vedere [Ancoraggi nelle espressioni regolari](anchors.md).

Asserzione | Descrizione | Criterio | Corrispondenze
--------- | ----------- | ------- | ------- 
**^** | La corrispondenza deve iniziare all'inizio della stringa o della riga. | `^\d{3}` | "901" in "901-333-"
**$** | La corrispondenza deve verificarsi alla fine della stringa o prima di **\n** alla fine della riga o della stringa. | `-\d{3}$` | "-333" in "-901-333"
**\A** | La corrispondenza deve verificarsi all'inizio della stringa. | `\A\d{3}` | "901" in "901-333-"
**\Z** | La corrispondenza deve verificarsi alla fine della stringa o prima di **\n** alla fine della stringa. | `-\d{3}\Z` | "-333" in "-901-333"
**\z** | La corrispondenza deve verificarsi alla fine della stringa. | `-\d{3}\z` | "-333" in "-901-333"
**\G** | La corrispondenza deve verificarsi nel punto in cui è terminata la corrispondenza precedente. | `\G\(\d\)` | "(1)", "(3)", "(5)" in "(1)(3)(5)[7]&#40;9)"
**\b** | La corrispondenza deve verificarsi sul limite tra un carattere **\w** (alfanumerico) e un carattere **\W** (non alfanumerico). | `\b\w+\s\w+\b` | "them theme", "them them" in "them theme them them" 
**\B** | La corrispondenza non deve verificarsi su un limite **\b**. | `\Bend\w*\b` | "ends", "ender" in "end sends endure lender"

## <a name="grouping-constructs"></a>Costrutti di raggruppamento

I costrutti di raggruppamento delineano sottoespressioni di un'espressione regolare e in genere acquisiscono sottostringhe di una stringa di input. I costrutti di raggruppamento includono gli elementi del linguaggio elencati nella tabella seguente. Per altre informazioni, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

Costrutto di raggruppamento | Descrizione | Criterio | Corrispondenze
------------------ | ----------- | ------- | ------- 
**(**_subexpression_**)** | Acquisisce la sottoespressione corrispondente e le assegna un numero ordinale in base uno. | `(\w)\1` | "ee" in "deep"
**(?**<name> _subexpression_**)** | Acquisisce la sottoespressione corrispondente in un gruppo denominato. | `(?<double>\w)\k<double>` | "ee" in "deep"
**(?**<nome1-nome2> _subexpression_**)** | Definisce una definizione di gruppo di bilanciamento Per altre informazioni, vedere la sezione [Definizione del gruppo di bilanciamento](grouping.md#balancing-group-definitions) in [Costrutti di raggruppamento nelle espressioni regolari](grouping.md). | `(((?'Open'\()[^\(\)]*)+((?'Close-Open'\))[^\(\)]*)+)*(?(Open)(?!))$` | "((1-3)*(3-1))" in "3+2^((1-3)*(3-1))"
**(?**: subexpression**)** | Definisce un gruppo di non acquisizione. | `Write(?:Line)?` | "WriteLine" in "Console.WriteLine()", "Write" in "Console.Write(value)"
**(?imnsx-imnsx**: _subexpression_**)** | Applica o disabilita le opzioni specificate nella _sottoespressione_. Per altre informazioni, vedere [Opzioni di espressioni regolari](options.md). | `A\d{2}(?i:\w+)\b` | "A12xl", "A12XL" in "A12xl A12XL a12xl"
**(?**= _subexpression_**)** | Asserzione lookahead positiva di larghezza zero. | `\w+(?=\.)` | "is", "ran" e "out" in "He is. The dog ran. The sun is out."
**(?!** _subexpression_**)** | Asserzione lookahead negativa di larghezza zero. | `\b(?!un)\w+\b` | "sure", "used" in "unsure sure unity used"
**(?**<= _subexpression_**)** | Asserzione lookbehind positiva di larghezza zero. | `(?<=19)\d{2}\b` | "99", "50", "05" in "1851 1999 1950 1905 2003"
**(?**<! _subexpression_**)** | Asserzione lookbehind negativa di larghezza zero. | `(?<!19)\d{2}\b` | "51", "03" in "1851 1999 1950 1905 2003"
**(?**> _subexpression_**)** | Sottoespressione non di backtracking (o "greedy"). | `[13579](?>A+B+)` | "1ABB", "3ABB" e "5AB" in "1ABB 3ABBC 5AB 5AC"

## <a name="quantifiers"></a>Quantificatori

Un quantificatore specifica il numero di istanze dell'elemento precedente, che può essere un carattere, un gruppo o una classe di caratteri, che devono essere presenti nella stringa di input affinché venga trovata una corrispondenza. I quantificatori includono gli elementi del linguaggio elencati nella tabella seguente. Per altre informazioni, vedere [Quantificatori nelle espressioni regolari](quantifiers.md).

Quantificatore | Descrizione | Criterio | Corrispondenze
---------- | ----------- | ------- | -------
__*__ | Trova la corrispondenza dell'elemento precedente zero o più volte. | `\d*\.\d` | ".0", "19.9", "219.9"
**+** | Trova la corrispondenza dell'elemento precedente una o più volte. | `"be+"` | "bee" in "been", "be" in "bent"
**?** | Trova la corrispondenza con l'elemento precedente zero volte o una volta soltanto. | `"rai?n"` | "ran", "rain"
**{**_n_**}** | Trova la corrispondenza con l'elemento precedente esattamente *n* volte. | `",\d{3}"` | ",043" in "1,043.6", ",876", ",543" e ",210" in "9,876,543,210"
**{**_n_,**}** | Trova la corrispondenza con l'elemento precedente almeno *n* volte. | `"\d{2,}"` | "166", "29", "1930"
**{**_n_,_m_**}** | Trova la corrispondenza con l'elemento precedente almeno *n* volte, ma non più di *m* volte. | `"\d{3,5}"` | "166", "17668"; "19302" in "193024"
__*?__ | Trova la corrispondenza dell'elemento precedente zero o più volte, ma il minor numero di volte possibile. | `\d*?\.\d` | ".0", "19.9", "219.9"
**+?** | Trova la corrispondenza dell'elemento precedente una o più volte, ma il minor numero di volte possibile. | `"be+?"` | "be" in "been", "be" in "bent"
**??** | Trova la corrispondenza dell'elemento precedente zero volte o una volta, ma il minor numero di volte possibile. | `"rai??n"` | "ran", "rain"
**{**_n_**}?** | Trova la corrispondenza con l'elemento precedente esattamente *n* volte. | `",\d{3}?"` | ",043" in "1,043.6", ",876", ",543" e ",210" in "9,876,543,210"
**{**_n_,**}?** | Trova la corrispondenza dell'elemento precedente almeno *n* volte, ma il minor numero di volte possibile. | `"\d{2,}?"` | "166", "29", "1930"
**{**_n_,_m_**}?** | Trova la corrispondenza con l'elemento precedente tra *n* e *m* volte, ma il minor numero di volte possibile. | `"\d{3,5}?"` | "166", "17668"; "193", "024" in "193024"

## <a name="backreference-constructs"></a>Costrutti di backreference

Un backreference consente a una sottoespressione di cui è stata trovata la corrispondenza in precedenza di essere identificata successivamente nella stessa espressione regolare. Nella tabella seguente sono elencati i costrutti di backreference supportati dalle espressioni regolari in .NET Framework. Per altre informazioni, vedere [Costrutti di backreference nelle espressioni regolari](backreference.md).

Costrutto di backreference | Descrizione | Criterio | Corrispondenze
----------------------- | ----------- | ------- | -------
**\**_numero_ | Backreference. Trova la corrispondenza del valore di una sottoespressione numerata. | `(\w)\1 ` | "ee" in "seek"
**\k<**_nome_**>** | Backreference denominato. Trova la corrispondenza del valore di un'espressione denominata. | `(?<char>\w)\k<char>` | "ee" in "seek"

## <a name="alternation-constructs"></a>Costrutti di alternanza

I costrutti di alternanza modificano un'espressione regolare per abilitare la corrispondenza di tipo either/or. Questi costrutti includono gli elementi del linguaggio elencati nella tabella seguente. Per altre informazioni, vedere [Costrutti di alternanza nelle espressioni regolari](alternation.md).

Costrutto di alternanza | Descrizione | Criterio | Corrispondenze
--------------------- | ----------- | ------- | ------- 
**&#124;** | Trova la corrispondenza di qualsiasi un elemento separato dal carattere di barra verticale (*&#124;). | `th(e*&#124;is*&#124;at)` | "the", "this" in "this is the day. "
__(?(__*expression*__)__*yes*__&#124;__*no*__)__ | Corrisponde a *yes* se il criterio di espressione regolare definito da *expression* corrisponde. In caso contrario, corrisponde alla parte *no* facoltativa. *expression* è interpretata come asserzione di larghezza zero. | `(?(A)A\d{2}\b*&#124;\b\d{3}\b)` | "A10", "910" in "A10 C103 910"
**(?(**_name_**)**_yes_&#124;_no_**)** | Corrisponde a *yes* se esiste una corrispondenza per *name*, un gruppo di acquisizione denominato o numerato. In caso contrario, corrisponde alla parte *no* facoltativa. | `(?<quoted>")?(?,(quoted).+?"*&#124;\S+\s)` | Dogs.jpg, "Yiska playing.jpg" in "Dogs.jpg "Yiska playing.jpg""

## <a name="substitutions"></a>Sostituzioni

Le sostituzioni sono elementi del linguaggio di espressioni regolari supportati nei modelli di sostituzione. Per altre informazioni, vedere [Sostituzioni nelle espressioni regolari](substitutions.md). I metacaratteri elencati nella tabella seguente sono asserzioni atomiche di larghezza zero.

Carattere | Descrizione | Criterio | Modello di sostituzione | Stringa di input | Stringa di risultato
--------- | ----------- | ------- | ------------------- | ------------ | ------------- 
**$**_number_ | Sostituisce la sottostringa corrispondente al gruppo *number*. | `\b(\w+)(\s)(\w+)\b` | `$3$2$1` | "one two" | "two one"
**${**_nome_**}** | Sostituisce la sottostringa corrispondente al gruppo denominato *nome*. | `\b(?<word1>\w+)(\s)(?<word2>\w+)\b` | `${word2} ${word1}` | "one two" | "two one"
**$$** | Sostituisce un valore letterale "$". | `\b(\d+)\s?USD` | `$$$1` | "103 USD" | "$103"
**$&** | Sostituisce una copia dell'intera corrispondenza. | `\$?\d*\.?\d+` | `**$&**` | "$1.30" | "**$1.30**"
**$`** | Sostituisce tutto il testo della stringa di input prima della corrispondenza. | `B+` | `$`` | "AABBCC" | "AAAACC"
**$'** | Sostituisce tutto il testo della stringa di input successiva alla corrispondenza. | `B+` | `$'` | "AABBCC" | "AACCCC"
**$+** | Sostituisce l'ultimo gruppo acquisito. | `B+(C+)` | `$+` | "AABBCCDD" | "AACCDD"
**$_** | Sostituisce l'intera stringa di input. | `B+` | `$_` | "AABBCC" | "AAAABBCCCC"

## <a name="regular-expression-options"></a>Opzioni di espressioni regolari

È possibile specificare opzioni che controllano il modo in cui il motore delle espressioni regolari interpreta un criterio di espressione regolare. Molte di queste opzioni possono essere specificate inline (nel criterio di espressione regolare) o come uno o più costanti `RegexOptions`. Questa guida di riferimento rapida elenca solo le opzioni inline. Per altre informazioni sulle opzioni inline e `RegexOptions`, vedere l'articolo [Opzioni di espressioni regolari](options.md). 

È possibile specificare un'opzione inline in due modi:

* Usando il costrutto vario **(?imnsx-imnsx)**, dove un segno meno (-) prima di un'opzione o di un set di opzioni consente di disattivare tali opzioni. Ad esempio, **(?i-mn)** attiva la corrispondenza senza distinzione tra maiuscole e minuscole (i), disattiva la modalità su più righe (**m**) e disattiva le acquisizioni dei gruppi senza nome (**n**). L'opzione si applica al criterio di espressione regolare dal punto in cui l'opzione viene definita e diventa effettiva sia alla fine del criterio sia al punto in cui un altro costrutto annulla l'opzione.

* Usando il costrutto di raggruppamento **(?imnsx-imnsx:**_sottoespressione_**)**, che definisce le opzioni solo per il gruppo specificato.

Il motore delle espressioni regolari di .NET supporta le seguenti opzioni inline.

Opzione | Descrizione | Criterio | Corrispondenze
------ | ----------- | ------- | ------- 
**i** | Usa la corrispondenza che non fa distinzione tra maiuscole e minuscole. | **\b(?i)a(?-i)a\w+\b** | "aardvark", "aaaAuto" in "aardvark AAAuto aaaAuto Adam breakfast" 
**m** | Usare la modalità multiriga. **^** e **$** corrispondono all'inizio e alla fine di una riga, anziché all'inizio e alla fine di una stringa. | Per un esempio, vedere la sezione "Modalità multiriga" in [Opzioni di espressioni regolari](options.md). | 
**n*** | Non acquisire gruppi senza nome. | Per altre informazioni, vedere la sezione "Solo acquisizioni esplicite" in [Opzioni di espressioni regolari](options.md). | 
**s** | Usare la modalità a riga singola. | Per un esempio, vedere la sezione "Modalità a riga singola" in [Opzioni di espressioni regolari](options.md). | 
**x** | Ignorare gli spazi vuoti non di escape nel criterio di espressione regolare. | **\b(?x) \d+ \s \w+** | "1 aardvark", "2 cats" in "1 aardvark 2 cats IV centurions" 

##<a name="miscellaneous-constructs"></a>Costrutti vari

I costrutti vari consentono di modificare un criterio di espressione regolare o forniscono informazioni su di esso. Nella tabella seguente sono elencati i costrutti vari supportati da .NET. Per altre informazioni, vedere [Costrutti vari nelle espressioni regolari](miscellaneous.md).

Costrutto | Definizione | Esempio
--------- | ---------- | ------- 
**(?imnsx-imnsx)** | Imposta o disabilita opzioni come la distinzione tra maiuscole e minuscole nella parte centrale di un modello. Per altre informazioni, vedere [Opzioni di espressioni regolari](options.md). | `\bA(?i)b\w+\b` trova la corrispondenza di "ABA", "Able" in "ABA Able Act"
**(?#** _comment_**)** | Commento inline. Il commento termina in corrispondenza della prima parentesi chiusa. | `\bA(?#` corrisponde a parole che iniziano con `A)\w+\b`
**#** [fino alla fine della riga] | Commento in modalità X. Il commento inizia da un carattere # senza codice di escape e continua fino alla fine della riga. | `(?x)\bA\w+\b#` corrisponde a parole che iniziano con `A`

## <a name="see-also"></a>Vedere anche




[System.Text.RegularExpressions](xref:System.Text.RegularExpressions)

[Regex](xref:System.Text.RegularExpressions.Regex)

[Espressioni regolari in .NET](regular-expressions.md)

[Modello a oggetti delle espressioni regolari](object-model.md)

[Esempi di espressioni regolari](regex-examples.md)

[Download in formato Word (.docx)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)
    
[Download in formato PDF (.pdf)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)



<!--HONumber=Nov16_HO1-->


