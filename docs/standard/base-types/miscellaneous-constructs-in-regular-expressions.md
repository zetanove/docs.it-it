---
title: "Costrutti vari nelle espressioni regolari | Microsoft Docs"
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
  - "espressioni regolari di .NET Framework, costrutti vari"
  - "costrutti, varie"
  - "espressioni regolari, costrutti vari"
ms.assetid: 7d10d11f-680f-4721-b047-fb136316b4cd
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Costrutti vari nelle espressioni regolari
Le espressioni regolari in .NET Framework includono tre costrutti di linguaggio misti.  Consente di abilitare o disabilitare opzioni di corrispondenza specifiche all'interno di un modello di espressione regolare.  I due restanti consentono di includere commenti in un'espressione regolare.  
  
## Opzioni Inline  
 È possibile impostare o disabilitare opzioni del criterio di ricerca specifiche per parte di un'espressione regolare tramite la sintassi  
  
```  
(?imnsx-imnsx)  
```  
  
 Si elencano le opzioni che si desidera attivare dopo il punto interrogativo e le opzioni che si desidera disabilitare dopo il segno di sottrazione.  Nella tabella seguente viene descritta ciascuna opzione.  Per ulteriori informazioni su ogni opzione, vedere [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|`i`|Corrispondenza che non fa distinzione tra maiuscole e minuscole.|  
|`m`|Modalità multiriga.|  
|`n`|Solo acquisizioni esplicite. \(Le parentesi non funzionano come gruppi di acquisizione.\)|  
|`s`|Modalità a riga singola.|  
|`x`|Ignora spazi vuoti non validi e consenti i commenti in modalità X.|  
  
 Qualsiasi modifica nelle opzioni dell'espressione regolare definita dal costrutto `(?imnsx-imnsx)` rimane attiva fino alla fine del gruppo di inclusione.  
  
> [!NOTE]
>  Il costrutto di raggruppamento `(?imnsx-imnsx:`*subexpression*`)` fornisce la funzionalità identica per una sottoespressione.  Per ulteriori informazioni, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
 Nell'esempio seguente vengono utilizzate le opzioni `i`, `n` e `x` per attivare la mancata distinzione tra maiuscole e minuscole e le acquisizioni esplicite, e per ignorare lo spazio vuoto nel criterio dell'espressione regolare all'interno di un'espressione regolare.  
  
 [!code-csharp[RegularExpressions.Language.Miscellaneous#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.miscellaneous/cs/miscellaneous1.cs#1)]
 [!code-vb[RegularExpressions.Language.Miscellaneous#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.miscellaneous/vb/miscellaneous1.vb#1)]  
  
 Nell'esempio vengono definite due espressioni regolari.  Il primo, `\b(D\w+)\s(d\w+)\b`, corrisponde a due parole consecutive che iniziano con una "D" maiuscola e una "d" minuscola.  La seconda espressione regolare, `\b(D\w+)(?ixn) \s (d\w+) \b`, utilizza opzioni inline per modificare questo modello, come descritto nella tabella seguente.  Un confronto dei risultati conferma l'effetto del costrutto `(?ixn)`.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Iniziare dal confine di una parola.|  
|`(D\w+)`|Corrisponde a una "D" maiuscola seguita da uno o più caratteri alfanumerici.  Si tratta del primo gruppo di acquisizione.|  
|`(?ixn)`|Da questo punto in avanti, effettuare confronti senza distinzione tra maiuscole e minuscole, fare solo acquisizioni esplicite e ignorare gli spazi vuoti nel criterio di espressione regolare.|  
|`\s`|Trovare la corrispondenza di uno spazio vuoto.|  
|`(d\w+)`|Corrisponde a una "d" maiuscola o minuscola seguita da uno o più caratteri alfanumerici.  Questo gruppo non viene acquisito perché è stata attivata l'opzione `n` \(acquisizione esplicita\).|  
|`\b`|Trovare la corrispondenza di un confine di parola.|  
  
## Commento Inline  
 Il costrutto `(?#` *comment*`)` consente di includere un commento inline in un'espressione regolare.  Il motore delle espressioni regolari non utilizza parti del commento nella corrispondenza tra modelli, anche se il commento è incluso nella stringa restituita dal metodo <xref:System.Text.RegularExpressions.Regex.ToString%2A?displayProperty=fullName>.  Il commento termina in corrispondenza della prima parentesi chiusa.  
  
 Nell'esempio riportato di seguito viene ripetuto il primo modello di espressione regolare dell'esempio fornito nella sezione precedente.  Aggiunge due commenti inline all'espressione regolare per indicare se il confronto prevede la distinzione tra maiuscole e minuscole.  Il modello dell'espressione regolare, `\b((?# case-sensitive comparison)D\w+)\s((?#case-insensitive comparison)d\w+)\b`, viene definito nel seguente modo.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Iniziare dal confine di una parola.|  
|`(?# case-sensitive comparison)`|Commento.  Non influisce sul comportamento dei criteri di ricerca.|  
|`(D\w+)`|Corrisponde a una "D" maiuscola seguita da uno o più caratteri alfanumerici.  Primo gruppo di acquisizione.|  
|`\s`|Trovare la corrispondenza di uno spazio vuoto.|  
|`(?ixn)`|Da questo punto in avanti, effettuare confronti senza distinzione tra maiuscole e minuscole, fare solo acquisizioni esplicite e ignorare gli spazi vuoti nel criterio di espressione regolare.|  
|`(?#case-insensitive comparison)`|Commento.  Non influisce sul comportamento dei criteri di ricerca.|  
|`(d\w+)`|Corrisponde a una "d" maiuscola o minuscola seguita da uno o più caratteri alfanumerici.  Si tratta del secondo gruppo di acquisizione.|  
|`\b`|Trovare la corrispondenza di un confine di parola.|  
  
 [!code-csharp[RegularExpressions.Language.Miscellaneous#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.miscellaneous/cs/miscellaneous2.cs#2)]
 [!code-vb[RegularExpressions.Language.Miscellaneous#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.miscellaneous/vb/miscellaneous2.vb#2)]  
  
## Commento a fine riga  
 Un simbolo di cancelletto \(`#`\) contrassegna un commento in modalità x che inizia dal valore senza caratteri escape \# alla fine del criterio di espressione regolare e continua fino alla fine della riga.  Per utilizzare questo costrutto, è necessario attivare l'opzione `x` \(tramite opzioni inline\) o fornire il valore <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> al parametro `option` in caso di creazione di un'istanza dell'oggetto <xref:System.Text.RegularExpressions.Regex> o di chiamata a un metodo statico di <xref:System.Text.RegularExpressions.Regex>.  
  
 Nell'esempio seguente viene illustrato il costrutto del commento di fine riga.  Determina se una stringa è una stringa di formato composto che include almeno un elemento di formato.  Nella tabella riportata di seguito vengono descritti i costrutti nel modello dell'espressione regolare:  
  
 `\{\d+(,-*\d+)*(\:\w{1,4}?)*\}(?x) # Looks for a composite format item.`  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\{`|Corrisponde a una parentesi graffa aperta.|  
|`\d+`|Corrisponde a una o più cifre decimali.|  
|`(,-*\d+)*`|Corrisponde a zero o a un'occorrenza di una virgola, seguita da un segno di sottrazione facoltativo, seguito da una o più cifre decimali.|  
|`(\:\w{1,4}?)*`|Corrisponde a zero o a un'occorrenza del segno dei due punti, seguito da 1\-4 spazi vuoti \(ma comunque il minor numero di caratteri possibile\).|  
|`(?#case insensitive comparison)`|Commento inline.  Non ha alcun effetto sul comportamento dei criteri di ricerca.|  
|`\}`|Corrisponde a una parentesi graffa di chiusura.|  
|`(?x)`|Attiva l'opzione per ignorare gli spazi vuoti nei motivi per riconoscere il commento a fine riga.|  
|`# Looks for a composite format item.`|Un commento a fine riga.|  
  
 [!code-csharp[RegularExpressions.Language.Miscellaneous#3](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.miscellaneous/cs/miscellaneous3.cs#3)]
 [!code-vb[RegularExpressions.Language.Miscellaneous#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.miscellaneous/vb/miscellaneous3.vb#3)]  
  
 Anziché fornire il costrutto `(?x)` nell'espressione regolare, sarebbe stato possibile riconoscere il commento chiamando il metodo <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=fullName> e passandogli il valore di enumerazione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>.  
  
## Vedere anche  
 [Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)