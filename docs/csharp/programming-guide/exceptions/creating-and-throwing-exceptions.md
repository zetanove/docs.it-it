---
title: Creazione e generazione di eccezioni (Guida per programmatori C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- catching exceptions [C#]
- throwing exceptions [C#]
- exceptions [C#], creating
- exceptions [C#], throwing
ms.assetid: 6bbba495-a115-4c6d-90cc-1f4d7b5f39e2
caps.latest.revision: 28
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c3eab50a6a785676dd397498fbe95348187e2b7e
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="creating-and-throwing-exceptions-c-programming-guide"></a>Creazione e generazione di eccezioni (Guida per programmatori C#)
Le eccezioni vengono usate per indicare che si è verificato un errore durante l'esecuzione del programma. Vengono creati oggetti eccezione che descrivono un errore e quindi *generati* con la parola chiave [throw](../../../csharp/language-reference/keywords/throw.md). Il runtime cerca quindi il gestore di eccezioni più compatibile.  
  
 I programmatori devono generare eccezioni quando una o più delle condizioni seguenti sono true:  
  
-   Il metodo non può completare la funzionalità definita.  
  
     Ad esempio, se un parametro verso un metodo ha un valore non valido:  
  
     [!code-cs[csProgGuideExceptions#12](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/creating-and-throwing-exceptions_1.cs)]  
  
-   Viene eseguita una chiamata non appropriata a un oggetto, in base allo stato dell'oggetto.  
  
     Un esempio potrebbe essere il tentativo di scrivere su un file di sola lettura. Nei casi in cui lo stato di un oggetto non consente un'operazione, generare un'istanza di <xref:System.InvalidOperationException> o un oggetto sulla base di una derivazione di questa classe. Questo è un esempio di un metodo che genera un oggetto <xref:System.InvalidOperationException>:  
  
     [!code-cs[csProgGuideExceptions#13](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/creating-and-throwing-exceptions_2.cs)]  
  
-   Quando un argomento verso un metodo genera un'eccezione.  
  
     In questo caso, è necessario intercettare l'eccezione originale e creare un'istanza <xref:System.ArgumentException>. L'eccezione originale deve essere passato al costruttore di <xref:System.ArgumentException> come parametro <xref:System.Exception.InnerException%2A>:  
  
     [!code-cs[csProgGuideExceptions#14](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/creating-and-throwing-exceptions_3.cs)]  
  
 Le eccezioni contengono una proprietà denominata <xref:System.Exception.StackTrace%2A>. Questa stringa contiene il nome dei metodi nello stack di chiamate corrente, insieme al numero di riga e al nome del file in cui è stata generata l'eccezione per ogni metodo. Viene creato in automatico un oggetto <xref:System.Exception.StackTrace%2A> da Common Language Runtime (CLR) dal punto dell'istruzione `throw`, in modo tale che le eccezioni debbano essere create dal punto in cui deve iniziare l'analisi dello stack.  
  
 Tutte le eccezioni contengono una proprietà denominata <xref:System.Exception.Message%2A>. Questa stringa deve essere impostata per spiegare il motivo dell'eccezione. Si noti che le informazioni sensibili alla sicurezza non devono essere inserite nel testo del messaggio. Oltre a <xref:System.Exception.Message%2A>, <xref:System.ArgumentException> contiene una proprietà denominata <xref:System.ArgumentException.ParamName%2A> che deve essere impostata sul nome dell'argomento che ha causato la generazione dell'eccezione. Nel caso di un setter delle proprietà, <xref:System.ArgumentException.ParamName%2A> deve essere impostato su `value`.  
  
 I membri di metodi pubblici e protetti devono generare eccezioni quando non saranno in grado di completare le funzioni previste. La classe di eccezione generata deve essere l'eccezione più specifica disponibile che soddisfa le condizioni di errore. Queste eccezioni devono essere documentate come parte delle funzionalità della classe e le classi derivate o gli aggiornamenti per la classe originale devono conservare lo stesso comportamento per la compatibilità con le versioni precedenti.  
  
## <a name="things-to-avoid-when-throwing-exceptions"></a>Comportamenti da evitare per la generazione di eccezioni  
 L'elenco seguente include operazioni da evitare durante la generazione di eccezioni:  
  
-   Le eccezioni non devono essere usate per modificare il flusso di un programma come parte della normale esecuzione. Le eccezioni non devono essere usate per notificare e gestire le condizioni di errore.  
  
-   Le eccezioni non devono essere restituite come valore o parametro restituito anziché generato.  
  
-   Non generare <xref:System.Exception?displayProperty=fullName>, <xref:System.SystemException?displayProperty=fullName>, <xref:System.NullReferenceException?displayProperty=fullName> o <xref:System.IndexOutOfRangeException?displayProperty=fullName> Intenzionalmente dal codice sorgente.  
  
-   Non creare eccezioni che possono essere generate in modalità di debug e non in modalità di rilascio. Per identificare gli errori di run-time durante la fase di sviluppo, usare il metodo di asserzione di debug.  
  
## <a name="defining-exception-classes"></a>Definizione delle classi di eccezioni  
 I programmi possono generare una classe di eccezione predefinita nello spazio dei nomi <xref:System>, ad eccezione dei casi indicati in precedenza, oppure creare proprie classi di eccezione da <xref:System.Exception>. Le classi derivate devono definire almeno quattro costruttori: uno predefinito, uno che imposta la proprietà del messaggio e uno che imposta sia la proprietà <xref:System.Exception.Message%2A> che la proprietà <xref:System.Exception.InnerException%2A>. Il quarto costruttore viene usato per serializzare l'eccezione. Le nuove classi di eccezione devono essere serializzabili. Ad esempio:  
  
 [!code-cs[csProgGuideExceptions#15](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/creating-and-throwing-exceptions_4.cs)]  
  
 Le nuove proprietà devono semplicemente essere aggiunte alla classe di eccezioni quando i dati che forniscono sono utili per risolvere l'eccezione. Se vengono aggiunte nuove proprietà alla classe di eccezioni derivata, `ToString()` deve essere sottoposto a override per restituire le informazioni aggiunte.  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/index.md)   
 [Gerarchia delle eccezioni](http://msdn.microsoft.com/library/f7d68675-be06-40fb-a555-05f0c5a6f66b)   
 [Gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exception-handling.md)
