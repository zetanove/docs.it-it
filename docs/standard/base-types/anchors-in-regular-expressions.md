---
title: "Ancoraggi in espressioni regolari | Microsoft Docs"
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
  - "espressioni regolari di .NET Framework, ancoraggi"
  - "espressioni regolari di .NET Framework, asserzioni atomiche a larghezza zero"
  - "ancoraggi, in espressioni regolari"
  - "asserzioni atomiche a larghezza zero"
  - "metacaratteri, ancoraggi"
  - "metacaratteri, asserzioni atomiche a larghezza zero"
  - "espressioni regolari, ancoraggi"
  - "espressioni regolari, asserzioni atomiche a larghezza zero"
ms.assetid: 336391f6-2614-499b-8b1b-07a6837108a7
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Ancoraggi in espressioni regolari
<a name="top"></a> Gli ancoraggi, o asserzioni atomiche di larghezza zero, specificano una posizione della stringa in cui deve verificarsi una corrispondenza. Quando si usa un ancoraggio nell'espressione di ricerca, il motore delle espressioni regolari non avanza nella stringa né utilizza caratteri, ma cerca una corrispondenza solo nella posizione specificata. Ad esempio, `^` specifica che la corrispondenza deve iniziare all'inizio di una riga o stringa. Di conseguenza, l'espressione regolare `^http:` considera la corrispondenza "http:" solo quando si verifica all'inizio di una riga. La tabella seguente contiene gli ancoraggi supportati dalle espressioni regolari in .NET Framework.  
  
