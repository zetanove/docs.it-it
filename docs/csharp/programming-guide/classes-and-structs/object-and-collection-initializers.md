---
title: "Inizializzatori di oggetto e di raccolte (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "inizializzatori di raccolta [C#]"
  - "inizializzatori di oggetto [C#]"
ms.assetid: c58f3db5-d7d4-4651-bd2d-5a3a97357f61
caps.latest.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 27
---
# Inizializzatori di oggetto e di raccolte (Guida per programmatori C#)
Gli inizializzatori di oggetto consentono di assegnare valori a qualsiasi proprietà o campo accessibile di un oggetto in fase di creazione senza dover richiamare un costruttore seguito da righe di istruzioni di assegnazione.  La sintassi dell'inizializzatore di oggetto consente di specificare gli argomenti per un costruttore o di omettere gli argomenti \(e la sintassi di parentesi\).  Nell'esempio seguente viene illustrato come utilizzare un inizializzatore di oggetto con un tipo denominato, `Cat` e come richiamare il costruttore predefinito.  Si noti l'uso di proprietà implementate automaticamente nella classe `Cat`.  Per altre informazioni, vedere [Proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md).  
  
 [!code-cs[csProgGuideLINQ#39](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_1.cs)]  
  
 [!code-cs[csProgGuideLINQ#45](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_2.cs)]  
  
## Inizializzatori di oggetto con tipi anonimi  
 Anche se gli inizializzatori di oggetto possono essere utilizzati in qualsiasi contesto, sono particolarmente utili nelle espressioni di query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)].  Le espressioni di query si avvalgono di frequente di [tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md), che possono essere inizializzati solo con un inizializzatore di oggetto, come illustrato nella seguente dichiarazione.  
  
```  
var pet = new { Age = 10, Name = "Fluffy" };  
```  
  
 I tipi anonimi consentono alla clausola `select` in un'espressione di query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] di trasformare gli oggetti della sequenza originale in oggetti i cui valori e la cui forma potrebbero essere diversi dall'originale.  Questo è utile se si desidera archiviare solo una parte delle informazioni di ogni oggetto di una sequenza.  Nell'esempio seguente, si supponga che un oggetto prodotto \(`p`\) contenga diversi campi e metodi e che si sia interessati a creare solo una sequenza di oggetti che contengono il nome e il prezzo unitario del prodotto.  
  
 [!code-cs[csProgGuideLINQ#40](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_3.cs)]  
  
 Quando questa query verrà eseguita, la variabile `productInfos` conterrà una sequenza di oggetti a cui sarà possibile accedere in un'istruzione `foreach` come illustrato in questo esempio:  
  
```  
foreach(var p in productInfos){...}  
```  
  
 Ogni oggetto nel nuovo tipo anonimo dispone di due proprietà pubbliche che ricevono gli stessi nomi delle proprietà o dei campi nell'oggetto originale.  È inoltre possibile rinominare un campo mentre si crea un tipo anonimo. Nell'esempio seguente il campo `UnitPrice` viene rinominato in `Price`.  
  
```  
select new {p.ProductName, Price = p.UnitPrice};  
```  
  
## Inizializzatori di oggetto con tipi nullable  
 L'uso di un inizializzatore di oggetto con struct nullable genera un errore in fase di compilazione.  
  
## Inizializzatori di raccolta  
 Gli inizializzatori di raccolta consentono di specificare uno o più inizializzatori di elemento quando si inizializza una classe di raccolte che implementa <xref:System.Collections.IEnumerable> o una classe con un metodo di estensione `Add`.  Gli inizializzatori di elemento possono essere un semplice valore, un'espressione o un inizializzatore di oggetto.  Se si utilizza un inizializzatore di raccolta, non è necessario specificare più chiamate al metodo `Add` della classe nel codice sorgente, in quanto le chiamate vengono aggiunte dal compilatore.  
  
 Negli esempi seguenti vengono illustrati due semplici inizializzatori di raccolta:  
  
```  
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };  
List<int> digits2 = new List<int> { 0 + 1, 12 % 3, MakeInt() };  
```  
  
 Nell'inizializzatore di raccolta riportato di seguito vengono utilizzati inizializzatori di oggetto per inizializzare oggetti della classe `Cat` definiti in un esempio precedente.  Si noti che i singoli inizializzatori di oggetto sono racchiusi tra parentesi e separati da virgole.  
  
 [!code-cs[csProgGuideLINQ#41](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_4.cs)]  
  
 È possibile specificare [null](../../../csharp/language-reference/keywords/null.md) come elemento in un inizializzatore di raccolta se il metodo `Add` della raccolta lo consente.  
  
 [!code-cs[csProgGuideLINQ#42](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_5.cs)]  
  
 È possibile specificare elementi indicizzati se la raccolta supporta l'indicizzazione.  
  
```  
var numbers = new Dictionary<int, string> {   
    [7] = "seven",   
    [9] = "nine",   
    [13] = "thirteen"   
};  
  
```  
  
## Esempio  
 [!code-cs[csProgGuideLINQ#46](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_6.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)