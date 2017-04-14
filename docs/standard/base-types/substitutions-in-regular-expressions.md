---
title: "Sostituzioni nelle espressioni regolari | Microsoft Docs"
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
  - "espressioni regolari di .NET Framework, sostituzioni"
  - "costrutti, sostituzioni"
  - "metacaratteri, sostituzioni"
  - "espressioni regolari, sostituzioni"
  - "modelli di sostituzione"
  - "sostituzioni"
ms.assetid: d1f52431-1c7d-4dc6-8792-6b988256892e
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Sostituzioni nelle espressioni regolari
<a name="Top"></a> Le sostituzioni sono elementi di linguaggio riconosciuti solo all'interno dei criteri di sostituzione. Utilizzano un modello di espressione regolare per definire in tutto o in parte il testo che sostituirà il testo corrispondente nella stringa di input. Il criterio di sostituzione può essere costituito da una o più sostituzioni insieme a caratteri letterali. I criteri di sostituzione vengono forniti agli overload del metodo <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=fullName> che dispongono di un parametro `replacement` e al metodo <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=fullName>. I metodi sostituiscono il criterio di ricerca con il criterio definito dal parametro `replacement`.  
  
 .NET Framework definisce gli elementi di sostituzione elencati nella tabella riportata di seguito.  
  
