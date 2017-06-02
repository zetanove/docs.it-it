---
title: "Modello a oggetti delle espressioni regolari | Microsoft Docs"
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
  - "espressioni regolari di .NET Framework, backreference"
  - "espressioni regolari di .NET Framework, classi"
  - "backreference"
  - "Capture (classe)"
  - "CaptureCollection (classe)"
  - "caratteri [.NET Framework], backreference"
  - "caratteri [.NET Framework], metacaratteri"
  - "caratteri [.NET Framework], espressioni regolari"
  - "classi [.NET Framework], espressione regolare"
  - "Group (classe)"
  - "GroupCollection (classe)"
  - "Match (classe)"
  - "MatchCollection (classe)"
  - "metacaratteri, backreference"
  - "metacaratteri, classi di espressioni regolari"
  - "analisi di testo con espressioni regolari, backreference"
  - "analisi di testo con espressioni regolari, classi"
  - "corrispondenza al modello con espressioni regolari, backreference"
  - "corrispondenza al modello con espressioni regolari, classi"
  - "Regex (classe)"
  - "espressioni regolari [.NET Framework]"
  - "espressioni regolari [.NET Framework], backreference"
  - "espressioni regolari [.NET Framework], classi"
  - "ripetizione di gruppi di caratteri"
  - "ricerca con espressioni regolari, backreference"
  - "ricerca con espressioni regolari, classi"
  - "stringhe [.NET Framework], espressioni regolari"
  - "sottostringhe"
ms.assetid: 49a21470-64ca-4b5a-a889-8e24e3c0af7e
caps.latest.revision: 26
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 26
---
# Modello a oggetti delle espressioni regolari
<a name="introduction"></a> In questo argomento è illustrato il modello a oggetti usato insieme alle espressioni regolari di .NET Framework. Include le sezioni seguenti:  
  
