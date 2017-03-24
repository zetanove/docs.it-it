---
title: "Procedura: dichiarare un delegato, crearne un&#39;istanza e utilizzarlo (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "delegati [C#], dichiarazione e creazione di istanze"
ms.assetid: 61c4895f-f785-48f8-8bfe-db73b411c4ae
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# Procedura: dichiarare un delegato, crearne un&#39;istanza e utilizzarlo (Guida per programmatori C#)
In C\# 1.0 e versioni successive i delegati possono essere dichiarati come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideDelegates#13](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_1.cs)]  
  
 [!code-cs[csProgGuideDelegates#14](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_2.cs)]  
  
 In C\# 2.0 è disponibile un metodo più semplice scrivere la dichiarazione precedente, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideDelegates#32](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_3.cs)]  
  
 In C\# 2.0 e versioni successive, è anche possibile utilizzare un metodo anonimo per dichiarare e inizializzare un [delegato](../../../csharp/language-reference/keywords/delegate.md), come illustrato esempio seguente.  
  
 [!code-cs[csProgGuideDelegates#15](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_4.cs)]  
  
 In C\# 3.0 e versioni successive, è inoltre possibile dichiarare i delegati e crearne un'istanza utilizzando un'espressione lambda, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideDelegates#31](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_5.cs)]  
  
 Per ulteriori informazioni, vedere [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 Nell'esempio che segue viene illustrato come dichiarare, creare un'istanza e utilizzare un delegato.  La classe `BookDB` incapsula il database di una libreria che gestisce un database di volumi.  Espone un metodo `ProcessPaperbackBooks`, che ricerca tutti i tascabili all'interno del database e chiama un delegato per ciascuno di essi.  Il tipo `delegate` utilizzato viene denominato `ProcessBookDelegate`.  La classe `Test` utilizza questa classe per stampare i titoli e il prezzo medio dei tascabili.  
  
 L'utilizzo dei delegati consente la separazione ottimale delle funzionalità tra il database della libreria e il codice client.  Il codice client non contiene alcuna informazione sulle modalità di archiviazione dei libri o sul meccanismo che consente al codice di individuare i tascabili;  il codice della libreria non contiene alcuna informazione sull'elaborazione effettuata sui tascabili individuati.  
  
## Esempio  
 [!code-cs[csProgGuideDelegates#12](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_6.cs)]  
  
## Programmazione efficiente  
  
-   Dichiarazione di un delegato.  
  
     Nell'istruzione seguente viene dichiarato un nuovo tipo delegato.  
  
     [!code-cs[csProgGuideDelegates#16](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_7.cs)]  
  
     Ciascun tipo di delegato descrive il numero e il tipo degli argomenti e il tipo di valore restituito dai metodi in esso incapsulato.  Ogni volta che è necessario una nuovo insieme di tipi di argomento o un nuovo tipo di valore restituito, è necessario dichiarare un nuovo tipo di delegato.  
  
-   Creazione di un'istanza di un delegato.  
  
     Dopo aver dichiarato un tipo delegato, è necessario creare un oggetto delegato e associarlo a un determinato metodo.  Nell'esempio precedente questa operazione viene eseguita passando il metodo `PrintTitle` al metodo `ProcessPaperbackBooks`, come illustrato nell'esempio seguente:  
  
     [!code-cs[csProgGuideDelegates#17](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_8.cs)]  
  
     Viene creato un nuovo oggetto delegato associato al metodo crea un nuovo oggetto delegato associato al metodo [statico](../../../csharp/language-reference/keywords/static.md)`Test.PrintTitle`.  Analogamente, il metodo non statico `AddBookToTotal` sull'oggetto `totaller` viene passato come illustrato nell'esempio seguente:  
  
     [!code-cs[csProgGuideDelegates#18](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_9.cs)]  
  
     In entrambi i casi un nuovo oggetto delegato viene passato al metodo `ProcessPaperbackBooks`.  
  
     Dopo la creazione di un delegato, il metodo ad esso associato non viene mai modificato: gli oggetti delegati non sono modificabili.  
  
-   Chiamata a un delegato.  
  
     Una volta creato un oggetto delegato, questo viene in genere passato a un altro codice che chiamerà il delegato.  Per la chiamata di un oggetto delegato viene utilizzato il nome dell'oggetto stesso, seguito dagli argomenti, racchiusi tra parentesi, che devono essere passati al delegato.  Di seguito viene riportato un esempio di chiamata a un delegato:  
  
     [!code-cs[csProgGuideDelegates#19](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_10.cs)]  
  
     Un delegato può essere chiamato in modo sincrono, come in questo esempio, o in modo asincrono utilizzando i metodi `BeginInvoke` e `EndInvoke`.  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)