|Sostituzione|Descrizione|  
|------------------|-----------------|  
|`$` *numero*|Include nella stringa di sostituzione l'ultima sottostringa corrispondente al gruppo di acquisizione identificato da *numero* dove *numero* è un valore decimale. Per ulteriori informazioni, vedere [Sostituzione di un gruppo numerato](#Numbered).|  
|`${` *name* `}`|Include nella stringa di sostituzione l'ultima sottostringa corrispondente al gruppo denominato definito da `(?<`*nome*`> )`. Per ulteriori informazioni, vedere [Sostituzione di un gruppo denominato](#Named).|  
|`$$`|Include un solo simbolo letterale "$" nella stringa di sostituzione. Per ulteriori informazioni, vedere [Sostituzione di un simbolo "$"](#DollarSign).|  
|`$&`|Include una copia dell'intera corrispondenza nella stringa di sostituzione. Per ulteriori informazioni, vedere [Sostituzione dell'intera corrispondenza](#EntireMatch).|  
|`$``|Include nella stringa di sostituzione tutto il testo della stringa di input precedente alla corrispondenza. Per ulteriori informazioni, vedere [Sostituzione del testo prima della corrispondenza](#BeforeMatch).|  
|`$'`|Include nella stringa di sostituzione tutto il testo della stringa di input successivo alla corrispondenza. Per ulteriori informazioni, vedere [Sostituzione del testo dopo la corrispondenza](#AfterMatch).|  
|`$+`|Include nella stringa di sostituzione l'ultimo gruppo acquisito. Per ulteriori informazioni, vedere [Sostituzione dell'ultimo gruppo acquisito](#LastGroup).|  
|`$_`|Include l'intera stringa di input nella stringa di sostituzione. Per ulteriori informazioni, vedere [Sostituzione dell'intera stringa di input](#EntireString).|  
  
## Elementi di sostituzione e criteri di sostituzione  
 Le sostituzioni sono gli unici costrutti speciali riconosciuti in un criterio di sostituzione. Nessuno degli altri elementi del linguaggio delle espressioni regolari, compresi i caratteri di escape e il punto \(`.`\), che corrispondono a qualsiasi carattere, è supportato. Analogamente, gli elementi del linguaggio di sostituzione sono riconosciuti solo nei criteri di sostituzione e non sono mai validi nei modelli di espressioni regolari.  
  
 L'unico carattere che può essere utilizzato in un modello di espressione regolare o in una sostituzione è il carattere `$`, anche se presenta un significato diverso in ogni contesto. In un modello di espressione regolare `$` è un ancoraggio che corrisponde al termine della stringa. In un criterio di sostituzione, `$` indica l'inizio di una sostituzione.  
  
> [!NOTE]
>  Per una funzionalità simile a un criterio di sostituzione all'interno di un'espressione regolare, utilizzare un backreference. Per ulteriori informazioni sui backreference, vedere [Costrutti di backreference](../../../docs/standard/base-types/backreference-constructs-in-regular-expressions.md).  
  
<a name="Numbered"></a>   
## Sostituzione di un gruppo numerato  
 L'elemento di linguaggio `$`*numero* include l'ultima sottostringa corrispondente al gruppo di acquisizione *numero* nella stringa di sostituzione, dove *numero* è l'indice del gruppo di acquisizione. Ad esempio, il criterio di sostituzione `$1` indica che la sottostringa corrispondente deve essere sostituita dal primo gruppo acquisito. Per altre informazioni sui gruppi di acquisizione numerati, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
 Tutte le cifre che seguono `$` vengono interpretate come appartenenti al gruppo *numero*. Se questa non è la propria intenzione, è possibile sostituire un gruppo denominato invece. Ad esempio, è possibile utilizzare la stringa di sostituzione `${1}1` anziché `$11` per definire la stringa di sostituzione come la validità del gruppo innanzitutto acquisito con il numero "1 ". Per ulteriori informazioni, vedere [Sostituzione di un gruppo denominato](#Named).  
  
 I gruppi di acquisizione a cui non sono stati assegnati nomi in modo esplicito tramite la sintassi `(?<`*nome*`>)` vengono numerati da sinistra verso destra a partire da uno. I gruppi denominati sono anche numerati da sinistra a destra, a partire dall'indice dell'ultimo gruppo senza nome più uno. Ad esempio, nell'espressione regolare `(\w)(?<digit>\d)` l'indice del gruppo denominato `digit` è 2.  
  
 Se *numero* non specifica un gruppo di acquisizione valido definito nel criterio di espressione regolare, `$`*numero* viene interpretato come una sequenza di caratteri letterali usata per sostituire ogni corrispondenza.  
  
 Nell'esempio seguente viene usata la sostituzione `$`*numero*per rimuovere il simbolo di valuta da un valore decimale. Rimuove i simboli di valuta trovati all'inizio o alla fine di un valore valutario e riconosce i due separatori decimali più comuni \("." e ","\).  
  
 [!code-csharp[Conceptual.RegEx.Language.Substitutions#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/numberedgroup1.cs#1)]
 [!code-vb[Conceptual.RegEx.Language.Substitutions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/numberedgroup1.vb#1)]  
  
 Il criterio di ricerca di espressioni regolari `\p{Sc}*(\s?\d+[.,]?\d*)\p{Sc}*` è definito nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\p{Sc}*`|Trovare la corrispondenza con zero o più caratteri di simboli valutari.|  
|`\s?`|Trova la corrispondenza di uno o nessuno spazio vuoto.|  
|`\d+`|Trova la corrispondenza con una o più cifre decimali.|  
|`[.,]?`|Trova la corrispondenza con zero o con un punto o una virgola.|  
|`\d*`|Ricerca la corrispondenza di zero o di più cifre decimali.|  
|`(\s?\d+[.,]?\d*)`|Corrisponde a uno spazio vuoto seguito da una o più cifre decimali, seguite da zero o un punto o una virgola, seguita da zero o più cifre decimali. Equivale al primo gruppo di acquisizione. Poiché il criterio di sostituzione è `$1`, la chiamata al metodo <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=fullName> sostituisce la sottostringa corrispondente intera con questo gruppo acquisito.|  
  
 [Torna all'inizio](#Top)  
  
<a name="Named"></a>   
## Sostituzione di un gruppo denominato  
 L'elemento di linguaggio `${`*nome*`}` sostituisce l'ultima sottostringa corrispondente al gruppo di acquisizione *nome*, dove *nome* è il nome di un gruppo di acquisizione definito dall'elemento di linguaggio `(?<`*nome*`>)`. Per altre informazioni sui gruppi di acquisizione denominati, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
 Se *nome* non specifica un gruppo di acquisizione denominato valido definito nel criterio di espressione regolare ma è costituito dalle cifre, `${`*nome*`}` viene interpretato come un gruppo numerato.  
  
 Se *nome* non specifica un gruppo di acquisizione denominato valido o un gruppo di acquisizione numerato valido definito nel criterio di espressione regolare, `${`*nome*`}` viene interpretato come una sequenza di caratteri letterali usata per sostituire ogni corrispondenza.  
  
 Nell'esempio seguente viene usata la sostituzione `${`*nome*`}` per rimuovere il simbolo di valuta da un valore decimale. Rimuove i simboli di valuta trovati all'inizio o alla fine di un valore valutario e riconosce i due separatori decimali più comuni \("." e ","\).  
  
 [!code-csharp[Conceptual.RegEx.Language.Substitutions#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/namedgroup1.cs#2)]
 [!code-vb[Conceptual.RegEx.Language.Substitutions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/namedgroup1.vb#2)]  
  
 Il criterio di ricerca di espressioni regolari `\p{Sc}*(?<amount>\s?\d[.,]?\d*)\p{Sc}*` è definito nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\p{Sc}*`|Trovare la corrispondenza con zero o più caratteri di simboli valutari.|  
|`\s?`|Trova la corrispondenza di uno o nessuno spazio vuoto.|  
|`\d+`|Trova la corrispondenza con una o più cifre decimali.|  
|`[.,]?`|Trova la corrispondenza con zero o con un punto o una virgola.|  
|`\d*`|Ricerca la corrispondenza di zero o di più cifre decimali.|  
|`(?<amount>\s?\d[.,]?\d*)`|Corrisponde a uno spazio vuoto seguito da una o più cifre decimali, seguite da zero o un punto o una virgola, seguita da zero o più cifre decimali. Questo è il gruppo di acquisizione denominato `amount`. Poiché il criterio di sostituzione è `${amount}`, la chiamata al metodo <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=fullName> sostituisce la sottostringa corrispondente intera con questo gruppo acquisito.|  
  
 [Torna all'inizio](#Top)  
  
<a name="DollarSign"></a>   
## Sostituzione di un carattere "$"  
 La sostituzione `$$` inserisce un carattere "$" letterale nella stringa sostituita.  
  
 Nell'esempio riportato di seguito viene utilizzato l'oggetto <xref:System.Globalization.NumberFormatInfo> per determinare il simbolo di valuta delle impostazioni cultura correnti e la relativa posizione in una stringa di valuta. Compila quindi in modo dinamico sia un modello di espressione regolare sia un criterio di sostituzione. Se l'esempio viene eseguito in un computer le cui impostazioni cultura correnti sono en\-US, tale computer genera il criterio di espressione regolare `\b(\d+)(\.(\d+))?` e il criterio di sostituzione `$$ $1$2`. Il criterio di sostituzione sostituisce il testo corrispondente con un simbolo di valuta e uno spazio seguiti dal primo e dal secondo gruppo acquisito.  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/dollarsign1.cs#8)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/dollarsign1.vb#8)]  
  
 Il criterio di ricerca di espressioni regolari `\b(\d+)(\.(\d+))?` è definito nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia la corrispondenza all'inizio di un confine di parola.|  
|`(\d+)`|Trova la corrispondenza con una o più cifre decimali. Equivale al primo gruppo di acquisizione.|  
|`\.`|Trovare la corrispondenza con un punto \(ovvero il separatore decimale\).|  
|`(\d+)`|Trova la corrispondenza con una o più cifre decimali. Equivale al terzo gruppo di acquisizione.|  
|`(\.(\d+))?`|Trovare la corrispondenza con zero o una occorrenza di un punto seguito da una o più cifre decimali. Equivale al secondo gruppo di acquisizione.|  
  
<a name="EntireMatch"></a>   
## Sostituzione dell'intera corrispondenza  
 La sostituzione `$&` include l'intera corrispondenza nella stringa di sostituzione. Spesso viene utilizzata per aggiungere una sottostringa all'inizio o alla fine della stringa corrispondente. Ad esempio, il criterio di sostituzione `($&)` aggiunge parentesi all'inizio e alla fine di ogni corrispondenza. Se non esiste alcuna corrispondenza, la sostituzione `$&` non ha alcun effetto.  
  
 Nell'esempio seguente viene utilizzata la sostituzione `$&` per aggiungere virgolette all'inizio e alla fine dei titoli di libro archiviati in una matrice di stringhe.  
  
 [!code-csharp[Conceptual.RegEx.Language.Substitutions#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/entirematch1.cs#3)]
 [!code-vb[Conceptual.RegEx.Language.Substitutions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/entirematch1.vb#3)]  
  
 Il criterio di ricerca di espressioni regolari `^(\w+\s?)+$` è definito nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`^`|Inizia la corrispondenza all'inizio della stringa di input.|  
|`(\w+\s?)+`|Ottiene una o più volte la corrispondenza con il modello di uno o più caratteri alfanumerici seguiti da zero o da uno spazio vuoto.|  
|`$`|Trova la corrispondenza con la fine della stringa di input.|  
  
 Il criterio di sostituzione `"$&"` aggiunge le virgolette letterali all'inizio e alla fine di ogni corrispondenza.  
  
 [Torna all'inizio](#Top)  
  
<a name="BeforeMatch"></a>   
## Sostituzione del testo prima della corrispondenza  
 La sostituzione `$`` sostituisce la stringa corrispondente con l'intera stringa di input prima della corrispondenza. Ovvero, duplica la stringa di input fino alla corrispondenza e rimuove il testo corrispondente. Qualsiasi testo che segue il testo corrispondente resta invariato nella stringa di risultato. Se esistono più corrispondenze in una stringa di input, il testo di sostituzione viene derivato dalla stringa di input originale anziché dalla stringa in cui il testo è stato sostituito dalle corrispondenze precedenti. Nell'esempio viene illustrata una situazione di questo tipo. Se non esiste alcuna corrispondenza, la sostituzione `$`` non ha alcun effetto.  
  
 Nell'esempio seguente viene usato il criterio di espressione regolare `\d+` per trovare la corrispondenza con una sequenza di una o più cifre decimali nella stringa di input. La stringa di sostituzione `$`` sostituisce queste cifre con il testo che precede la corrispondenza.  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/before1.cs#4)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/before1.vb#4)]  
  
 In questo esempio, la stringa di input `"aa1bb2cc3dd4ee5"` contiene cinque corrispondenze. La tabella seguente illustra come la sostituzione `$`` fa in modo che il motore delle espressioni regolari sostituisca ogni corrispondenza nella stringa di input. Il testo inserito viene visualizzato in grassetto nella colonna dei risultati.  
  
|Corrispondenza con|Posizione|Stringa prima della corrispondenza|Stringa di risultato|  
|------------------------|---------------|----------------------------------------|--------------------------|  
|1|2|aa|aa`aa`bb2cc3dd4ee5|  
|2|5|aa1bb|aaaabb`aa1bb`cc3dd4ee5|  
|3|8|aa1bb2cc|aaaabbaa1bbcc`aa1bb2cc`dd4ee5|  
|4|11|aa1bb2cc3dd|aaaabbaa1bbccaa1bb2ccdd`aa1bb2cc3dd`ee5|  
|5|14|aa1bb2cc3dd4ee|aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddee `aa1bb2cc3dd4ee`|  
  
 [Torna all'inizio](#Top)  
  
<a name="AfterMatch"></a>   
## Sostituzione del testo dopo la corrispondenza  
 La sostituzione `$'` sostituisce la stringa corrispondente con l'intera stringa di input dopo la corrispondenza. Ovvero, duplica la stringa di input dopo la corrispondenza e rimuove il testo corrispondente. Qualsiasi testo che precede il testo corrispondente resta invariato nella stringa di risultato. Se non esiste alcuna corrispondenza, la sostituzione `$'` non ha alcun effetto.  
  
 Nell'esempio seguente viene usato il criterio di espressione regolare `\d+` per trovare la corrispondenza con una sequenza di una o più cifre decimali nella stringa di input. La stringa di sostituzione `$'` sostituisce queste cifre con il testo che segue la corrispondenza.  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/after1.cs#5)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/after1.vb#5)]  
  
 In questo esempio, la stringa di input `"aa1bb2cc3dd4ee5"` contiene cinque corrispondenze. La tabella seguente illustra come la sostituzione `$'` fa in modo che il motore delle espressioni regolari sostituisca ogni corrispondenza nella stringa di input. Il testo inserito viene visualizzato in grassetto nella colonna dei risultati.  
  
|Corrispondenza con|Posizione|Stringa dopo la corrispondenza|Stringa di risultato|  
|------------------------|---------------|------------------------------------|--------------------------|  
|1|2|bb2cc3dd4ee5|aa`bb2cc3dd4ee5`bb2cc3dd4ee5|  
|2|5|cc3dd4ee5|aabb2cc3dd4ee5bb`cc3dd4ee5`cc3dd4ee5|  
|3|8|dd4ee5|aabb2cc3dd4ee5bbcc3dd4ee5cc`dd4ee5`dd4ee5|  
|4|11|ee5|aabb2cc3dd4ee5bbcc3dd4ee5ccdd4ee5dd`ee5`ee5|  
|5|14|<xref:System.String.Empty?displayProperty=fullName>|aabb2cc3dd4ee5bbcc3dd4ee5ccdd4ee5ddee5ee|  
  
 [Torna all'inizio](#Top)  
  
<a name="LastGroup"></a>   
## Sostituzione dell'ultimo gruppo acquisito  
 La sostituzione `$+` sostituisce la stringa corrispondente con l'ultimo gruppo acquisito. Se non esistono gruppi acquisiti o se il valore dell'ultimo gruppo acquisito è <xref:System.String.Empty?displayProperty=fullName>, la sostituzione `$+` non ha effetto.  
  
 L'esempio seguente identifica le parole duplicate in una stringa e utilizza la sostituzione `$+` per sostituirle con una sola occorrenza della parola. L'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> viene utilizzata per garantire che le parole che differiscono solo in termini di maiuscole e minuscole siano considerate come parole duplicate.  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/lastmatch1.cs#6)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/lastmatch1.vb#6)]  
  
 Il criterio di ricerca di espressioni regolari `\b(\w+)\s\1\b` è definito nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`(\w+)`|Trova la corrispondenza di uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.|  
|`\s`|Trova la corrispondenza con uno spazio vuoto.|  
|`\1`|Trovare la corrispondenza con il primo gruppo acquisito.|  
|`\b`|Termina la corrispondenza sul confine di parola.|  
  
 [Torna all'inizio](#Top)  
  
<a name="EntireString"></a>   
## Sostituzione dell'intera stringa di input  
 La sostituzione `$_` sostituisce la stringa corrispondente con l'intera stringa di input. Ovvero, rimuove il testo corrispondente e lo sostituisce con la stringa intera, compreso il testo corrispondente.  
  
 Nell'esempio seguente vengono corrisposte una o più cifre decimali della stringa di input. Utilizza la sostituzione `$_` per sostituirli con l'intera stringa di input.  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/entire1.cs#7)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/entire1.vb#7)]  
  
 In questo esempio, la stringa di input `"ABC123DEF456"` contiene due corrispondenze. La tabella seguente illustra come la sostituzione `$_` fa in modo che il motore delle espressioni regolari sostituisca ogni corrispondenza nella stringa di input. Il testo inserito viene visualizzato in grassetto nella colonna dei risultati.  
  
|Corrispondenza con|Posizione|Corrispondenza con|Stringa di risultato|  
|------------------------|---------------|------------------------|--------------------------|  
|1|3|123|ABC`ABC123DEF456`DEF456|  
|2|5|456|ABCABC123DEF456DEF`ABC123DEF456`|  
  
## Vedere anche  
 [Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)