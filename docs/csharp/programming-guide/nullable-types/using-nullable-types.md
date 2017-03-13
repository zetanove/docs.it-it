---
title: "Utilizzo dei tipi nullable (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "nullable (tipi) [C#], informazioni sui tipi nullable"
ms.assetid: 0bacbe72-ce15-4b14-83e1-9c14e6380c28
caps.latest.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 31
---
# Utilizzo dei tipi nullable (Guida per programmatori C#)
I tipi nullable possono rappresentare tutti i valori di un tipo sottostante e un valore [null](../../../csharp/language-reference/keywords/null.md) aggiuntivo.  Vengono dichiarati in uno dei seguenti modi:  
  
 `System.Nullable<T> variable`  
  
 In alternativa  
  
 `T?  variable`  
  
 `T` è il tipo sottostante del tipo nullable.  `T` può essere qualsiasi tipo di valore, compreso `struct`, ma non può essere un tipo di riferimento.  
  
 Per un esempio relativo ai casi di utilizzo di un tipo nullable, si consideri che una variabile booleana ordinaria può avere due valori: true e false.  Non esiste alcun valore che significa "non definito".  In numerose applicazioni di programmazione, in particolare nelle interazioni di database, possono essere presenti variabili con uno stato non definito.  Un campo di un database, ad esempio, può contenere i valori true o false, ma può anche non contenere alcun valore.  Analogamente, i tipi di riferimento possono essere impostati su `null` per indicare che non sono inizializzati.  
  
 Questa differenza può comportare un aumento del lavoro di programmazione poiché richiede l'utilizzo di ulteriori variabili per archiviare le informazioni sullo stato, l'utilizzo di valori speciali e così via.  Mediante il modificatore dei tipi nullable, in C\# è possibile creare variabili di tipo di valore che indicano un valore non definito.  
  
## Esempi di tipi nullable  
 È possibile utilizzare qualsiasi tipo di valore come base per un tipo nullable.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideTypes#4](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_1.cs)]  
  
## Membri dei tipi nullable  
 Ogni istanza di un tipo nullable dispone di due proprietà pubbliche in sola lettura:  
  
-   `HasValue`  
  
     `HasValue` è di tipo `bool`.  È impostata su `true` se la variabile contiene un valore non null.  
  
-   `Value`  
  
     `Value` è dello stesso tipo del tipo sottostante.  Se `HasValue` è impostata su `true`, `Value` conterrà un valore significativo.  Se `HasValue` è impostata su `false`, l'accesso a `Value` genererà un'eccezione <xref:System.InvalidOperationException>.  
  
 In questo esempio viene utilizzato il membro `HasValue` per verificare se la variabile contiene un valore prima di tentare di visualizzarlo.  
  
 [!code-cs[csProgGuideTypes#5](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_2.cs)]  
  
 È anche possibile eseguire il test di un valore come nell'esempio riportato di seguito:  
  
 [!code-cs[csProgGuideTypes#6](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_3.cs)]  
  
## Conversioni esplicite  
 È possibile eseguire il cast di un tipo nullable su un tipo regolare, in modo esplicito tramite cast oppure mediante la proprietà `Value`.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideTypes#7](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_4.cs)]  
  
 Se è stata definita una conversione specifica tra due tipi di dati, sarà possibile utilizzare la stessa conversione anche con le versioni nullable di questi tipi.  
  
## Conversioni implicite  
 Una variabile di tipo nullable può essere impostata su null con la parola chiave `null`, come illustrato nell'esempio riportato di seguito:  
  
 [!code-cs[csProgGuideTypes#8](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_5.cs)]  
  
 La conversione da un tipo ordinario a un tipo nullable è implicita.  
  
 [!code-cs[csProgGuideTypes#9](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_6.cs)]  
  
## Operatori  
 Con i tipi nullable è anche possibile utilizzare gli operatori unari e binari predefiniti, nonché gli eventuali operatori definiti dall'utente disponibili per i tipi di valore esistenti.  Se gli operandi sono null, questi operatori generano un valore null. In caso contrario, per calcolare il risultato l'operando utilizza il valore contenuto.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideTypes#10](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_7.cs)]  
  
 Quando si eseguono confronti con tipi nullable, se il valore di uno dei tipi nullable è null e l'altro no, tutti i confronti restituiscono `false` ad eccezione di `!=` \(diverso da\).  È importante non presupporre che, poiché un particolare confronto restituisce `false`, il caso opposto restituisca `true`.  Nell'esempio seguente 10 non è maggiore di, minore di o uguale a null.  Solo `num1 != num2` restituisce `true`.  
  
 [!code-cs[csProgGuideTypes#11](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_8.cs)]  
  
 Un confronto di uguaglianze di due tipi nullable che sono entrambi null restituisce `true`.  
  
## OperatoreOperatore  
 L'operatore `??` definisce un valore predefinito che viene restituito quando un tipo nullable viene assegnato a un tipo non nullable.  
  
 [!code-cs[csProgGuideTypes#12](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_9.cs)]  
  
 Questo operatore può essere utilizzato anche con più tipi nullable.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideTypes#13](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_10.cs)]  
  
## Tipotype  
 Il tipo nullable `bool?` può contenere tre valori diversi: [true](../../../csharp/language-reference/keywords/true.md), [false](../../../csharp/language-reference/keywords/false.md) e [null](../../../csharp/language-reference/keywords/null.md).  Per informazioni sull'esecuzione del cast da un tipo bool?  a un tipo bool, vedere [Procedura: eseguire il cast sicuro da bool? a bool](../../../csharp/programming-guide/nullable-types/how-to-safely-cast-from-bool-to-bool.md).  
  
 I valori booleani nullable sono come il tipo di variabile booleano utilizzato in SQL.  Per verificare che i risultati prodotti da `&` e  `|` siano coerenti con il tipo booleano a tre valori di SQL, sono disponibili i seguenti operatori predefiniti:  
  
 `bool?  operator &(bool?  x, bool?  y)`  
  
 `bool?  operator |(bool?  x, bool?  y)`  
  
 I risultati di questi operatori sono elencati nella tabella riportata di seguito:  
  
|X|y|x&y|x&#124;y|  
|-------|-------|---------|--------------|  
|true|true|true|true|  
|true|false|false|true|  
|true|null|null|true|  
|false|true|false|true|  
|false|false|false|false|  
|false|null|false|null|  
|null|true|null|true|  
|null|false|false|null|  
|null|null|null|null|  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)   
 [Conversione boxing dei tipi nullable](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)   
 [Nullable Value Types](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)