|Ancoraggio|Descrizione|  
|----------------|-----------------|  
|`^`|La corrispondenza deve iniziare all'inizio della stringa o della riga. Per altre informazioni, vedere [Inizio di stringa o riga](#Start).|  
|`$`|La corrispondenza deve verificarsi alla fine della stringa o della riga oppure prima di `\n` alla fine della stringa o della riga. Per altre informazioni, vedere [Fine di stringa o riga](#End).|  
|`\A`|La corrispondenza deve verificarsi solo all'inizio della stringa \(nessun supporto per più righe\). Per altre informazioni, vedere [Solo inizio di stringa](#StartOnly).|  
|`\Z`|La corrispondenza deve verificarsi alla fine della stringa o prima di `\n` alla fine della stringa. Per altre informazioni, vedere [Fine di stringa o prima di terminare una nuova riga](#EndOrNOnly).|  
|`\z`|La corrispondenza deve verificarsi solo alla fine della stringa. Per altre informazioni, vedere [Solo fine di stringa](#EndOnly).|  
|`\G`|La corrispondenza deve iniziare nella posizione in cui è terminata la corrispondenza precedente. Per altre informazioni, vedere [Corrispondenze contigue](#Contiguous).|  
|`\b`|La corrispondenza deve verificarsi in un confine di parola. Per altre informazioni, vedere [Confine di parola](#WordBoundary).|  
|`\B`|La corrispondenza non deve verificarsi in un confine di parola. Per altre informazioni, vedere [Carattere che non costituisce un confine di parola](#NonwordBoundary).|  
  
<a name="Start"></a>   
## Inizio di stringa o riga: ^  
 L'ancoraggio `^` specifica che il criterio seguente deve iniziare in corrispondenza della posizione del primo carattere della stringa. Se si usa `^` con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> \(vedere [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md)\), la corrispondenza deve verificarsi all'inizio di ogni riga.  
  
 L'esempio seguente usa l'ancoraggio `^` in un'espressione regolare che estrae informazioni sugli anni durante i quali sono esistite alcune squadre di baseball professionale. L'esempio chiama due overload del metodo <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName>  
  
-   La chiamata dell'overload <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%29> trova solo la prima sottostringa nella stringa di input corrispondente al criterio di espressione regolare.  
  
-   La chiamata dell'overload <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29> con il parametro `options` impostato su <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> trova tutte le cinque sottostringhe.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/startofstring1.cs#1)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/startofstring1.vb#1)]  
  
 Il criterio di ricerca di espressioni regolari `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+` è definito nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`^`|La corrispondenza deve iniziare all'inizio della stringa di input \(o all'inizio della riga se il metodo viene chiamato con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>\).|  
|`((\w+(\s?)){2,}`|Trova uno o più caratteri alfanumerici seguiti da nessuno o uno spazio esattamente due volte. Equivale al primo gruppo di acquisizione. Questa espressione definisce anche un secondo e un terzo gruppo di acquisizione: il secondo è costituito dalla parola acquisita, il terzo dagli spazi acquisiti.|  
|`,\s`|Trova una virgola seguita da uno spazio vuoto.|  
|`(\w+\s\w+)`|Trova uno o più caratteri alfanumerici seguiti da uno spazio, seguito da uno o più caratteri alfanumerici. Questo è il quarto gruppo di acquisizione.|  
|`,`|Trova la corrispondenza con una virgola.|  
|`\s\d{4}`|Trova uno spazio seguito da quattro cifre decimali.|  
|\(\-`(\d{4}&#124;present))?`|Trova nessuna o una occorrenza di un trattino seguita da quattro cifre decimali o dalla stringa "present". Equivale al sesto gruppo di acquisizione. Include anche un settimo gruppo di acquisizione.|  
|`,?`|Trova nessuna o una occorrenza di una virgola.|  
|`(\s\d{4}(-(\d{4}&#124;present))?,?)+`|Trova una o più occorrenze di: uno spazio, quattro cifre decimali, nessuna o una occorrenza di un trattino seguita da quattro cifre decimali oppure la stringa "present" e nessuna o una virgola. Equivale al quinto gruppo di acquisizione.|  
  
 [Torna all'inizio](#top)  
  
<a name="End"></a>   
## Fine di stringa o riga: ^  
 L'ancoraggio `$` specifica che il criterio precedente deve verificarsi alla fine della stringa di input oppure prima di `\n` alla fine della stringa di input.  
  
 Se si usa `$` con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>, la corrispondenza può verificarsi anche alla fine di una riga. Notare che `$` corrisponde a `\n`, ma non a `\r\n` \(combinazione di ritorno a capo e caratteri di nuova riga o CR\/LF\). Per trovare la combinazione di caratteri CR\/LF, includere `\r?$` nel criterio di espressione regolare.  
  
 L'esempio seguente aggiunge l'ancoraggio `$` al criterio di espressione regolare usato nell'esempio della sezione [Inizio di stringa o riga](#Start). Se usato con la stringa di input originale, che include cinque righe di testo, il metodo <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%29?displayProperty=fullName> non riesce a trovare una corrispondenza, perché la fine della prima riga non corrisponde al criterio `$`. Quando la stringa di input originale viene suddivisa in una matrice di stringhe, il metodo <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%29?displayProperty=fullName> riesce a trovare la corrispondenza in ognuna delle cinque righe. Quando il metodo <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=fullName> viene chiamato con il parametro `options` impostato su <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>, non viene trovata alcuna corrispondenza perché il criterio di espressione regolare non tiene conto dell'elemento di ritorno a capo \(\\u\+000D\). Tuttavia, quando il criterio di espressione regolare viene modificato sostituendo `$` con `\r?$`, la chiamata del metodo <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=fullName> con il parametro `options` impostato su <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> trova di nuovo cinque corrispondenze.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/endofstring1.cs#2)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/endofstring1.vb#2)]  
  
 [Torna all'inizio](#top)  
  
<a name="StartOnly"></a>   
## Solo inizio di stringa: \\A  
 L'ancoraggio `\A` specifica che la corrispondenza deve verificarsi all'inizio della stringa di input. L'ancoraggio è identico a `^`, ad eccezione del fatto che `\A` ignora l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>. Di conseguenza, può trovare solo l'inizio della prima riga in una stringa di input con più righe.  
  
 L'esempio seguente è simile agli esempi per gli ancoraggi `^` e `$`. L'esempio usa l'ancoraggio `\A` in un'espressione regolare che estrae informazioni sugli anni durante i quali sono esistite alcune squadre di baseball professionale. La stringa di input include cinque righe. La chiamata del metodo <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=fullName> trova solo la prima sottostringa nella stringa di input corrispondente al criterio di espressione regolare. Come mostrato nell'esempio, l'opzione <xref:System.Text.RegularExpressions.RegexOptions> non ha alcun effetto.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/startofstring2.cs#3)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/startofstring2.vb#3)]  
  
 [Torna all'inizio](#top)  
  
<a name="EndOrNOnly"></a>   
## Fine di stringa o prima di terminare una nuova riga: \\Z  
 L'ancoraggio `\Z` specifica che la corrispondenza deve verificarsi alla fine della stringa di input oppure prima di `\n` alla fine della stringa di input. L'ancoraggio è identico a `$`, ad eccezione del fatto che `\Z` ignora l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>. Di conseguenza, in una stringa con più righe può trovare solo la fine dell'ultima riga oppure l'ultima riga prima di `\n`.  
  
 Notare che `\Z` corrisponde a `\n`, ma non a `\r\n` \(combinazione di caratteri CR\/LF\). Per trovare la combinazione di caratteri CR\/LF, includere `\r?\Z` nel criterio di espressione regolare.  
  
 L'esempio seguente usa l'ancoraggio `\Z` in un'espressione regolare simile all'esempio della sezione [Inizio di stringa o riga](#Start), che estrae informazioni sugli anni durante i quali sono esistite alcune squadre di baseball professionale. La sottoespressione `\r?\Z`nell'espressione regolare `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\Z` trova la fine di una stringa e anche una stringa che termina con `\n` o `\r\n`. Di conseguenza, ogni elemento nella matrice corrisponde al criterio di espressione regolare.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/endofstring2.cs#4)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/endofstring2.vb#4)]  
  
 [Torna all'inizio](#top)  
  
<a name="EndOnly"></a>   
## Solo fine di stringa: \\z  
 L'ancoraggio `\z` specifica che la corrispondenza deve verificarsi alla fine della stringa di input. Come per l'elemento del linguaggio `$`, `\z` ignora l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>. Diversamente dall'elemento del linguaggio `\Z`, `\z` non trova un carattere `\n` alla fine di una stringa. Di conseguenza, può trovare solo l'ultima riga della stringa di input.  
  
 L'esempio seguente usa l'ancoraggio `\z` in un'espressione regolare che è altrimenti identica all'esempio della sezione precedente, che estrae informazioni sugli anni durante i quali sono esistite alcune squadre di baseball professionale. L'esempio prova a trovare ognuno dei cinque elementi in una matrice di stringhe con il criterio di espressione regolare `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\z`. Due delle stringhe terminano con caratteri di ritorno a capo e di avanzamento riga, mentre le altre due no. Come mostrato dall'output, solo le stringhe senza carattere di ritorno a capo o avanzamento riga corrispondono al criterio.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/endofstring3.cs#5)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/endofstring3.vb#5)]  
  
 [Torna all'inizio](#top)  
  
<a name="Contiguous"></a>   
## Corrispondenze contigue: \\G  
 L'ancoraggio `\G` specifica che la corrispondenza deve verificarsi nel punto in cui è terminata la corrispondenza precedente. Se usato con il metodo <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName> o <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=fullName>, questo ancoraggio garantisce che tutte le corrispondenze siano contigue.  
  
 L'esempio seguente usa un'espressione regolare per estrarre i nomi delle specie di roditori da una stringa con valori delimitati da virgole.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/contiguous1.cs#6)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/contiguous1.vb#6)]  
  
 L'espressione regolare `\G(\w+\s?\w*),?` viene interpretata come illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\G`|La corrispondenza deve iniziare nel punto in cui termina l'ultima corrispondenza.|  
|`\w+`|Trova la corrispondenza di uno o più caratteri alfanumerici.|  
|`\s?`|Trova nessuno o uno spazio.|  
|`\w*`|Trova la corrispondenza di zero o più caratteri alfanumerici.|  
|`(\w+\s?\w*)`|Trova uno o più caratteri alfanumerici seguiti da nessuno o uno spazio, seguito da nessuno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.|  
|`,?`|Trova nessuna o una occorrenza di un carattere virgola letterale.|  
  
 [Torna all'inizio](#top)  
  
<a name="WordBoundary"></a>   
## Confine di parola: \\b  
 L'ancoraggio `\b` specifica che la corrispondenza deve verificarsi in un confine tra un carattere alfanumerico \(elemento del linguaggio `\w`\) e uno non alfanumerico \(elemento del linguaggio `\W`\). I caratteri alfanumerici sono costituiti da lettere, cifre e caratteri di sottolineatura. Un carattere non alfanumerico è qualsiasi carattere diverso da lettere, cifre e carattere di sottolineatura. Per altre informazioni, vedere [Classi di caratteri](../../../docs/standard/base-types/character-classes-in-regular-expressions.md). La corrispondenza può verificarsi anche in un confine di parola all'inizio o alla fine della stringa.  
  
 L'ancoraggio `\b` viene usato di frequente per garantire che una sottoespressione corrisponda a un'intera parola anziché solo all'inizio o alla fine di una parola. L'espressione regolare `\bare\w*\b` nell'esempio seguente mostra questo utilizzo. L'espressione trova qualsiasi parola che inizia con la sottostringa "are". L'output dell'esempio mostra anche che `\b` trova sia l'inizio sia la fine della stringa di input.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/word1.cs#7)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/word1.vb#7)]  
  
 Il criterio di ricerca di espressioni regolari viene interpretato come illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`are`|Trova la sottostringa "are".|  
|`\w*`|Trova la corrispondenza di zero o più caratteri alfanumerici.|  
|`\b`|Termina la corrispondenza sul confine di parola.|  
  
 [Torna all'inizio](#top)  
  
<a name="NonwordBoundary"></a>   
## Carattere che non costituisce un confine di parola: \\B  
 L'ancoraggio `\B` specifica che la corrispondenza non deve verificarsi in un confine di parola. Si tratta dell'effetto contrario rispetto all'ancoraggio `\b`.  
  
 L'esempio seguente usa l'ancoraggio `\B` per individuare le occorrenze della sottostringa "qu" in una parola. Il criterio di espressione regolare `\Bqu\w+` trova una sottostringa che inizia con "qu" che non si trova all'inizio di una parola e che continua fino alla fine della parola.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/nonword1.cs#8)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/nonword1.vb#8)]  
  
 Il criterio di ricerca di espressioni regolari viene interpretato come illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\B`|La corrispondenza non deve iniziare nel confine di parola.|  
|`qu`|Trova la sottostringa "qu".|  
|`\w+`|Trova la corrispondenza di uno o più caratteri alfanumerici.|  
  
## Vedere anche  
 [Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)   
 [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md)