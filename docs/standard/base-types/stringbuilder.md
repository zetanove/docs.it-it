---
title: "Uso della classe StringBuilder in .NET Framework | Microsoft Docs"
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
  - "Remove (metodo)"
  - "stringhe [.NET Framework], capacità"
  - "StringBuilder (oggetto)"
  - "Replace (metodo)"
  - "AppendFormat (metodo)"
  - "Append (metodo)"
  - "Insert (metodo)"
  - "stringhe [.NET Framework], oggetto StringBuilder"
ms.assetid: 5c14867c-9a99-45bc-ae7f-2686700d377a
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Uso della classe StringBuilder in .NET Framework
L'oggetto <xref:System.String> non è modificabile. Ogni volta che si usa uno dei metodi nella classe <xref:System.String?displayProperty=fullName>, si crea un nuovo oggetto stringa in memoria che richiede una nuova allocazione di spazio. In situazioni in cui è necessario modificare ripetutamente una stringa, il sovraccarico associato alla creazione di un nuovo oggetto <xref:System.String> può essere dispendioso. La classe <xref:System.Text.StringBuilder?displayProperty=fullName> può essere usata per modificare una stringa senza creare un nuovo oggetto. Ad esempio, l'uso della classe <xref:System.Text.StringBuilder> può migliorare le prestazioni quando si concatenano più stringhe in un ciclo.  
  
