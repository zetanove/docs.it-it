---
title: "static (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "static"
  - "static_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "static (parola chiave) [C#]"
ms.assetid: 5509e215-2183-4da3-bab4-6b7e607a4fdf
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# static (Riferimenti per C#)
Utilizzare il modificatore `static` per dichiarare un membro statico che appartiene al tipo stesso anziché a un oggetto specifico.  Il modificatore `static` può essere utilizzato con classi, campi, metodi, proprietà, operatori, eventi e costruttori, ma non con indicizzatori, distruttori o tipi che non sono classi.  Per ulteriori informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
## Esempio  
 La classe seguente viene dichiarata come `static` e contiene soltanto metodi `static`:  
  
 [!code-cs[csrefKeywordsModifiers#18](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#18)]  
  
 Una dichiarazione di costanti o di tipi è in modo implicito un membro static.  
  
 Non è possibile fare riferimento a un membro static mediante un'istanza.  È invece possibile ottenere il risultato desiderato utilizzando il nome del tipo in cui è dichiarato.  Si consideri ad esempio la seguente classe:  
  
 [!code-cs[csrefKeywordsModifiers#19](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#19)]  
  
 Per fare riferimento al membro statico `x`, utilizzare il nome completo, `MyBaseC.MyStruct.x`, a meno che il membro non sia accessibile dallo stesso ambito:  
  
```c#  
Console.WriteLine(MyBaseC.MyStruct.x);  
```  
  
 Mentre l'istanza di una classe contiene una copia distinta di tutti i campi di istanza della classe, esiste una sola copia per ciascun campo static.  
  
 Non è possibile utilizzare [this](../../../csharp/language-reference/keywords/this.md) per fare riferimento a metodi statici o a funzioni di accesso della proprietà statiche.  
  
 Se la parola chiave `static` viene applicata a una classe, tutti i membri della classe devono essere statici.  
  
 Le classi e le classi statiche potrebbero avere costruttori statici.  I costruttori statici vengono chiamati in un determinato momento compreso tra l'avvio del programma e la creazione di un'istanza della classe.  
  
> [!NOTE]
>  La parola chiave `static` ha un utilizzo limitato rispetto a C\+\+.  Per un confronto con la corrispondente parola chiave di C\+\+, vedere [Statico](/visual-cpp/misc/static-cpp).  
  
 Per illustrare le caratteristiche dei membri statici, si consideri una classe che rappresenta un dipendente di un'azienda.  Si supponga che la classe contenga un metodo per conteggiare i dipendenti e un campo per memorizzarne il numero.  Sia il metodo che il campo non appartengono ad alcuna istanza di tipo dipendente,  in quanto appartengono alla classe azienda  e devono pertanto essere dichiarati come membri static della classe.  
  
## Esempio  
 In questo esempio si leggono il nome e l'identificatore di un nuovo dipendente; il contatore di dipendenti viene quindi incrementato di un'unità e vengono visualizzate le informazioni relative al nuovo dipendente e al numero di dipendenti aggiornato.  Per semplicità, questo programma legge il numero attuale di dipendenti dalla tastiera.  In un'applicazione reale, queste informazioni verrebbero lette da un file.  
  
 [!code-cs[csrefKeywordsModifiers#20](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#20)]  
  
## Esempio  
 In questo esempio viene mostrato che, sebbene sia possibile inizializzare un campo statico tramite un altro campo statico non ancora dichiarato, i risultati non saranno definiti finché non verrà assegnato un valore al campo statico in modo esplicito.  
  
 [!code-cs[csrefKeywordsModifiers#21](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#21)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)