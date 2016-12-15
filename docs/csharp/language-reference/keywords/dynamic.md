---
title: "dynamic (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "dynamic_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "dynamic [C#]"
  - "dynamic (parola chiave) [C#]"
ms.assetid: 9e797102-cc83-4964-bf58-afe4f54d16bc
caps.latest.revision: 25
caps.handback.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# dynamic (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il tipo `dynamic` abilita le operazioni nelle quali il controllo dei tipi in fase di compilazione viene ignorato.  Queste operazioni vengono invece risolte in fase di esecuzione.  Il tipo `dynamic` semplifica l'accesso alle API COM, quali le API di automazione di Office, alle API dinamiche, quali le librerie IronPython, e al modello DOM \(Document Object Model\) HTML.  
  
 Il tipo `dynamic` si comporta come tipo `object` nella maggior parte delle circostanze.  Le operazioni che contengono espressioni di tipo `dynamic` tuttavia non vengono risolte o sono sottoposte a controllo del tipo da parte del compilatore.  Il compilatore raggruppa le informazioni sull'operazione e tali informazioni vengono utilizzate in un secondo momento per valutare l'operazione in fase di esecuzione.  Come parte del processo, le variabili del tipo `dynamic` vengono compilate in variabili di tipo `object`.  Il tipo `dynamic` esiste quindi solo in fase di compilazione, non in fase di esecuzione.  
  
 Nell'esempio che segue, la variabile di tipo `dynamic` viene messa a confronto con una variabile di tipo `object`.  Per verificare il tipo di ciascuna variabile in fase di compilazione, posizionare il puntatore del mouse su `dyn` o `obj` nelle istruzioni `WriteLine`.  IntelliSense mostra **dynamic** per `dyn` e **object** per `obj`.  
  
 [!code-cs[csrefKeywordsTypes#21](../../../csharp/language-reference/keywords/codesnippet/CSharp/dynamic_1.cs)]  
  
 Le istruzioni `WriteLine` visualizzano i tipi di runtime di `dyn` e `obj`.  A quel punto, entrambi hanno lo stesso tipo, numero intero.  Il risultato è il seguente:  
  
 `System.Int32`  
  
 `System.Int32`  
  
 Per vedere in fase di compilazione la differenza tra `dyn` e `obj`, aggiungere le due righe seguenti tra le dichiarazioni e le istruzioni `WriteLine` nell'esempio precedente.  
  
```c#  
dyn = dyn + 3;  
obj = obj + 3;  
  
```  
  
 Viene segnalato un errore del compilatore per il tentativo di aggiunta di un numero intero e di un oggetto in un'espressione `obj + 3`.  Tuttavia, non è stato segnalato alcun errore per `dyn + 3`.  L'espressione che contiene `dyn` non viene controllata in fase di compilazione perché il tipo di `dyn` è `dynamic`.  
  
## Contesto  
 La parola chiave `dynamic` può essere visualizzata direttamente o come componente di un tipo costruito nelle situazioni seguenti:  
  
-   Nelle dichiarazioni, come tipo di una proprietà, campo, indicizzatore, parametro, valore restituito, variabile locale o vincolo di tipo.  Nella definizione della classe seguente viene utilizzato `dynamic` in molte dichiarazioni diverse.  
  
     [!code-cs[csrefKeywordsTypes#22](../../../csharp/language-reference/keywords/codesnippet/CSharp/dynamic_2.cs)]  
  
-   In conversioni esplicite del tipo, come tipo di destinazione di una conversione.  
  
     [!code-cs[csrefKeywordsTypes#23](../../../csharp/language-reference/keywords/codesnippet/CSharp/dynamic_3.cs)]  
  
-   In ogni contesto in cui i tipi vengono utilizzati come valori, come sul lato destro dell'operatore `is` o dell'operatore `as`, o come argomento a `typeof` come parte di un tipo costruito.  Ad esempio, nelle seguenti espressioni è possibile utilizzare `dynamic`.  
  
     [!code-cs[csrefKeywordsTypes#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/dynamic_4.cs)]  
  
## Esempio  
 Nell'esempio seguente viene utilizzato `dynamic` in molte dichiarazioni.  Il metodo `Main` contrappone anche il controllo dei tipi in fase di compilazione con il controllo dei tipi in fase di esecuzione.  
  
 [!code-cs[csrefKeywordsTypes#25](../../../csharp/language-reference/keywords/codesnippet/CSharp/dynamic_5.cs)]  
  
 Per ulteriori informazioni ed esempi, vedere [Utilizzo del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md).  
  
## Vedere anche  
 <xref:System.Dynamic.ExpandoObject?displayProperty=fullName>   
 <xref:System.Dynamic.DynamicObject?displayProperty=fullName>   
 [Utilizzo del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [oggetto](../../../csharp/language-reference/keywords/object.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [as](../../../csharp/language-reference/keywords/as.md)   
 [typeof](../../../csharp/language-reference/keywords/typeof.md)   
 [Procedura: eseguire il cast sicuro tramite gli operatori as e is](../../../csharp/programming-guide/types/how-to-safely-cast-by-using-as-and-is-operators.md)   
 [Procedura dettagliata: creazione e utilizzo di oggetti dinamici](../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)