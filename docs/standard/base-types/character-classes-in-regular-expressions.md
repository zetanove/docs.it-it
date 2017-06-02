---
title: "Classi di caratteri nelle espressioni regolari | Microsoft Docs"
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
  - "espressioni regolari di .NET Framework, classi di caratteri"
  - "classi di caratteri"
  - "caratteri, sintassi corrispondente"
  - "espressioni regolari, classi di caratteri"
ms.assetid: 0f8bffab-ee0d-4e0e-9a96-2b4a252bb7e4
caps.latest.revision: 58
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 52
---
# Classi di caratteri nelle espressioni regolari
Una classe di caratteri definisce un set di caratteri, di cui uno qualsiasi può verificarsi in una stringa di input per trovare una corrispondenza.  Il linguaggio delle espressioni regolari di .NET Framework supporta le seguenti classi di caratteri:  
  
-   Gruppi di caratteri positivi.  Un carattere nella stringa di input deve corrispondere a un set di caratteri specificato.  Per altre informazioni, vedere [Gruppo di caratteri positivi](#PositiveGroup).  
  
-   Gruppi di caratteri negativi.  Un carattere nella stringa di input non deve corrispondere a un set di caratteri specificato.  Per altre informazioni, vedere [Gruppo di caratteri negativi](#NegativeGroup).  
  
-   Qualsiasi carattere.  Il carattere `.` \(punto\) in un'espressione regolare è un carattere jolly che corrisponde a qualsiasi carattere, eccetto `\n`.  Per altre informazioni, vedere [Qualsiasi carattere](#AnyCharacter).  
  
-   Categoria generale Unicode o blocco denominato.  Per trovare una corrispondenza, un carattere nella stringa di input deve appartenere a una particolare categoria Unicode o essere compreso in un intervallo contiguo di caratteri Unicode.  Per altre informazioni, vedere [Categoria Unicode o blocco Unicode](#CategoryOrBlock).  
  
-   Categoria Unicode generale o blocco denominato.  Per trovare una corrispondenza, un carattere nella stringa di input non deve appartenere a una particolare categoria Unicode o non deve essere compreso in un intervallo contiguo di caratteri Unicode.  Per altre informazioni, vedere [Categoria Unicode negativa o blocco Unicode](#NegativeCategoryOrBlock).  
  
-   Carattere alfanumerico.  Un carattere nella stringa di input può appartenere a qualsiasi categoria Unicode appropriata per i caratteri alfanumerico.  Per altre informazioni, vedere [Carattere alfanumerico](#WordCharacter).  
  
-   Carattere non alfanumerico.  Un carattere nella stringa di input può appartenere a qualsiasi categoria Unicode che non sia un carattere alfanumerico.  Per altre informazioni, vedere [Carattere non alfanumerico](#NonWordCharacter).  
  
-   Spazio vuoto.  Un carattere nella stringa di input può essere qualsiasi carattere separatore Unicode, nonché un numero qualsiasi di caratteri di controllo.  Per altre informazioni, vedere [Spazio vuoto](#WhitespaceCharacter).  
  
-   Carattere diverso da uno spazio vuoto.  Un carattere nella stringa di input può essere qualsiasi carattere diverso da uno spazio vuoto.  Per altre informazioni, vedere [Carattere diverso da uno spazio vuoto](#NonWhitespaceCharacter).  
  
-   Cifra decimale.  Un carattere nella stringa di input può essere qualsiasi numero di caratteri classificati come cifre decimali Unicode.  Per altre informazioni, vedere [Carattere decimale numerico](#DigitCharacter).  
  
-   Cifra non decimale.  Un carattere nella stringa di input può essere qualsiasi carattere tranne una cifra decimale Unicode.  Per altre informazioni, vedere [Carattere decimale numerico](#NonDigitCharacter).  
  
 .NET Framework supporta espressioni di sottrazione di classi di caratteri che consentono di definire un set di caratteri come risultato dell'esclusione di una classe di caratteri da un'altra classe di caratteri.  Per altre informazioni, vedere [Sottrazione di classi di caratteri](#CharacterClassSubtraction).  
  
<a name="PositiveGroup"></a>   
## Gruppo di caratteri positivi: \[ \]  
 Un gruppo di caratteri positivi specifica un elenco di caratteri che possono essere presenti in una stringa di input per trovare una corrispondenza.  È possibile specificare l'elenco di caratteri singolarmente, come intervallo o entrambi.  
  
 Di seguito viene indicata la sintassi per specificare un elenco di singoli caratteri:  
  
 \[*character\_group*\]  
  
 dove  *character\_group* è un elenco dei singoli caratteri che possono apparire nella stringa di input affinché una corrispondenza riesca.  *character\_group* può contenere qualsiasi combinazione di uno o più caratteri letterali, [caratteri di escape](../../../docs/standard/base-types/character-escapes-in-regular-expressions.md) o classi di caratteri.  
  
 Di seguito viene indicata la sintassi per specificare un intervallo di caratteri:  
  
```  
[firstCharacter-lastCharacter]  
```  
  
 dove *firstCharacter* è il carattere che inizia l'intervallo e *lastCharacter* è il carattere che lo termina.  Un intervallo di caratteri è una serie contigua di caratteri definita specificando il primo carattere della serie, un trattino \(\-\), quindi l'ultimo carattere della serie.  Due caratteri sono contigui se hanno punti di codice Unicode adiacenti.  
  
 Nella tabella seguente sono elencati alcuni criteri di espressione regolare comuni contenenti classi di caratteri positivi.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`[aeiou]`|Corrisponde a tutte le vocali.|  
|`[\p{P}\d]`|Corrisponde a tutti i caratteri di punteggiatura e tutte le cifre decimali.|  
|`[\s\p{P}]`|Corrisponde a tutti gli spazi vuoti e ai caratteri di punteggiatura.|  
  
 Nell'esempio seguente viene definito un gruppo di caratteri positivi contenente i caratteri "a" ed "e" in modo che la stringa di input contenga obbligatoriamente le parole "grey" o "gray" seguite da un'altra parola perché si verifichi una corrispondenza.  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/positivecharclasses.cs#1)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/positivecharclasses.vb#1)]  
  
 L'espressione regolare `gr[ae]y\s\S+?[\s|\p{P}]` viene definita come segue:  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`gr`|Corrisponde ai caratteri letterali "gr".|  
|`[ae]`|Corrisponde a una "a" o una "e".|  
|`y\s`|Corrisponde al carattere letterale "y" seguito da uno spazio vuoto.|  
|`\S+?`|Corrisponde a uno o più spazi vuoti, ma al minor numero possibile.|  
|`[\s\p{P}]`|Corrisponde a uno spazio vuoto o a un segno di punteggiatura.|  
  
 Le corrispondenze dell'esempio seguente sono relative a parole che iniziano con una lettera maiuscola qualsiasi.  Viene usata la sottoespressione `[A-Z]` per rappresentare l'intervallo di lettere maiuscole da A a Z.  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/range.cs#3)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/range.vb#3)]  
  
 L'espressione regolare `\b[A-Z]\w*\b` viene definita come illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia dal confine di una parola.|  
|`[A-Z]`|Corrisponde a qualsiasi carattere maiuscolo da A a Z.|  
|`\w*`|Trova la corrispondenza di zero o più caratteri alfanumerici.|  
|`\b`|Trova la corrispondenza di un confine di parola.|  
  
 [Torna all'inizio](#Top)  
  
<a name="NegativeGroup"></a>   
## Gruppo di caratteri negativi: \[^\]  
 Un gruppo di caratteri negativi specifica un elenco di caratteri che non devono essere presenti in una stringa di input per trovare una corrispondenza.  È possibile specificare l'elenco di caratteri singolarmente, come intervallo o entrambi.  
  
 Di seguito viene indicata la sintassi per specificare un elenco di singoli caratteri:  
  
 \[*^character\_group*\]  
  
 dove  *character\_group* è un elenco dei singoli caratteri che non possono apparire nella stringa di input affinché una corrispondenza riesca.  *character\_group* può contenere qualsiasi combinazione di uno o più caratteri letterali, [caratteri di escape](../../../docs/standard/base-types/character-escapes-in-regular-expressions.md) o classi di caratteri.  
  
 Di seguito viene indicata la sintassi per specificare un intervallo di caratteri:  
  
 \[^*firstCharacter*\-*lastCharacter*\]  
  
 dove *firstCharacter* è il carattere che inizia l'intervallo e *lastCharacter* è il carattere che lo termina.  Un intervallo di caratteri è una serie contigua di caratteri definita specificando il primo carattere della serie, un trattino \(\-\), quindi l'ultimo carattere della serie.  Due caratteri sono contigui se hanno punti di codice Unicode adiacenti.  
  
 Due o più intervalli di caratteri possono essere concatenati.  Ad esempio, per specificare l'intervallo di cifre decimali comprese tra "0" e "9", l'intervallo di lettere minuscole comprese tra "a" e "f" e l'intervallo di lettere maiuscole comprese tra "A" e "F", usare `[0-9a-fA-F]`.  
  
 L'accento circonflesso iniziale \(`^`\) in un gruppo di caratteri negativi è obbligatorio e indica che tale gruppo è un gruppo di caratteri negativi anziché un gruppo di caratteri positivi.  
  
> [!IMPORTANT]
>  Un gruppo di caratteri negativi in un criterio di ricerca di espressioni regolari più grande non è un'asserzione di larghezza zero.  Ovvero, dopo avere valutato il gruppo di caratteri negativi, il motore delle espressioni regolari avanza di un carattere nella stringa di input.  
  
 Nella tabella seguente sono elencati alcuni criteri di espressione regolare comuni contenenti gruppi di caratteri negativi.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`[^aeiou]`|Corrisponde a tutti i caratteri eccetto le vocali.|  
|`[^\p{P}\d]`|Corrisponde a tutti i caratteri eccetto caratteri di punteggiatura e cifre decimali.|  
  
 Le corrispondenze dell'esempio seguente sono relative a tutte le parole che iniziano con i caratteri "th" e non sono seguite dalla lettera "o".  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/negativecharclasses.cs#2)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/negativecharclasses.vb#2)]  
  
 L'espressione regolare `\bth[^o]\w+\b` viene definita come illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia dal confine di una parola.|  
|`th`|Corrisponde ai caratteri letterali "th".|  
|`[^o]`|Corrisponde a tutti i caratteri diversi da "o".|  
|`\w+`|Trova la corrispondenza di uno o più caratteri alfanumerici.|  
|`\b`|Terminare al confine di una parola.|  
  
 [Torna all'inizio](#Top)  
  
<a name="AnyCharacter"></a>   
## Qualsiasi carattere: .  
 Il carattere punto \(.\) corrisponde a qualsiasi carattere eccetto `\n` \(carattere di nuova riga, \\u000A\), con le due qualificazioni seguenti:  
  
-   Se un criterio di ricerca di espressioni regolari viene modificato dall'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> o se la parte del criterio contenente la classe di caratteri `.` viene modificata dall'opzione `s`, `.` corrisponde a qualsiasi carattere.  Per altre informazioni, vedere [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).  
  
     Nell'esempio seguente viene illustrato il diverso comportamento della classe di caratteri `.` per impostazione predefinita e con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>.  L'espressione regolare `^.+` parte dall'inizio della stringa e individua una corrispondenza per ogni carattere.  Per impostazione predefinita, la corrispondenza termina alla fine della prima riga. Il criterio di ricerca di espressioni regolari trova la corrispondenza del carattere di ritorno a capo, `\r` o \\u000D, ma non di `\n`.  Poiché l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> interpreta l'intera stringa di input come riga singola, ottiene una corrispondenza per ogni carattere nella stringa di input, incluso `\n`.  
  
     [!code-csharp[Conceptual.Regex.Language.CharacterClasses#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/any2.cs#5)]
     [!code-vb[Conceptual.Regex.Language.CharacterClasses#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/any2.vb#5)]  
  
> [!NOTE]
>  Poiché corrisponde a qualsiasi carattere eccetto `\n`, la classe di caratteri `.` corrisponde anche a `\r` \(il carattere di ritorno a capo, \\u000D\).  
  
-   In un gruppo di caratteri positivi o negativi un punto viene interpretato come carattere punto letterale e non come classe di caratteri.  Per altre informazioni, vedere [Gruppo di caratteri positivi](#PositiveGroup) e [Gruppo di caratteri negativi](#NegativeGroup) descritti in precedenza in questo argomento.  Nell'esempio seguente viene fornita un'illustrazione mediante la definizione di un'espressione regolare che include il carattere punto \(`.`\) sia come classe di caratteri che come membro di un gruppo di caratteri positivi.  L'espressione regolare `\b.*[.?!;:](\s|\z)` inizia in corrispondenza di confine di parola, corrisponde a qualsiasi carattere fino a quando non incontra uno dei quattro segni di punteggiatura, incluso un punto, quindi individua la corrispondenza con uno spazio vuoto o con la fine della stringa.  
  
     [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/any1.cs#4)]
     [!code-vb[Conceptual.RegEx.Language.CharacterClasses#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/any1.vb#4)]  
  
> [!NOTE]
>  Poiché corrisponde a qualsiasi carattere, l'elemento di linguaggio `.` viene spesso usato con un quantificatore lazy se un criterio di ricerca di espressioni regolari tenta di ottenere più volte una corrispondenza con ogni carattere.  Per altre informazioni, vedere [Quantificatori](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md).  
  
 [Torna all'inizio](#Top)  
  
<a name="CategoryOrBlock"></a>   
## Categoria Unicode o blocco Unicode: \\p{}  
 Lo standard Unicode assegna una categoria generale a ogni carattere.  Ad esempio, un carattere particolare può essere una lettera maiuscola \(rappresentata dalla categoria `Lu`\), una cifra decimale \(la categoria `Nd`\), un simbolo matematico \(la categoria `Sm`\) o un separatore di paragrafo \(la categoria `Zl`\).  Anche set di caratteri specifici nello standard Unicode occupano un intervallo specifico o un blocco di punti di codice consecutivi.  Il set di caratteri latini si trova ad esempio da \\u0000 a \\u007F, mentre il set di caratteri arabi si trova da \\u0600 a \\u06FF.  
  
 Costrutto dell'espressione regolare  
  
 `\p{` *name* `}`  
  
 corrisponde a qualsiasi carattere appartenente a una categoria generale Unicode o a un blocco denominato, dove *name* è l'abbreviazione della categoria o il nome del blocco denominato.  Per un elenco di abbreviazioni della categoria, vedere la sezione [Categorie generali Unicode supportate](#SupportedUnicodeGeneralCategories) più avanti in questo argomento.  Per un elenco dei blocchi denominati, vedere la sezione [Blocchi denominati supportati](#SupportedNamedBlocks) più avanti in questo argomento.  
  
 Nell'esempio seguente viene usato il costrutto `\p{`*name*`}` per individuare una corrispondenza per una categoria generale Unicode \(in questo caso la categoria `Pd` o Punctuation, Dash\) e un blocco denominato \(i blocchi denominati `IsGreek` e `IsBasicLatin`\).  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/category1.cs#6)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/category1.vb#6)]  
  
 L'espressione regolare `\b(\p{IsGreek}+(\s)?)+\p{Pd}\s(\p{IsBasicLatin}+(\s)?)+` viene definita come illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia dal confine di una parola.|  
|`\p{IsGreek}+`|Corrisponde a uno o più caratteri greci.|  
|`(\s)?`|Trova la corrispondenza di uno o nessuno spazio vuoto.|  
|`(\p{IsGreek}+(\s)?)+`|Ottiene una o più volte la corrispondenza con il modello di uno o più caratteri greci seguiti da zero o da uno spazio vuoto.|  
|`\p{Pd}`|Corrisponde a un carattere "Pd" \(Punctuation, Dash\).|  
|`\s`|Trova la corrispondenza con uno spazio vuoto.|  
|`\p{IsBasicLatin}+`|Corrisponde a uno o più caratteri latini di base.|  
|`(\s)?`|Trova la corrispondenza di uno o nessuno spazio vuoto.|  
|`(\p{IsBasicLatin}+(\s)?)+`|Ottiene una o più volte la corrispondenza con il modello di uno o più caratteri latini di base seguiti da zero o da uno spazio vuoto.|  
  
 [Torna all'inizio](#Top)  
  
<a name="NegativeCategoryOrBlock"></a>   
## Categoria Unicode negativa o blocco Unicode: \\P {}  
 Lo standard Unicode assegna una categoria generale a ogni carattere.  Ad esempio, un carattere particolare può essere una lettera maiuscola \(rappresentata dalla categoria `Lu`\), una cifra decimale \(la categoria `Nd`\), un simbolo matematico \(la categoria `Sm`\) o un separatore di paragrafo \(la categoria `Zl`\).  Anche set di caratteri specifici nello standard Unicode occupano un intervallo specifico o un blocco di punti di codice consecutivi.  Il set di caratteri latini si trova ad esempio da \\u0000 a \\u007F, mentre il set di caratteri arabi si trova da \\u0600 a \\u06FF.  
  
 Costrutto dell'espressione regolare  
  
 `\P{` *name* `}`  
  
 corrisponde a qualsiasi carattere non appartenente a una categoria generale Unicode o a un blocco denominato, dove *name* è l'abbreviazione della categoria o il nome del blocco denominato.  Per un elenco di abbreviazioni della categoria, vedere la sezione [Categorie generali Unicode supportate](#SupportedUnicodeGeneralCategories) più avanti in questo argomento.  Per un elenco dei blocchi denominati, vedere la sezione [Blocchi denominati supportati](#SupportedNamedBlocks) più avanti in questo argomento.  
  
 L'esempio seguente usa il costrutto `\P{`*name*`}` per rimuovere qualsiasi simbolo di valuta \(in questo caso la categoria `Sc` o Symbol, Currency\) dalle stringhe numeriche.  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/notcategory1.cs#7)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/notcategory1.vb#7)]  
  
 Il criterio di ricerca di espressioni regolari `(\P{Sc})+` corrisponde a uno o più caratteri che non siano simboli di valuta e rimuove efficacemente qualsiasi simbolo di valuta dalla stringa del risultato.  
  
 [Torna all'inizio](#Top)  
  
<a name="WordCharacter"></a>   
## Carattere alfanumerico: \\w  
 `\w` trova la corrispondenza con qualsiasi carattere alfanumerico.  Un carattere alfanumerico è un membro di una delle categorie Unicode elencate nella seguente tabella.  
  
|Categoria|Descrizione|  
|---------------|-----------------|  
|Ll|Letter, Lowercase|  
|Lu|Letter, Uppercase|  
|Lt|Letter, Titlecase|  
|Lo|Letter, Other|  
|Lm|Letter, Modifier|  
|Nd|Number, Decimal Digit|  
|Pc|Punctuation, Connector.  Questa categoria include dieci caratteri, tra cui quello più comunemente usato è \(\_\) LOWLINE, u\+005F.|  
  
 Se viene specificato il comportamento conforme a ECMAScript, `\w` equivale a `[a-zA-Z_0-9]`.  Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione "Comportamento della corrispondenza ECMAScript" in [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).  
  
> [!NOTE]
>  Poiché corrisponde a qualsiasi carattere alfanumerico, l'elemento di linguaggio `\w` viene spesso usato con un quantificatore lazy se un criterio di ricerca di espressioni regolari tenta di ottenere più volte una corrispondenza con ogni carattere alfanumerico, seguito da un carattere alfanumerico specifico.  Per altre informazioni, vedere [Quantificatori](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md).  
  
 Nell'esempio seguente viene usato l'elemento di linguaggio `\w` per individuare una corrispondenza con i caratteri duplicati in una parola.  L'esempio definisce un criterio di ricerca di espressioni regolari, `(\w)\1`, che può essere interpretato nel modo seguente.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|\(\\w\)|Corrisponde a un carattere alfanumerico.  Equivale al primo gruppo di acquisizione.|  
|\\1|Corrisponde al valore della prima acquisizione.|  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/wordchar1.cs#8)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/wordchar1.vb#8)]  
  
 [Torna all'inizio](#Top)  
  
<a name="NonWordCharacter"></a>   
## Carattere non alfanumerico: \\W  
 `\W` trova la corrispondenza con qualsiasi carattere non alfanumerico.  L'elemento di linguaggio \\W è equivalente alla classe di caratteri seguente:  
  
```  
[^\p{Ll}\p{Lu}\p{Lt}\p{Lo}\p{Nd}\p{Pc}\p{Lm}]  
```  
  
 In altre parole, corrisponde a tutti i caratteri, ad eccezione di quelli elencati nella tabella seguente.  
  
|Categoria|Descrizione|  
|---------------|-----------------|  
|Ll|Letter, Lowercase|  
|Lu|Letter, Uppercase|  
|Lt|Letter, Titlecase|  
|Lo|Letter, Other|  
|Lm|Letter, Modifier|  
|Nd|Number, Decimal Digit|  
|Pc|Punctuation, Connector.  Questa categoria include dieci caratteri, tra cui quello più comunemente usato è \(\_\) LOWLINE, u\+005F.|  
  
 Se viene specificato il comportamento conforme a ECMAScript, `\W` equivale a `[^a-zA-Z_0-9]`.  Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione "Comportamento della corrispondenza ECMAScript" in [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).  
  
> [!NOTE]
>  Poiché corrisponde a qualsiasi carattere non alfanumerico, l'elemento di linguaggio `\W` viene spesso usato con un quantificatore lazy se un criterio di ricerca di espressioni regolari tenta di ottenere più volte una corrispondenza con ogni carattere non alfanumerico, seguito da un carattere non alfanumerico specifico.  Per altre informazioni, vedere [Quantificatori](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md).  
  
 L'esempio seguente illustra la classe di caratteri `\W`.  Definisce un criterio di ricerca di espressioni regolari, `\b(\w+)(\W){1,2}`, che corrisponde a una parola seguita da uno o due caratteri non alfanumerici, ad esempio uno spazio vuoto o un segno di punteggiatura.  L'espressione regolare viene interpretata come illustrato nella tabella seguente.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|\\b|Inizia la corrispondenza sul confine di parola.|  
|\(\\w\+\)|Trova la corrispondenza di uno o più caratteri alfanumerici.  Equivale al primo gruppo di acquisizione.|  
|\(\\W\){1,2}|Ottiene una o due volte una corrispondenza con un carattere non alfanumerico.  Equivale al secondo gruppo di acquisizione.|  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/nonwordchar1.cs#9)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/nonwordchar1.vb#9)]  
  
 Poiché l'oggetto <xref:System.Text.RegularExpressions.Group> per il secondo gruppo di acquisizione contiene un solo carattere non alfanumerico acquisito, nell'esempio vengono recuperati tutti i caratteri non alfanumerici acquisiti dall'oggetto <xref:System.Text.RegularExpressions.CaptureCollection> restituito dalla proprietà <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=fullName>.  
  
 [Torna all'inizio](#Top)  
  
<a name="WhitespaceCharacter"></a>   
## Spazio vuoto: \\s  
 `\s` trova la corrispondenza con qualsiasi spazio vuoto.  È equivalente alle sequenze di escape e alle categorie Unicode elencate nella tabella seguente.  
  
|Categoria|Descrizione|  
|---------------|-----------------|  
|`\f`|Carattere di avanzamento modulo, \\u000C.|  
|`\n`|Carattere di nuova riga, \\u000A.|  
|`\r`|Carattere di ritorno a capo, \\u000D.|  
|`\t`|Carattere di tabulazione, \\u0009.|  
|`\v`|Carattere di tabulazione verticale, \\u000B.|  
|`\x85`|Puntini di sospensione o carattere NEXT LINE \(NEL\) \(...\), \\u0085.|  
|`\p{Z}`|Corrisponde a qualsiasi carattere separatore.|  
  
 Se viene specificato il comportamento conforme a ECMAScript, `\s` equivale a `[\f\n\r\t\v]`.  Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione "Comportamento della corrispondenza ECMAScript" in [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).  
  
 L'esempio seguente illustra la classe di caratteri `\s`.  Definisce un criterio di ricerca di espressioni regolari, `\b\w+(e)?s(\s|$)`, che corrisponde a una parola che termina in "s" o "es" seguita da uno spazio vuoto o dalla fine della stringa di input.  L'espressione regolare viene interpretata come illustrato nella tabella seguente.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|\\b|Inizia la corrispondenza sul confine di parola.|  
|\\w\+|Trova la corrispondenza di uno o più caratteri alfanumerici.|  
|\(e\)?|Ottiene zero o una volta la corrispondenza con una "e".|  
|s|Corrisponde a una "s".|  
|\(\\s&#124;$\)|Corrisponde a uno spazio vuoto o alla fine della stringa di input.|  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/whitespace1.cs#10)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/whitespace1.vb#10)]  
  
 [Torna all'inizio](#Top)  
  
<a name="NonWhitespaceCharacter"></a>   
## Carattere diverso da uno spazio vuoto: \\S  
 `\S` trova la corrispondenza con qualsiasi carattere diverso da uno spazio.  È equivalente al criterio di ricerca di espressioni regolari `[^\f\n\r\t\v\x85\p{Z}]` o è il contrario del criterio di ricerca di espressioni regolari equivalente a `\s`, che corrisponde a spazi vuoti.  Per altre informazioni, vedere [Spazio vuoto: \\s](#WhitespaceCharacter).  
  
 Se viene specificato il comportamento conforme a ECMAScript, `\S` equivale a `[^ \f\n\r\t\v]`.  Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione "Comportamento della corrispondenza ECMAScript" in [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).  
  
 L'esempio seguente illustra l'elemento di linguaggio `\S`.  Il criterio di espressione regolare `\b(\S+)\s?` corrisponde a stringhe delimitate da spazi vuoti.  Il secondo elemento nell'oggetto <xref:System.Text.RegularExpressions.GroupCollection> della corrispondenza contiene la stringa corrispondente.  L'espressione regolare può essere interpretata come indicato nella tabella seguente.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`(\S+)`|Trova la corrispondenza con uno o più caratteri diversi dallo spazio vuoto.  Equivale al primo gruppo di acquisizione.|  
|`\s?`|Trova la corrispondenza di uno o nessuno spazio vuoto.|  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/nonwhitespace1.cs#11)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/nonwhitespace1.vb#11)]  
  
 [Torna all'inizio](#Top)  
  
<a name="DigitCharacter"></a>   
## Carattere cifra decimale: \\d  
 `\d` trova la corrispondenza con qualsiasi cifra decimale.  È equivalente al criterio di ricerca di espressioni regolari `\p{Nd}` che include le cifre decimali standard da 0 a 9 e le cifre decimali di diversi altri set di caratteri.  
  
 Se viene specificato il comportamento conforme a ECMAScript, `\d` equivale a `[0-9]`.  Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione "Comportamento della corrispondenza ECMAScript" in [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).  
  
 L'esempio seguente illustra l'elemento di linguaggio `\d`.  Viene verificato se una stringa di input rappresenta un numero di telefono valido negli Stati Uniti e in Canada.  Il criterio di ricerca di espressioni regolari `^(\(?\d{3}\)?[\s-])?\d{3}-\d{4}$` è definito nel modo illustrato nella tabella seguente.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`^`|Inizia la corrispondenza all'inizio della stringa di input.|  
|`\(?`|Corrisponde a zero o a un carattere letterale "\(".|  
|`\d{3}`|Trova la corrispondenza con tre cifre decimali.|  
|`\)?`|Corrisponde a zero o a un carattere letterale "\)".|  
|`[\s-]`|Corrisponde a un trattino o a uno spazio vuoto.|  
|`(\(?  \d{3}\)?[\s-])?`|Trova la corrispondenza zero o una volta con una parentesi di apertura facoltativa seguita da tre cifre decimali, una parentesi di chiusura facoltativa e uno spazio vuoto o un trattino.  Equivale al primo gruppo di acquisizione.|  
|`\d{3}-\d{4}`|Corrisponde a tre cifre decimali seguite da un trattino e da altre quattro cifre decimali.|  
|`$`|Trova la corrispondenza con la fine della stringa di input.|  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/digit1.cs#12)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/digit1.vb#12)]  
  
 [Torna all'inizio](#Top)  
  
<a name="NonDigitCharacter"></a>   
## Carattere non numerico: \\D  
 `\D` trova la corrispondenza con qualsiasi carattere non numerico.  È equivalente al criterio di ricerca di espressioni regolari `\P{Nd}`.  
  
 Se viene specificato il comportamento conforme a ECMAScript, `\D` equivale a `[^0-9]`.  Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione "Comportamento della corrispondenza ECMAScript" in [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).  
  
 Nell'esempio seguente viene illustrato l'elemento di linguaggio \\D.  Verifica se una stringa, ad esempio un numero parte, è formata dalla combinazione corretta di caratteri decimali e non decimali.  Il criterio di ricerca di espressioni regolari `^\D\d{1,5}\D*$` è definito nel modo illustrato nella tabella seguente.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`^`|Inizia la corrispondenza all'inizio della stringa di input.|  
|`\D`|Corrisponde a un carattere non numerico.|  
|`\d{1,5}`|Corrisponde a una fino a cinque cifre decimali.|  
|`\D*`|Corrisponde a zero, uno o più caratteri non decimali.|  
|`$`|Trova la corrispondenza con la fine della stringa di input.|  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/nondigit1.cs#13)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/nondigit1.vb#13)]  
  
 [Torna all'inizio](#Top)  
  
<a name="SupportedUnicodeGeneralCategories"></a>   
## Categorie generali Unicode supportate  
 In Unicode sono definite le categorie generali elencate nella tabella riportata di seguito.  Per altre informazioni, vedere le sezioni relative al formato di File UCD e ai valori di categoria generale nel [database di caratteri unicode](http://go.microsoft.com/fwlink/?LinkId=57650).  
  
|Categoria|Descrizione|  
|---------------|-----------------|  
|`Lu`|Letter, Uppercase|  
|`Ll`|Letter, Lowercase|  
|`Lt`|Letter, Titlecase|  
|`Lm`|Letter, Modifier|  
|`Lo`|Letter, Other|  
|`L`|Tutti i caratteri alfanumerici.  Sono inclusi i caratteri `Lu`, `Ll`, `Lt`, `Lm` e `Lo`.|  
|`Mn`|Mark, Nonspacing|  
|`Mc`|Mark, Spacing Combining|  
|`Me`|Mark, Enclosing|  
|`M`|Tutti i contrassegni diacritici.  Sono incluse le categorie `Mn`, `Mc` e `Me`.|  
|`Nd`|Number, Decimal Digit|  
|`Nl`|Number, Letter|  
|`No`|Number, Other|  
|`N`|Tutti i numeri.  Sono incluse le categorie `Nd`, `Nl` e `No`.|  
|`Pc`|Punctuation, Connector|  
|`Pd`|Punctuation, Dash|  
|`Ps`|Punctuation, Open|  
|`Pe`|Punctuation, Close|  
|`Pi`|Punctuation, Initial quote \(può comportarsi come Ps o Pe a seconda dell'utilizzo\)|  
|`Pf`|Punctuation, Final quote \(può comportarsi come Ps o Pe a seconda dell'utilizzo\)|  
|`Po`|Punctuation, Other|  
|`P`|Tutti i caratteri di punteggiatura.  Sono incluse le categorie `Pc`, `Pd`, `Ps`, `Pe`, `Pi`, `Pf` e `Po`.|  
|`Sm`|Symbol, Math|  
|`Sc`|Symbol, Currency|  
|`Sk`|Symbol, Modifier|  
|`So`|Symbol, Other|  
|`S`|Tutti i simboli.  Sono incluse le categorie `Sm`, `Sc`, `Sk` e `So`.|  
|`Zs`|Separator, Space|  
|`Zl`|Separator, Line|  
|`Zp`|Separator, Paragraph|  
|`Z`|Tutti i caratteri separatori.  Sono incluse le categorie `Zs`, `Zl` e `Zp`.|  
|`Cc`|Other, Control|  
|`Cf`|Other, Format|  
|`Cs`|Other, Surrogate|  
|`Co`|Other, Private Use|  
|`Cn`|Other, Not Assigned \(nessun carattere ha questa proprietà\)|  
|`C`|Tutti i caratteri di controllo.  Sono incluse le categorie `Cc`, `Cf`, `Cs`, `Co` e `Cn`.|  
  
 È possibile determinare la categoria Unicode di qualsiasi particolare carattere passando tale carattere al metodo <xref:System.Char.GetUnicodeCategory%2A>.  L'esempio seguente usa il metodo <xref:System.Char.GetUnicodeCategory%2A> per determinare la categoria di ogni elemento in una matrice che contiene caratteri latini selezionati.  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/getunicodecategory1.cs#14)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/getunicodecategory1.vb#14)]  
  
 [Torna all'inizio](#Top)  
  
<a name="SupportedNamedBlocks"></a>   
## Blocchi denominati supportati  
 In .NET Framework sono disponibili i blocchi denominati elencati nella tabella riportata di seguito.  Il set di blocchi denominati supportati è basato su Unicode 4.0 e Perl 5.6.  
  
|Intervallo di punti di codice|Nome del blocco|  
|-----------------------------------|---------------------|  
|0000 \- 007F|`IsBasicLatin`|  
|0080 \- 00FF|`IsLatin-1Supplement`|  
|0100 \- 017F|`IsLatinExtended-A`|  
|0180 \- 024F|`IsLatinExtended-B`|  
|0250 \- 02AF|`IsIPAExtensions`|  
|02B0 \- 02FF|`IsSpacingModifierLetters`|  
|0300 \- 036F|`IsCombiningDiacriticalMarks`|  
|0370 \- 03FF|`IsGreek`<br /><br /> \-oppure\-<br /><br /> `IsGreekandCoptic`|  
|0400 \- 04FF|`IsCyrillic`|  
|0500 \- 052F|`IsCyrillicSupplement`|  
|0530 \- 058F|`IsArmenian`|  
|0590 \- 05FF|`IsHebrew`|  
|0600 \- 06FF|`IsArabic`|  
|0700 \- 074F|`IsSyriac`|  
|0780 \- 07BF|`IsThaana`|  
|0900 \- 097F|`IsDevanagari`|  
|0980 \- 09FF|`IsBengali`|  
|0A00 \- 0A7F|`IsGurmukhi`|  
|0A80 \- 0AFF|`IsGujarati`|  
|0B00 \- 0B7F|`IsOriya`|  
|0B80 \- 0BFF|`IsTamil`|  
|0C00 \- 0C7F|`IsTelugu`|  
|0C80 \- 0CFF|`IsKannada`|  
|0D00 \- 0D7F|`IsMalayalam`|  
|0D80 \- 0DFF|`IsSinhala`|  
|0E00 \- 0E7F|`IsThai`|  
|0E80 \- 0EFF|`IsLao`|  
|0F00 \- 0FFF|`IsTibetan`|  
|1000 \- 109F|`IsMyanmar`|  
|10A0 \- 10FF|`IsGeorgian`|  
|1100 \- 11FF|`IsHangulJamo`|  
|1200 \- 137F|`IsEthiopic`|  
|13A0 \- 13FF|`IsCherokee`|  
|1400 \- 167F|`IsUnifiedCanadianAboriginalSyllabics`|  
|1680 \- 169F|`IsOgham`|  
|16A0 \- 16FF|`IsRunic`|  
|1700 \- 171F|`IsTagalog`|  
|1720 \- 173F|`IsHanunoo`|  
|1740 \- 175F|`IsBuhid`|  
|1760 \- 177F|`IsTagbanwa`|  
|1780 \- 17FF|`IsKhmer`|  
|1800 \- 18AF|`IsMongolian`|  
|1900 \- 194F|`IsLimbu`|  
|1950 \- 197F|`IsTaiLe`|  
|19E0 \- 19FF|`IsKhmerSymbols`|  
|1D00 \- 1D7F|`IsPhoneticExtensions`|  
|1E00 \- 1EFF|`IsLatinExtendedAdditional`|  
|1F00 \- 1FFF|`IsGreekExtended`|  
|2000 \- 206F|`IsGeneralPunctuation`|  
|2070 \- 209F|`IsSuperscriptsandSubscripts`|  
|20A0 \- 20CF|`IsCurrencySymbols`|  
|20D0 \- 20FF|`IsCombiningDiacriticalMarksforSymbols`<br /><br /> \-oppure\-<br /><br /> `IsCombiningMarksforSymbols`|  
|2100 \- 214F|`IsLetterlikeSymbols`|  
|2150 \- 218F|`IsNumberForms`|  
|2190 \- 21FF|`IsArrows`|  
|2200 \- 22FF|`IsMathematicalOperators`|  
|2300 \- 23FF|`IsMiscellaneousTechnical`|  
|2400 \- 243F|`IsControlPictures`|  
|2440 \- 245F|`IsOpticalCharacterRecognition`|  
|2460 \- 24FF|`IsEnclosedAlphanumerics`|  
|2500 \- 257F|`IsBoxDrawing`|  
|2580 \- 259F|`IsBlockElements`|  
|25A0 \- 25FF|`IsGeometricShapes`|  
|2600 \- 26FF|`IsMiscellaneousSymbols`|  
|2700 \- 27BF|`IsDingbats`|  
|27C0 \- 27EF|`IsMiscellaneousMathematicalSymbols-A`|  
|27F0 \- 27FF|`IsSupplementalArrows-A`|  
|2800 \- 28FF|`IsBraillePatterns`|  
|2900 \- 297F|`IsSupplementalArrows-B`|  
|2980 \- 29FF|`IsMiscellaneousMathematicalSymbols-B`|  
|2A00 \- 2AFF|`IsSupplementalMathematicalOperators`|  
|2B00 \- 2BFF|`IsMiscellaneousSymbolsandArrows`|  
|2E80 \- 2EFF|`IsCJKRadicalsSupplement`|  
|2F00 \- 2FDF|`IsKangxiRadicals`|  
|2FF0 \- 2FFF|`IsIdeographicDescriptionCharacters`|  
|3000 \- 303F|`IsCJKSymbolsandPunctuation`|  
|3040 \- 309F|`IsHiragana`|  
|30A0 \- 30FF|`IsKatakana`|  
|3100 \- 312F|`IsBopomofo`|  
|3130 \- 318F|`IsHangulCompatibilityJamo`|  
|3190 \- 319F|`IsKanbun`|  
|31A0 \- 31BF|`IsBopomofoExtended`|  
|31F0 \- 31FF|`IsKatakanaPhoneticExtensions`|  
|3200 \- 32FF|`IsEnclosedCJKLettersandMonths`|  
|3300 \- 33FF|`IsCJKCompatibility`|  
|3400 \- 4DBF|`IsCJKUnifiedIdeographsExtensionA`|  
|4DC0 \- 4DFF|`IsYijingHexagramSymbols`|  
|4E00 \- 9FFF|`IsCJKUnifiedIdeographs`|  
|A000 \- A48F|`IsYiSyllables`|  
|A490 \- A4CF|`IsYiRadicals`|  
|AC00 \- D7AF|`IsHangulSyllables`|  
|D800 \- DB7F|`IsHighSurrogates`|  
|DB80 \- DBFF|`IsHighPrivateUseSurrogates`|  
|DC00 \- DFFF|`IsLowSurrogates`|  
|E000 \- F8FF|`IsPrivateUse` o `IsPrivateUseArea`|  
|F900 \- FAFF|`IsCJKCompatibilityIdeographs`|  
|FB00 \- FB4F|`IsAlphabeticPresentationForms`|  
|FB50 \- FDFF|`IsArabicPresentationForms-A`|  
|FE00 \- FE0F|`IsVariationSelectors`|  
|FE20 \- FE2F|`IsCombiningHalfMarks`|  
|FE30 \- FE4F|`IsCJKCompatibilityForms`|  
|FE50 \- FE6F|`IsSmallFormVariants`|  
|FE70 \- FEFF|`IsArabicPresentationForms-B`|  
|FF00 \- FFEF|`IsHalfwidthandFullwidthForms`|  
|FFF0 \- FFFF|`IsSpecials`|  
  
 [Torna all'inizio](#Top)  
  
<a name="CharacterClassSubtraction"></a>   
## Sottrazione di classi di caratteri: \[base\_group \- excluded\_group\] \[\]  
 Una classe di caratteri definisce un set di caratteri.  La sottrazione di classi di caratteri produce un set di caratteri che è il risultato dell'esclusione dei caratteri di una classe di caratteri da un'altra classe di caratteri.  
  
 Un'espressione di sottrazione di classi di caratteri ha il formato seguente:  
  
 `[` *base\_group* `-[` *excluded\_group* `]]`  
  
 Le parentesi quadre \(`[]`\) e il trattino \(`-`\) sono obbligatori.  *base\_group*è un [gruppo di caratteri positivi](#PositiveGroup) o un [gruppo di caratteri negativi](#NegativeGroup).  Il componente *excluded\_group* è un altro gruppo di caratteri positivi o negativi o un'altra espressione di sottrazione di classi di caratteri, \(ovvero è possibile annidare espressioni di sottrazione di classi di caratteri\).  
  
 Si supponga ad esempio di disporre di un gruppo di base costituito dall'intervallo di caratteri compresi tra "a" e "z".  Per definire il set di caratteri costituito dal gruppo di base con l'esclusione del carattere "m", usare `[a-z-[m]]`.  Per definire il set di caratteri costituito dal gruppo di base con l'esclusione del set di caratteri "d", "j" e "p", usare `[a-z-[djp]]`.  Per definire il set di caratteri costituito dal gruppo di base con l'esclusione dell'intervallo di caratteri compresi tra "m" e "p", usare `[a-z-[m-p]]`.  
  
 Si consideri l'espressione di sottrazione di classi di caratteri annidata `[a-z-[d-w-[m-o]]]`.  L'espressione viene valutata partendo dall'intervallo di caratteri più interno verso quello più esterno.  Innanzitutto, l'intervallo di caratteri compresi tra "m" e "o" viene sottratto dall'intervallo di caratteri compresi tra "d" e "w", producendo il set di caratteri compresi tra "d" e "l" e tra "p" e "w".  Tale set viene quindi sottratto dall'intervallo di caratteri compreso tra "a" e "z", producendo il set di caratteri `[abcmnoxyz]`.  
  
 È possibile usare qualsiasi classe di caratteri con sottrazione di classi di caratteri.  Per definire il set di caratteri costituito da tutti i caratteri Unicode compresi tra \\u0000 e \\uFFFF eccetto gli spazi vuoti \(`\s`\), i caratteri nella categoria generale punteggiatura \(`\p{P}`\), i caratteri nel blocco denominato `IsGreek` \(`\p{IsGreek}`\) e il carattere di controllo Unicode NEXT LINE \(\\x85\), usare `[\u0000-\uFFFF-[\s\p{P}\p{IsGreek}\x85]]`.  
  
 Scegliere le classi di caratteri per un'espressione di sottrazione di classi di caratteri che produrrà risultati utili.  Evitare espressioni che producono set di caratteri vuoti, che non hanno corrispondenze o che equivalgono al gruppo di base originale.  Ad esempio, il set vuoto è il risultato dell'espressione `[\p{IsBasicLatin}-[\x00-\x7F]]`, che sottrae tutti i caratteri compresi nell'intervallo di caratteri `IsBasicLatin` dalla categoria generale `IsBasicLatin`.  Analogamente, il gruppo di base originale è il risultato dell'espressione `[a-z-[0-9]]`.  Questo è dovuto al fatto che il gruppo di base, ovvero l'intervallo dei caratteri compresi tra le lettere "a" e "z", non contiene alcun carattere del gruppo escluso, ovvero dell'intervallo dei caratteri compresi tra le cifre decimali "0" e "9".  
  
 Nell'esempio seguente viene definita un'espressione regolare, `^[0-9-[2468]]+$`, che corrisponde a zero e a cifre dispari in una stringa di input.  L'espressione regolare viene interpretata come illustrato nella tabella seguente.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|^|Inizia la corrispondenza all'inizio della stringa di input.|  
|`[0-9-[2468]]+`|Corrisponde a una o più occorrenze di qualsiasi carattere da 0 a 9 ad eccezione di 2, 4, 6 e 8.  In altre parole, corrisponde a una o più occorrenze di zero o di una cifra dispari.|  
|$|Termina la ricerca della corrispondenza alla fine della stringa di input.|  
  
 [!code-csharp[Conceptual.RegEx.Language.CharacterClasses#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/classsubtraction1.cs#15)]
 [!code-vb[Conceptual.RegEx.Language.CharacterClasses#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/classsubtraction1.vb#15)]  
  
## Vedere anche  
 <xref:System.Char.GetUnicodeCategory%2A>   
 [Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)   
 [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md)