## Importazione dello spazio dei nomi System.Type  
 La classe <xref:System.Text.StringBuilder> si trova nello spazio dei nomi <xref:System.Text>.  Per evitare di specificare il nome di tipo completo nel codice, è possibile importare lo spazio dei nomi <xref:System.Text>:  
  
 [!code-cpp[Conceptual.StringBuilder#11](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#11)]
 [!code-csharp[Conceptual.StringBuilder#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#11)]
 [!code-vb[Conceptual.StringBuilder#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#11)]  
  
## Creazione di un'istanza di un oggetto StringBuilder  
 È possibile creare una nuova istanza della classe <xref:System.Text.StringBuilder> inizializzando la variabile con uno dei metodi del costruttore di overload, come illustrato nell'esempio seguente.  
  
 [!code-cpp[Conceptual.StringBuilder#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#1)]
 [!code-csharp[Conceptual.StringBuilder#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#1)]
 [!code-vb[Conceptual.StringBuilder#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#1)]  
  
## Impostazione di capacità e lunghezza  
 Anche se <xref:System.Text.StringBuilder> è un oggetto dinamico che consente di espandere il numero di caratteri nella stringa incapsulata, è possibile specificare un valore per il numero massimo di caratteri che può contenere. Questo valore rappresenta la capacità dell'oggetto e non deve essere confuso con la lunghezza della stringa contenuta dall'oggetto <xref:System.Text.StringBuilder>. Ad esempio, è possibile creare una nuova istanza della classe <xref:System.Text.StringBuilder> con la stringa "Hello", che ha una lunghezza pari a 5 caratteri, e specificare che l'oggetto ha una capacità massima di 25 caratteri. Quando si modifica la classe <xref:System.Text.StringBuilder>, le dimensioni non vengono riallocate automaticamente fino a quando non viene raggiunta la capacità specificata. In questo caso, il nuovo spazio viene allocato automaticamente e la capacità viene raddoppiata. È possibile specificare la capacità della classe <xref:System.Text.StringBuilder> usando uno dei costruttori di overload. L'esempio seguente specifica che l'oggetto `MyStringBuilder` può essere ampliato fino a un massimo di 25 spazi.  
  
 [!code-cpp[Conceptual.StringBuilder#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#2)]
 [!code-csharp[Conceptual.StringBuilder#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#2)]
 [!code-vb[Conceptual.StringBuilder#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#2)]  
  
 Inoltre, è possibile usare la proprietà <xref:System.Text.StringBuilder.Capacity%2A> di lettura\/scrittura per impostare la lunghezza massima dell'oggetto. L'esempio seguente usa la proprietà **Capacità** per definire la lunghezza massima dell'oggetto.  
  
 [!code-cpp[Conceptual.StringBuilder#3](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#3)]
 [!code-csharp[Conceptual.StringBuilder#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#3)]
 [!code-vb[Conceptual.StringBuilder#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#3)]  
  
 Il metodo <xref:System.Text.StringBuilder.EnsureCapacity%2A> può essere usato per verificare la capacità dell'oggetto **StringBuilder** corrente. Se la capacità è maggiore del valore passato, non vengono apportate modifiche. Invece, se la capacità è minore del valore passato, la capacità corrente viene modificata in modo che corrisponda al valore passato.  
  
 La proprietà <xref:System.Text.StringBuilder.Length%2A> può essere anche visualizzata o impostata. Se si imposta la proprietà **Lunghezza** su un valore maggiore della proprietà **Capacità**, la proprietà **Capacità** viene impostata automaticamente sullo stesso valore della proprietà **Lunghezza**. L'impostazione della proprietà **Lunghezza** su un valore minore della lunghezza della stringa all'interno dell'oggetto **StringBuilder** corrente consente di abbreviare la stringa.  
  
## Modifica della stringa StringBuilder  
 La tabella seguente elenca i metodi che è possibile usare per modificare il contenuto di **StringBuilder**.  
  
|Nome metodo|Uso|  
|-----------------|---------|  
|<xref:System.Text.StringBuilder.Append%2A?displayProperty=fullName>|Aggiunge informazioni alla fine dell'oggetto **StringBuilder** corrente.|  
|<xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=fullName>|Sostituisce un identificatore di formato passato in una stringa con il testo formattato.|  
|<xref:System.Text.StringBuilder.Insert%2A?displayProperty=fullName>|Inserisce una stringa o un oggetto nell'indice specificato dell'oggetto **StringBuilder** corrente.|  
|<xref:System.Text.StringBuilder.Remove%2A?displayProperty=fullName>|Rimuove un numero specificato di caratteri dall'oggetto **StringBuilder** corrente.|  
|<xref:System.Text.StringBuilder.Replace%2A?displayProperty=fullName>|Sostituisce un determinato carattere nell'indice specificato.|  
  
### Aggiungi  
 Il metodo **Append** può essere usato per aggiungere testo o una rappresentazione di stringa di un oggetto alla fine di una stringa rappresentata dall'oggetto **StringBuilder** corrente. Nell'esempio seguente viene inizializzato un oggetto **StringBuilder** su "Hello World" e quindi viene aggiunto il testo alla fine dell'oggetto. Lo spazio viene allocato automaticamente in base alle esigenze.  
  
 [!code-cpp[Conceptual.StringBuilder#4](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#4)]
 [!code-csharp[Conceptual.StringBuilder#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#4)]
 [!code-vb[Conceptual.StringBuilder#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#4)]  
  
### AppendFormat  
 Il metodo <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=fullName> aggiunge il testo alla fine dell'oggetto <xref:System.Text.StringBuilder>. Supporta la funzionalità di formattazione composita \(per altre informazioni, vedere [Formattazione composita](../../../docs/standard/base-types/composite-formatting.md)\) chiamando l'implementazione <xref:System.IFormattable> dell'oggetto o gli oggetti da formattare. Pertanto, accetta le stringhe di formato standard per i valori numerici, di data e ora e di enumerazione, le stringhe di formato personalizzato per i valori numerici e di data e ora e le stringhe di formato definite per i tipi personalizzati. Per informazioni sulla formattazione, vedere [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md). È possibile usare questo metodo per personalizzare il formato delle variabili e aggiungere tali valori a <xref:System.Text.StringBuilder>. L'esempio seguente usa il metodo <xref:System.Text.StringBuilder.AppendFormat%2A> per inserire un valore Integer formattato come valore di valuta alla fine di un oggetto <xref:System.Text.StringBuilder>.  
  
 [!code-cpp[Conceptual.StringBuilder#5](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#5)]
 [!code-csharp[Conceptual.StringBuilder#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#5)]
 [!code-vb[Conceptual.StringBuilder#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#5)]  
  
### INS  
 Il metodo <xref:System.Text.StringBuilder.Insert%2A> aggiunge una stringa o un oggetto in una posizione specificata nell'oggetto <xref:System.Text.StringBuilder> corrente. L'esempio seguente usa questo metodo per inserire una parola nella sesta posizione di un oggetto <xref:System.Text.StringBuilder>.  
  
 [!code-cpp[Conceptual.StringBuilder#6](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#6)]
 [!code-csharp[Conceptual.StringBuilder#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#6)]
 [!code-vb[Conceptual.StringBuilder#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#6)]  
  
### Rimuovi  
 È possibile usare il metodo **Remove** per rimuovere un numero specificato di caratteri dall'oggetto <xref:System.Text.StringBuilder> corrente, a partire dall'indice in base zero specificato. L'esempio seguente usa il metodo **Remove** per abbreviare un oggetto <xref:System.Text.StringBuilder>.  
  
 [!code-cpp[Conceptual.StringBuilder#7](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#7)]
 [!code-csharp[Conceptual.StringBuilder#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#7)]
 [!code-vb[Conceptual.StringBuilder#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#7)]  
  
### Sostituire  
 Il metodo **Replace** può essere usato per sostituire i caratteri all'interno dell'oggetto <xref:System.Text.StringBuilder> con un altro carattere specificato. L'esempio seguente usa il metodo **Replace** per cercare un oggetto <xref:System.Text.StringBuilder> per tutte le istanze del carattere punto esclamativo \(\!\) e per sostituirle con il carattere punto interrogativo \(?\).  
  
 [!code-cpp[Conceptual.StringBuilder#8](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#8)]
 [!code-csharp[Conceptual.StringBuilder#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#8)]
 [!code-vb[Conceptual.StringBuilder#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#8)]  
  
## Conversione di un oggetto StringBuilder in una stringa  
 È necessario convertire l'oggetto <xref:System.Text.StringBuilder> in un oggetto <xref:System.String> prima di poter passare la stringa rappresentata dall'oggetto <xref:System.Text.StringBuilder> a un metodo che contiene un parametro <xref:System.String> o per visualizzarlo nell'interfaccia utente. Per eseguire la conversione, chiamare il metodo <xref:System.Text.StringBuilder.ToString%2A?displayProperty=fullName>. Nell'esempio seguente vengono chiamati diversi metodi <xref:System.Text.StringBuilder>, quindi viene chiamato il metodo <xref:System.Text.StringBuilder.ToString?displayProperty=fullName> per visualizzare la stringa.  
  
 [!code-csharp[Conceptual.StringBuilder#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/tostringexample1.cs#10)]
 [!code-vb[Conceptual.StringBuilder#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/tostringexample1.vb#10)]  
  
## Vedere anche  
 <xref:System.Text.StringBuilder?displayProperty=fullName>   
 [Operazioni di base su stringhe](../../../docs/standard/base-types/basic-string-operations.md)   
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)