-   [Motore delle espressioni regolari](#Engine)  
  
-   [Oggetti MatchCollection e Match](#Match_and_MCollection)  
  
-   [Raccolta Group](#GroupCollection)  
  
-   [Gruppo Captured](#the_captured_group)  
  
-   [Raccolta Capture](#CaptureCollection)  
  
-   [Singola acquisizione](#the_individual_capture)  
  
<a name="Engine"></a>   
## Motore delle espressioni regolari  
 Il motore delle espressioni regolari di .NET Framework è rappresentato dalla classe <xref:System.Text.RegularExpressions.Regex>. Il motore delle espressioni regolari è responsabile dell'analisi e della compilazione di un'espressione regolare e dell'esecuzione di operazioni che associano il criterio di espressione regolare a una stringa di input. Il motore è il componente centrale del modello a oggetti delle espressioni regolari di .NET Framework.  
  
 È possibile usare il motore delle espressioni regolari in uno dei due modi seguenti:  
  
-   Tramite la chiamata di metodi statici della classe <xref:System.Text.RegularExpressions.Regex>. I parametri del metodo includono la stringa di input e il criterio di espressione regolare. Il motore delle espressioni regolari memorizza nella cache le espressioni regolari usate nelle chiamate del metodo statico. Le chiamate ripetute a metodi di espressione regolare che usano la stessa espressione regolare offrono quindi prestazioni relativamente buone.  
  
-   Tramite la creazione di istanze di un oggetto <xref:System.Text.RegularExpressions.Regex>, mediante il passaggio di un'espressione regolare al costruttore di classe. In questo caso l'oggetto <xref:System.Text.RegularExpressions.Regex> è non modificabile \(sola lettura\) e rappresenta un motore delle espressioni regolari strettamente associato a una singola espressione regolare. Poiché le espressioni regolari usate dalle istanze di <xref:System.Text.RegularExpressions.Regex> non sono memorizzate nella cache, è consigliabile non creare più volte istanze di un oggetto <xref:System.Text.RegularExpressions.Regex> con la stessa espressione regolare.  
  
 È possibile chiamare i metodi della classe <xref:System.Text.RegularExpressions.Regex> per eseguire le operazioni seguenti:  
  
-   Determinare se una stringa corrisponde a un criterio di espressione regolare.  
  
-   Estrarre una singola corrispondenza o la prima corrispondenza.  
  
-   Estrarre tutte le corrispondenze.  
  
-   Sostituire una sottostringa con corrispondenza.  
  
-   Suddividere una singola stringa in una matrice di stringhe.  
  
 Queste operazioni sono descritte nelle sezioni seguenti.  
  
### Corrispondenza con un criterio di espressione regolare  
 Il metodo <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=fullName> restituisce `true` se la stringa corrisponde al modello. In caso contrario, `false`. Il metodo <xref:System.Text.RegularExpressions.Regex.IsMatch%2A> è usato spesso per convalidare l'input di stringa. Ad esempio, il codice seguente assicura che una stringa corrisponda a un numero di previdenza sociale negli Stati Uniti.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/validate1.cs#1)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/validate1.vb#1)]  
  
 Il criterio di ricerca di espressioni regolari `^\d{3}-\d{2}-\d{4}$` è interpretato nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`^`|Trova la corrispondenza con l'inizio della stringa di input.|  
|`\d{3}`|Trova la corrispondenza con tre cifre decimali.|  
|`-`|Trova la corrispondenza con un segno meno.|  
|`\d{2}`|Trova la corrispondenza con due cifre decimali.|  
|`-`|Trova la corrispondenza con un segno meno.|  
|`\d{4}`|Trova la corrispondenza con quattro cifre decimali.|  
|`$`|Trova la corrispondenza con la fine della stringa di input.|  
  
### Estrazione di una singola corrispondenza o della prima corrispondenza  
 Il metodo <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Text.RegularExpressions.Match> che include informazioni sulla prima sottostringa corrispondente a un criterio di espressione regolare. Se la proprietà `Match.Success` restituisce `true`, indicando che è stata rilevata una corrispondenza, sarà possibile ottenere informazioni sulle corrispondenze successive chiamando il metodo <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=fullName>. Le chiamate ai metodi possono continuare finché la proprietà `Match.Success` non restituisce `false`. Ad esempio, il codice seguente usa il metodo <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%29?displayProperty=fullName> per trovare la prima occorrenza di una parola duplicata in una stringa. Chiama quindi i metodi <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=fullName> per trovare eventuali occorrenze aggiuntive. L'esempio esamina la proprietà `Match.Success` dopo ogni chiamata al metodo, per determinare se la corrispondenza corrente è riuscita e se deve essere seguita da una chiamata al metodo <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=fullName>.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/match1.cs#2)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/match1.vb#2)]  
  
 Il criterio di espressione regolare `\b(\w+)\W+(\1)\b` è interpretato nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`(\w+)`|Trova la corrispondenza di uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.|  
|`\W+`|Trova la corrispondenza di uno o più caratteri non alfanumerici.|  
|`(\1)`|Trova la corrispondenza con la prima stringa acquisita. Equivale al secondo gruppo di acquisizione.|  
|`\b`|Termina la corrispondenza sul confine di parola.|  
  
### Estrazione di tutte le corrispondenze  
 Il metodo <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Text.RegularExpressions.MatchCollection> che include informazioni su tutte le corrispondenze rilevate dal motore delle espressioni regolari nella stringa di input. Ad esempio, è possibile riscrivere l'esempio precedente in modo da chiamare il metodo <xref:System.Text.RegularExpressions.Regex.Matches%2A> invece dei metodi <xref:System.Text.RegularExpressions.Regex.Match%2A> e <xref:System.Text.RegularExpressions.Match.NextMatch%2A>.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/matches1.cs#3)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/matches1.vb#3)]  
  
### Sostituzione di una sottostringa con corrispondenza  
 Il metodo <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=fullName> sostituisce ogni sottostringa corrispondente al criterio di espressione regolare con una stringa specificata o con un criterio di espressione regolare e restituisce l'intera stringa di input con le sostituzioni. Ad esempio, il codice riportato di seguito aggiunge il simbolo di valuta degli Stati Uniti prima di un numero decimale in una stringa.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/replace1.cs#4)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/replace1.vb#4)]  
  
 Il criterio di ricerca di espressioni regolari `\b\d+\.\d{2}\b` è interpretato nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`\d+`|Trova la corrispondenza con una o più cifre decimali.|  
|`\.`|Trova la corrispondenza con un punto.|  
|`\d{2}`|Trova la corrispondenza con due cifre decimali.|  
|`\b`|Termina la corrispondenza sul confine di parola.|  
  
 Il modello di sostituzione `$$$&` è interpretato nel modo illustrato nella tabella seguente.  
  
|Criterio|Stringa di sostituzione|  
|--------------|-----------------------------|  
|`$$`|Simbolo del dollaro \($\).|  
|`$&`|Intera stringa corrispondente.|  
  
### Suddivisione di una singola stringa in una matrice di stringhe  
 Il metodo <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=fullName> suddivide la stringa di input nelle posizioni definite da una corrispondenza di espressione regolare. Ad esempio, il codice seguente inserisce gli elementi di un elenco numerato in una matrice di stringhe.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/split1.cs#5)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/split1.vb#5)]  
  
 Il criterio di ricerca di espressioni regolari `\b\d{1,2}\.\s` è interpretato nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`\d{1,2}`|Trova la corrispondenza con una o due cifre decimali.|  
|`\.`|Trova la corrispondenza con un punto.|  
|`\s`|Trova la corrispondenza con uno spazio vuoto.|  
  
<a name="Match_and_MCollection"></a>   
## Oggetti MatchCollection e Match  
 I metodi Regex restituiscono due oggetti che fanno parte del modello a oggetti delle espressioni regolari: l'oggetto <xref:System.Text.RegularExpressions.MatchCollection> e l'oggetto <xref:System.Text.RegularExpressions.Match>.  
  
<a name="the_match_collection"></a>   
### Raccolta Match  
 Il metodo <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Text.RegularExpressions.MatchCollection> contenente gli oggetti <xref:System.Text.RegularExpressions.Match> che rappresentano tutte le corrispondenze rilevate dal motore delle espressioni regolari, in base all'ordine in cui si trovano nella stringa di input. Se non sono rilevate corrispondenze, il metodo restituisce un oggetto <xref:System.Text.RegularExpressions.MatchCollection> senza membri. La proprietà <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=fullName> permette di accedere a singoli membri della raccolta in base all'indice, da zero al valore della proprietà <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=fullName> meno uno.<xref:System.Text.RegularExpressions.MatchCollection.Item%2A> è l'indicizzatore della raccolta \(in C\#\) e la proprietà predefinita \(in Visual Basic\).  
  
 Per impostazione predefinita, la chiamata al metodo <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName> usa la valutazione lenta per il popolamento dell'oggetto <xref:System.Text.RegularExpressions.MatchCollection>. L'accesso alle proprietà che necessitano di una raccolta completamente popolata, ad esempio le proprietà <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=fullName> e <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=fullName>, potrebbe comportare gravi conseguenze per le prestazioni. È quindi consigliabile accedere alla raccolta usando l'oggetto <xref:System.Collections.IEnumerator> restituito dal metodo <xref:System.Text.RegularExpressions.MatchCollection.GetEnumerator%2A?displayProperty=fullName>. I singoli linguaggi forniscono i costrutti, ad esempio `For``Each` in Visual Basic e `foreach` in C\#, che eseguono il wrapping dell'interfaccia <xref:System.Collections.IEnumerator> della raccolta.  
  
 L'esempio seguente usa il metodo <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%29?displayProperty=fullName> per popolare un oggetto <xref:System.Text.RegularExpressions.MatchCollection> con tutte le corrispondenze rilevate in una stringa di input. L'esempio enumera la raccolta, copia le corrispondenze a una matrice di stringhe e registra le posizioni dei caratteri in una matrice di valori di tipo Integer.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/matchcollection1.cs#6)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/matchcollection1.vb#6)]  
  
<a name="the_match"></a>   
### Oggetto Match  
 La classe <xref:System.Text.RegularExpressions.Match> rappresenta il risultato della corrispondenza di una singola espressione regolare. È possibile accedere agli oggetti <xref:System.Text.RegularExpressions.Match> in due modi:  
  
-   Tramite il recupero dall'oggetto <xref:System.Text.RegularExpressions.MatchCollection> restituito dal metodo <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName>. Per recuperare i singoli oggetti <xref:System.Text.RegularExpressions.Match>, eseguire l'iterazione della raccolta usando il costrutto `foreach` \(in C\#\) o .`For Each`...`Next`.\(in Visual Basic\) oppure usare la proprietà <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=fullName> per recuperare un oggetto <xref:System.Text.RegularExpressions.Match> specifico in base all'indice o al nome. È anche possibile recuperare singoli oggetti <xref:System.Text.RegularExpressions.Match> dalla raccolta eseguendo l'iterazione della raccolta in base all'indice, da zero al numero di oggetti della raccolta meno uno. Questo metodo, tuttavia, non permette di avvalersi della valutazione lenta, poiché accede alla proprietà <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=fullName>.  
  
     L'esempio seguente recupera singoli oggetti <xref:System.Text.RegularExpressions.Match> da un oggetto <xref:System.Text.RegularExpressions.MatchCollection> eseguendo l'iterazione della raccolta tramite il costrutto `foreach` o `For Each`...`Next`. L'espressione regolare corrisponde semplicemente alla stringa "abc" nella stringa di input.  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/match2.cs#7)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/match2.vb#7)]  
  
-   Tramite la chiamata al metodo <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=fullName>, che restituisce un oggetto <xref:System.Text.RegularExpressions.Match> che rappresenta la prima corrispondenza in una stringa o in una parte di una stringa. È possibile stabilire se la corrispondenza è stata rilevata tramite il recupero del valore della proprietà `Match.Success`. Per recuperare gli oggetti <xref:System.Text.RegularExpressions.Match> che rappresentano corrispondenze successive, chiamare ripetutamente il metodo <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=fullName>, fino a quando la proprietà `Success` dell'oggetto <xref:System.Text.RegularExpressions.Match> restituito non sarà `false`.  
  
     L'esempio seguente usa i metodi <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%29?displayProperty=fullName> e <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=fullName> per la corrispondenza con la stringa "abc" nella stringa di input.  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/match3.cs#8)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/match3.vb#8)]  
  
 Due proprietà della classe <xref:System.Text.RegularExpressions.Match> restituiscono oggetti della raccolta:  
  
-   La proprietà <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Text.RegularExpressions.GroupCollection> che include informazioni sulle sottostringhe che corrispondono a gruppi di acquisizione nel criterio di espressione regolare.  
  
-   La proprietà `Match.Captures` restituisce un oggetto <xref:System.Text.RegularExpressions.CaptureCollection> di uso limitato. La raccolta non è popolata per un oggetto <xref:System.Text.RegularExpressions.Match> la cui proprietà `Success` è `false`. In caso contrario, contiene un singolo oggetto <xref:System.Text.RegularExpressions.Capture> che include le stesse informazioni dell'oggetto <xref:System.Text.RegularExpressions.Match>.  
  
 Per altre informazioni su questi oggetti, vedere le sezioni [Raccolta Group](#GroupCollection) e [Raccolta Capture](#CaptureCollection) più avanti in questo argomento.  
  
 Due proprietà aggiuntive della classe <xref:System.Text.RegularExpressions.Match> forniscono informazioni sulla corrispondenza. La proprietà `Match.Value` restituisce la sottostringa nella stringa di input corrispondente al criterio di espressione regolare. La proprietà `Match.Index` restituisce la posizione di inizio a base zero della stringa con corrispondenza nella stringa di input.  
  
 La classe <xref:System.Text.RegularExpressions.Match> include anche due metodi di corrispondenza del modello:  
  
-   Il metodo <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=fullName> trova la corrispondenza dopo la corrispondenza rappresentata dall'oggetto corrente <xref:System.Text.RegularExpressions.Match> e restituisce un oggetto <xref:System.Text.RegularExpressions.Match> che rappresenta quella corrispondenza.  
  
-   Il metodo <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=fullName> esegue un'operazione di sostituzione specificata nella stringa con corrispondenza e restituisce il risultato.  
  
 L'esempio seguente usa il metodo <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=fullName> per aggiungere un simbolo $ e uno spazio davanti a qualsiasi numero che include due cifre frazionarie.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/result1.cs#9)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/result1.vb#9)]  
  
 Il criterio di espressione regolare `\b\d+(,\d{3})*\.\d{2}\b` è definito nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`\d+`|Trova la corrispondenza con una o più cifre decimali.|  
|`(,\d{3})*`|Trova la corrispondenza con zero o più occorrenze di una virgola seguita da tre cifre decimali.|  
|`\.`|Trova la corrispondenza con il carattere del separatore decimale.|  
|`\d{2}`|Trova la corrispondenza con due cifre decimali.|  
|`\b`|Termina la corrispondenza sul confine di parola.|  
  
 Il modello di sostituzione `$$ $&` indica che la stringa con corrispondenza deve essere sostituita da un simbolo del dollaro \($\) \(modello `$$`\), uno spazio e il valore della corrispondenza \(modello `$&`\).  
  
 [Torna all'inizio](#introduction)  
  
<a name="GroupCollection"></a>   
## Raccolta Group  
 La proprietà <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Text.RegularExpressions.GroupCollection> che include gli oggetti <xref:System.Text.RegularExpressions.Group> che rappresentano i gruppi acquisiti in una singola corrispondenza. Il primo oggetto <xref:System.Text.RegularExpressions.Group> della raccolta \(in corrispondenza dell'indice 0\) rappresenta l'intera corrispondenza. Ogni oggetto successivo rappresenta i risultati di un singolo gruppo di acquisizione.  
  
 È possibile recuperare singoli oggetti <xref:System.Text.RegularExpressions.Group> nella raccolta usando la proprietà <xref:System.Text.RegularExpressions.GroupCollection.Item%2A?displayProperty=fullName>. I gruppi senza nome possono essere recuperati in base alla relativa posizione ordinale nella raccolta e i gruppi con nome possono essere recuperati in base al nome o alla posizione ordinale. Le acquisizioni senza nome compaiono per prime nella raccolta e sono indicizzate da sinistra a destra nell'ordine di visualizzazione nel criterio di espressione regolare. Le acquisizioni con nome sono indicizzate dopo le acquisizioni senza nome, da sinistra a destra nell'ordine di visualizzazione nel criterio di espressione regolare. Per determinare i gruppi numerati disponibili nella raccolta restituita per un metodo specifico di corrispondenza con l'espressione regolare, è possibile chiamare il metodo <xref:System.Text.RegularExpressions.Regex.GetGroupNumbers%2A?displayProperty=fullName> dell'istanza. Per determinare i gruppi con nome disponibili nella raccolta, è possibile chiamare il metodo <xref:System.Text.RegularExpressions.Regex.GetGroupNames%2A?displayProperty=fullName> dell'istanza. Entrambi i metodi sono particolarmente utili in routine di uso generale, che analizzano le corrispondenze rilevate da un'espressione regolare.  
  
 La proprietà <xref:System.Text.RegularExpressions.GroupCollection.Item%2A?displayProperty=fullName> è l'indicizzatore della raccolta in C\# e la proprietà predefinita dell'oggetto della raccolta in Visual Basic. È quindi possibile accedere ai singoli oggetti <xref:System.Text.RegularExpressions.Group> in base all'indice oppure in base al nome, nel caso dei gruppi con nome, come indicato di seguito:  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/groupsyntax1.cs#13)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/groupsyntax1.vb#13)]  
  
 L'esempio seguente definisce un'espressione regolare che usa costrutti di raggruppamento per acquisire il mese, il giorno e l'anno di una data.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/groupcollection1.cs#10)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/groupcollection1.vb#10)]  
  
 Il criterio di ricerca di espressioni regolari `\b(\w+)\s(\d{1,2}),\s(\d{4})\b` è definito nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`(\w+)`|Trova la corrispondenza di uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.|  
|`\s`|Trova la corrispondenza con uno spazio vuoto.|  
|`(\d{1,2})`|Trova la corrispondenza con una o due cifre decimali. Equivale al secondo gruppo di acquisizione.|  
|`,`|Trova la corrispondenza con una virgola.|  
|`\s`|Trova la corrispondenza con uno spazio vuoto.|  
|`(\d{4})`|Trova la corrispondenza con quattro cifre decimali. Equivale al terzo gruppo di acquisizione.|  
|`\b`|Termina la corrispondenza sul confine di parola.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="the_captured_group"></a>   
## Gruppo Captured  
 La classe <xref:System.Text.RegularExpressions.Group> rappresenta il risultato di un singolo gruppo di acquisizione. Gli oggetti di gruppo che rappresentano i gruppi di acquisizione definiti in un'espressione regolare sono restituiti dalla proprietà <xref:System.Text.RegularExpressions.GroupCollection.Item%2A> dell'oggetto <xref:System.Text.RegularExpressions.GroupCollection> restituito dalla proprietà <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=fullName>. La proprietà <xref:System.Text.RegularExpressions.GroupCollection.Item%2A> è l'indicizzatore \(in C\#\) e la proprietà predefinita \(in Visual Basic\) della classe <xref:System.Text.RegularExpressions.Group>. È anche possibile recuperare i singoli membri eseguendo l'iterazione della raccolta mediante il costrutto `foreach` o `For``Each`. Per un esempio, vedere la sezione precedente.  
  
 L'esempio seguente usa i costrutti di raggruppamento annidati per acquisire le sottostringhe nei gruppi. Il criterio di espressione regolare `(a(b))c` corrisponde alla stringa "abc". Assegna la sottostringa "ab" al primo gruppo di acquisizione e la sottostringa "b" al secondo gruppo di acquisizione.  
  
 [!code-csharp[RegularExpressions.Classes#6](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Classes/cs/Example.cs#6)]
 [!code-vb[RegularExpressions.Classes#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Classes/vb/Example.vb#6)]  
  
 L'esempio seguente usa costrutti di raggruppamento con nome per acquisire sottostringhe da una stringa che include dati nel formato "DATANAME:VALUE" e viene suddivisa in corrispondenza dei due punti \(:\) dall'espressione regolare.  
  
 [!code-csharp[RegularExpressions.Classes#8](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Classes/cs/Example.cs#8)]
 [!code-vb[RegularExpressions.Classes#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Classes/vb/Example.vb#8)]  
  
 Il criterio di ricerca di espressioni regolari `^(?<name>\w+):(?<value>\w+)` è definito nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`^`|Inizia la corrispondenza all'inizio della stringa di input.|  
|`(?<name>\w+)`|Trova la corrispondenza di uno o più caratteri alfanumerici. Il nome di questo gruppo di acquisizione è `name`.|  
|`:`|Trova la corrispondenza con i due punti.|  
|`(?<value>\w+)`|Trova la corrispondenza di uno o più caratteri alfanumerici. Il nome di questo gruppo di acquisizione è `value`.|  
  
 Le proprietà della classe <xref:System.Text.RegularExpressions.Group> forniscono informazioni sul gruppo acquisito. La proprietà `Group.Value` include la sottostringa acquisita, la proprietà`Group.Index` indica la posizione iniziale del gruppo acquisito nel testo di input, la proprietà `Group.Length` include la lunghezza del testo acquisito e la proprietà `Group.Success` indica se una sottostringa corrisponde al modello definito dal gruppo di acquisizione.  
  
 L'applicazione di quantificatori a un gruppo \(per altre informazioni, vedere [Quantificatori](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md)\) modificala relazione di un'acquisizione per ogni gruppo di acquisizione in due modi:  
  
-   Se il quantificatore `*` o `*?` \(che specifica zero o più corrispondenze\) è applicato a un gruppo, è possibile che per un gruppo di acquisizione non siano rilevate corrispondenze nella stringa di input. Se non è presente testo acquisito, le proprietà dell'oggetto <xref:System.Text.RegularExpressions.Group> sono impostate come mostrato nella tabella seguente.  
  
    |Proprietà del gruppo|Valore|  
    |--------------------------|------------|  
    |`Success`|`false`|  
    |`Value`|<xref:System.String.Empty?displayProperty=fullName>|  
    |`Length`|0|  
  
     Nell'esempio seguente viene illustrato questo concetto. Nel criterio di espressione regolare `aaa(bbb)*ccc` per il primo gruppo di acquisizione \(sottostringa "bbb"\) possono essere rilevate zero o più corrispondenze. Poiché la stringa di input "aaaccc" corrisponde al modello, per il gruppo di acquisizione non sono rilevate corrispondenze.  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/nocapture1.cs#11)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/nocapture1.vb#11)]  
  
-   I quantificatori possono corrispondere a più occorrenze di un modello definito da un gruppo di acquisizione. In questo caso, le proprietà `Value` e `Length` di un oggetto <xref:System.Text.RegularExpressions.Group> contengono informazioni sull'ultima sottostringa acquisita. Ad esempio, l'espressione regolare seguente corrisponde a una singola frase che termina con un punto. Usa due costrutti di raggruppamento: il primo acquisisce singole parole insieme a un carattere di spaziatura e il secondo acquisisce le singole parole. Come illustrato dall'output dell'esempio, anche se l'espressione regolare riesce ad acquisire un'intera frase, il secondo gruppo di acquisizione acquisisce solo l'ultima parola.  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/lastcapture1.cs#12)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/lastcapture1.vb#12)]  
  
 [Torna all'inizio](#introduction)  
  
<a name="CaptureCollection"></a>   
## Raccolta Capture  
 L'oggetto <xref:System.Text.RegularExpressions.Group> include informazioni solo sull'ultima acquisizione. L'intero set di acquisizioni eseguite da un gruppo di acquisizione è tuttavia ancora disponibile tramite l'oggetto <xref:System.Text.RegularExpressions.CaptureCollection> restituito dalla proprietà <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=fullName>. Ogni membro della raccolta è un oggetto <xref:System.Text.RegularExpressions.Capture> che rappresenta un'acquisizione eseguita da quel gruppo di acquisizione, in base all'ordine di acquisizione e quindi in base all'ordine in cui sono state rilevate corrispondenze per le stringhe acquisite da sinistra a destra nella stringa di input. È possibile recuperare singoli oggetti <xref:System.Text.RegularExpressions.Capture> dalla raccolta in uno dei due modi seguenti:  
  
-   Eseguendo un'iterazione nella raccolta mediante un costrutto quale `foreach` \(in C\#\) o `For``Each` \(in Visual Basic\).  
  
-   Usando la proprietà <xref:System.Text.RegularExpressions.CaptureCollection.Item%2A?displayProperty=fullName> per recuperare un oggetto specifico in base all'indice. La proprietà <xref:System.Text.RegularExpressions.CaptureCollection.Item%2A> è la proprietà predefinita \(in Visual Basic\) o l'indicizzatore \(in C\#\) dell'oggetto <xref:System.Text.RegularExpressions.CaptureCollection>.  
  
 Se a un gruppo di acquisizione non è applicato alcun quantificatore, l'oggetto <xref:System.Text.RegularExpressions.CaptureCollection> conterrà un singolo oggetto <xref:System.Text.RegularExpressions.Capture> di scarso interesse, poiché fornisce informazioni sulla stessa corrispondenza indicata dall'oggetto <xref:System.Text.RegularExpressions.Group>. Se a un gruppo di acquisizione è applicato un quantificatore, l'oggetto <xref:System.Text.RegularExpressions.CaptureCollection> conterrà tutte le acquisizioni eseguite dal gruppo di acquisizione e l'ultimo membro della raccolta rappresenterà la stessa acquisizione indicata dall'oggetto <xref:System.Text.RegularExpressions.Group>.  
  
 Ad esempio, se si usa il criterio di espressione regolare `((a(b))c)+`, in cui il quantificatore \+ specifica una o più corrispondenze, per acquisire corrispondenze dalla stringa "abcabcabc", l'oggetto <xref:System.Text.RegularExpressions.CaptureCollection> per ogni oggetto <xref:System.Text.RegularExpressions.Group> includerà tre membri.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/capturecollection1.cs#14)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/capturecollection1.vb#14)]  
  
 L'esempio seguente usa l'espressione regolare `(Abc)+` per trovare una o più esecuzioni consecutive della stringa "Abc" nella stringa "XYZAbcAbcAbcXYZAbcAb". L'esempio illustra l'uso della proprietà <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=fullName> per restituire più gruppi di sottostringhe acquisite.  
  
 [!code-csharp[RegularExpressions.Classes#5](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Classes/cs/Example.cs#5)]
 [!code-vb[RegularExpressions.Classes#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Classes/vb/Example.vb#5)]  
  
 [Torna all'inizio](#introduction)  
  
<a name="the_individual_capture"></a>   
## Singola acquisizione  
 La classe <xref:System.Text.RegularExpressions.Capture> include i risultati di una singola acquisizione di sottoespressione. La proprietà <xref:System.Text.RegularExpressions.Capture.Value%2A?displayProperty=fullName> include il testo con corrispondenza e la proprietà <xref:System.Text.RegularExpressions.Capture.Index%2A?displayProperty=fullName> indica la posizione a base zero nella stringa di input in cui inizia la sottostringa con corrispondenza.  
  
 L'esempio seguente analizza una stringa di input per ottenere la temperatura di città selezionate. Una città e la relativa temperatura sono separate da una virgola \(","\) e un punto e virgola \(";"\) separa i dati di ogni città. L'intera stringa di input rappresenta una singola corrispondenza. Nel criterio di espressione regolare `((\w+(\s\w+)*),(\d+);)+`, usato per analizzare la stringa, il nome della città è assegnato al secondo gruppo di acquisizione e la temperatura al quarto.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/capture1.cs#16)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/capture1.vb#16)]  
  
 L'espressione regolare è definita nel modo illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`\w+`|Trova la corrispondenza di uno o più caratteri alfanumerici.|  
|`(\s\w+)*`|Trova la corrispondenza con zero o più occorrenze di un carattere di spaziatura seguito da uno o più caratteri di parola. Questo modello corrisponde a nomi di città composti da più parole. Equivale al terzo gruppo di acquisizione.|  
|`(\w+(\s\w+)*)`|Trova la corrispondenza con uno o più caratteri di parola seguiti da zero o più caratteri di spaziatura e uno o più caratteri di parola. Equivale al secondo gruppo di acquisizione.|  
|`,`|Trova la corrispondenza con una virgola.|  
|`(\d+)`|Trova la corrispondenza con una o più cifre. Questo è il quarto gruppo di acquisizione.|  
|`;`|Trova la corrispondenza con un punto e virgola.|  
|`((\w+(\s\w+)*),(\d+);)+`|Trova la corrispondenza con modello di una parola seguita da parole aggiuntive seguite da una virgola, una o più cifre e un punto e virgola, una o più volte. Equivale al primo gruppo di acquisizione.|  
  
## Vedere anche  
 <xref:System.Text.RegularExpressions>   
 [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)   
 [Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)