---
title: Stringhe interpolate (C#) | Microsoft Docs
ms.date: 2017-02-03
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 324f267e-1c61-431a-97ed-852c1530742d
caps.latest.revision: 9
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: be7974018ce3195dc7344192d647fe64fb2ebcc4
ms.openlocfilehash: ee9d0f9803c6de056644587578792568ab25b4da
ms.contentlocale: it-it
ms.lasthandoff: 05/14/2017

---
# <a name="interpolated-strings-c-reference"></a>Stringhe interpolate (Riferimento per C#)

Vengono usate per la costruzione di stringhe.  Una stringa interpolata è simile a una stringa di modello che contiene *espressioni interpolate*.  Una stringa interpolata restituisce una stringa che sostituisce le espressioni interpolate in essa contenute con le rappresentazioni di stringa.  

Gli argomenti di una stringa interpolata sono più facili da comprendere rispetto a una [stringa di formato composito](../../../standard/base-types/composite-formatting.md#composite-format-string).  Ad esempio, la stringa interpolata  
  
```csharp  
Console.WriteLine($"Name = {name}, hours = {hours:hh}"); 
```  
contiene due espressioni interpolate, '{name}' e '{hours: hh}'. La stringa di formato composito equivalente è:

```csharp
Console.WriteLine("Name = {0}, hours = {1:hh}", name, hours);  
```  

La struttura di una stringa interpolata è:  
  
```  
$"<text> {<interpolated-expression> [,<field-width>] [<:format-string>] } <text> ..."  
```  

dove: 

- *field-width* è un intero con segno che indica il numero di caratteri nel campo. Se è positivo, il campo viene allineato a destra; se è negativo, viene allineato a sinistra. 

- *format-string* è una stringa di formato appropriata per il tipo di oggetto formattato. Ad esempio, per un valore @System.DateTime, potrebbe essere una stringa di formato data e ora standard come "D" o "d".

 È possibile usare una stringa interpolata ovunque sia possibile usare un valore letterale stringa.  La stringa interpolata viene valutata ogni volta che si esegue codice con la stringa interpolata. Ciò consente di separare la definizione e la valutazione di una stringa interpolata.  
  
 Per includere una parentesi graffa ("{" o "}") in una stringa interpolata, digitarne due, ovvero "{{" o "}}".  Per altri dettagli, vedere la sezione Conversioni implicite.  

Se la stringa interpolata contiene altri caratteri con un significato speciale in una stringa interpolata, ad esempio virgolette doppie ("), due punti (:) o virgola (,), è necessario specificare il carattere di escape se si presentano nel testo letterale, oppure inserirli in un'espressione racchiusa tra parentesi se sono elementi del linguaggio inclusi in un'espressione interpolata. Nell'esempio seguente viene specificato il carattere di escape delle virgolette per includerle nella stringa di risultato e si usano le parentesi per delimitare l'espressione `(age == 1 ? "" : "s")` in modo che i due punti non vengano interpretati come l'inizio di una stringa di formato.

[!code-cs[interpolated-strings4](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings4.cs#1)]  

## <a name="implicit-conversions"></a>Conversioni implicite  

Da una stringa interpolata vengono effettuate tre conversioni di tipo implicito:  

1. Conversione di una stringa interpolata in una @System.String. L'esempio seguente restituisce una stringa in cui le espressioni di stringa interpolata sono state sostituite con le rappresentazioni di stringa. Ad esempio:

   [!code-cs[interpolated-strings1](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings1.cs#1)]  

   Questo è il risultato finale di un'interpretazione della stringa. Tutte le occorrenze delle parentesi graffe doppie ("{{" e "}}") vengono convertite in parentesi graffe singole. 

2. Conversione di una stringa interpolata in una variabile <xref:System.IFormattable> che consente di creare più stringhe risultato con contenuto specifico delle impostazioni cultura da una singola istanza di <xref:System.IFormattable>. Ciò è utile per includere elementi quali i formati numerici e di data corretti per singole impostazioni cultura.  Tutte le occorrenze di parentesi graffe doppie ("{{" e "}}") rimangono tali finché la stringa non viene formattata in modo implicito o esplicito chiamando il metodo @System.Object.ToString.  Tutte le espressioni di interpolazione contenute vengono convertite in {0}, \{1\} e così via.  

   Nell'esempio seguente viene usata la reflection per visualizzare i membri, nonché i valori di campi e le proprietà di una variabile <xref:System.IFormattable> creata da una stringa interpolata. Viene anche passata la variabile <xref:System.IFormattable> al metodo @System.Console (System. String).

   [!code-cs[interpolated-strings2](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings2.cs#1)]  

   Si noti che la stringa interpolata può essere controllata solo tramite reflection. Se viene passata al metodo di formattazione delle stringhe, ad esempio @System.Console.WriteLine(System. String), gli elementi di formato vengono risolti e viene restituita la stringa di risultato. 

3. Conversione di una stringa interpolata in una variabile <xref:System.FormattableString> che rappresenta una stringa di formato composito. Grazie all'esame della stringa di formato composito e del modo in cui viene eseguito il rendering come stringa di risultato, è ad esempio possibile attuare misure di protezione contro attacchi di tipo injection durante la creazione di una query.  <xref:System.FormattableString> include anche overload <xref:System.FormattableString.ToString> che consentono di generare stringhe di risultato per @System.Globalization.InvariantCulture e @System.Globalization.CurrentCulture.  Tutte le occorrenze delle parentesi graffe doppie ("{{" e "}}") rimangono invariate finché non si applica la formattazione.  Tutte le espressioni di interpolazione contenute vengono convertite in {0}, \{1\} e così via.  

   [!code-cs[interpolated-strings3](../../../../samples/snippets/csharp/language-reference/keywords/interpolated-strings3.cs#1)]  

## <a name="language-specification"></a>Specifiche del linguaggio  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IFormattable?displayProperty=fullName>   
 <xref:System.FormattableString?displayProperty=fullName>   
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)

