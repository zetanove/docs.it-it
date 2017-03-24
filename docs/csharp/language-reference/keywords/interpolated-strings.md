---
title: "Stringhe interpolate (Riferimenti di C# e Visual Basic) | Microsoft Docs"
ms.date: "2017-02-03"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
ms.assetid: 324f267e-1c61-431a-97ed-852c1530742d
caps.latest.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 9
---
# Stringhe interpolate (Riferimenti di C# e Visual Basic)
Vengono usate per la costruzione di stringhe.  Un'espressione di stringa interpolata è simile a una stringa di modello che contiene espressioni.  Crea una stringa sostituendo le espressioni contenute con le rappresentazioni ToString dei risultati delle espressioni.  In relazione agli argomenti, è più facile comprendere una stringa interpolata che la [Formattazione composita](../Topic/Composite%20Formatting.md).  Ecco un esempio di stringa interpolata:  
  
```c#  
Console.WriteLine($"Name = {name}, hours = {hours:hh}")  
```  
  
 La struttura di una stringa interpolata è la seguente:  
  
```  
$ " <text> { <interpolation-expression> <optional-comma-field-width> <optional-colon-format> } <text> ... } "  
```  
  
 È possibile usare una stringa interpolata ovunque sia possibile usare un valore letterale stringa.  Durante l'esecuzione del programma il codice viene eseguito con il valore letterale stringa interpolato e il codice calcola un nuovo valore stringa letterale valutando le espressioni di interpolazione.  Questo calcolo viene effettuato ogni volta che si esegue codice con la stringa interpolata.  
  
 Per includere una parentesi graffa \("{" o "}"\) in una stringa interpolata, digitarne due, ovvero "{{" o "}}".  Per altri dettagli, vedere la sezione Conversioni implicite.  
  
## Conversioni implicite  
 Da una stringa interpolata vengono effettuate conversioni di tipo implicito:  
  
```c#  
var s = $"hello, {name}" System.IFormattable s = $"Hello, {name}" System.FormattableString s = $"Hello, {name}"  
  
```  
  
 Nel primo esempio viene prodotto un valore `string` in cui sono stati calcolati tutti i valori di interpolazione delle stringhe.  Si tratta del risultato finale ed è di tipo stringa.  Tutte le occorrenze delle parentesi graffe doppie \("{{" e "}}"\) vengono convertite in parentesi graffe singole.  
  
 Nel secondo esempio viene prodotta una variabile <xref:System.IFormattable> che consente di convertire la stringa con contesto non associato ad alcun paese.  Questo risulta utile per ottenere formati numerici e di dati corretti in lingue diverse.  Tutte le occorrenze di parentesi graffe doppie \("{{" e "}}"\) rimangono tali finché la stringa non viene formattata con ToString.  Tutte le espressioni di interpolazione contenute vengono convertite in {0}, \\{1\\} e così via.  
  
```c#  
s.ToString(null, System.Globalization.CultureInfo.InvariantCulture);  
```  
  
 Nel terzo esempio viene prodotto un oggetto <xref:System.FormattableString>, che consente di esaminare gli oggetti risultanti dai calcoli di interpolazione.  Grazie all'esame degli oggetti e del modo in cui viene eseguito il rendering di tali oggetti come stringhe, è ad esempio possibile attuare misure di protezione contro attacchi di tipo injection durante l'esecuzione di una query.  Con <xref:System.FormattableString> sono disponibili utili operazioni per produrre i risultati in formato stringa di InvariantCulture e CurrentCulture.  Tutte le occorrenze delle parentesi graffe doppie \("{{" e "}}"\) rimangono invariate finché non si applica la formattazione.  Tutte le espressioni di interpolazione contenute vengono convertite in {0}, \\{1\\} e così via.  
  
## Esempi  
  
```c#  
$"Name = {name}, hours = {hours:hh}" var s = $"hello, {name}" System.IFormattable s = $"Hello, {name}" System.FormattableString s = $"Hello, {name}" $"{person.Name, 20} is {person.Age:D3} year {(p.Age == 1 ? "" : "s")} old."  
  
```  
  
 Non è necessario racchiudere tra virgolette i caratteri di citazione all'interno di espressioni di interpolazione perché le espressioni di stringa interpolata iniziano con $ e il compilatore analizza le espressioni di interpolazione contenute come testo bilanciato finché non trova una virgola, un punto e virgola o una parentesi graffa di chiusura.  Per gli stessi motivi nell'ultimo esempio vengono usate le parentesi per consentire l'uso dell'espressione condizionale \(`p.Age == 1 ? "" : "s"`\) all'interno dell'espressione di interpolazione senza i due punti che indicano l'inizio di una specifica di formato.  All'esterno dell'espressione di interpolazione contenuta, ma in ogni caso all'interno dell'espressione di stringa interpolata, è necessario aggiungere un carattere di escape per le virgolette.  
  
## Sintassi  
  
```  
expression: interpolated-string-expression interpolated-string-expression: interpolated-string-start interpolations interpolated-string-end interpolations: single-interpolation single-interpolation interpolated-string-mid interpolations single-interpolation: interpolation-start interpolation-start : regular-string-literal interpolation-start: expression expression , expression  
  
```  
  
## Specifiche del linguaggio  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
 Per altre informazioni, vedere [Visual Basic Language Reference](../../../visual-basic/language-reference/index.md).  
  
## Vedere anche  
 <xref:System.IFormattable?displayProperty=fullName>   
 <xref:System.FormattableString?displayProperty=fullName>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Visual Basic Language Reference](../../../visual-basic/language-reference/index.md)   
 [Visual Basic Programming Guide](../../../visual-basic/programming-guide/index.md)