---
title: "Utilizzo degli indicizzatori (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "indicizzatori [C#], informazioni sugli indicizzatori"
ms.assetid: df70e1a2-3ce3-4aba-ad80-4b2f3538699f
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# Utilizzo degli indicizzatori (Guida per programmatori C#)
Gli indicizzatori sono una convenzione sintattica che consente di creare una [classe](../../../csharp/language-reference/keywords/class.md), una [struttura](../../../csharp/language-reference/keywords/struct.md) o un'[interfaccia](../../../csharp/language-reference/keywords/interface.md) accessibile dalle applicazioni client, come una matrice.  Gli indicizzatori sono in genere implementati in tipi il cui scopo principale consiste nell'incapsulare una raccolta o una matrice interna.  Ad esempio, si supponga di disporre di una classe denominata TempRecord che rappresenta la temperatura in Farenheit registrata 10 volte nell'arco di 24 ore.  La classe contiene una matrice denominata "temps" di tipo float per rappresentare le temperature e un oggetto <xref:System.DateTime> che rappresenta la data in cui sono state registrate le temperature.  L'implementazione di un indicizzatore in questa classe consente ai client di accedere alle temperature in un'istanza di TempRecord come `float temp = tr[4]` anziché come `float temp = tr.temps[4]`.  La notazione dell'indicizzatore non solo semplifica la sintassi per le applicazioni client, ma rende anche la classe e il relativo scopo più facilmente comprensibili ad altri sviluppatori.  
  
 Per dichiarare un indicizzatore su una classe o una struttura, utilizzare la parola chiave [this](../../../csharp/language-reference/keywords/this.md), come illustrato nell'esempio seguente:  
  
```  
public int this[int index]    // Indexer declaration  
{  
    // get and set accessors  
}  
  
```  
  
## Note  
 Il tipo di un indicizzatore e il tipo dei relativi parametri devono avere almeno lo stesso livello di accessibilità dell'indicizzatore.  Per ulteriori informazioni sui livelli di accessibilità, vedere [Modificatori di accesso](../../../csharp/language-reference/keywords/access-modifiers.md).  
  
 Per ulteriori informazioni sull'utilizzo degli indicizzatori con un'interfaccia, vedere [Indicizzatori di interfaccia](../../../csharp/programming-guide/indexers/indexers-in-interfaces.md).  
  
 La firma di un indicizzatore è costituita dal numero e dai tipi dei parametri formali.  Non include il tipo dell'indicizzatore né i nomi dei parametri formali.  Se vengono dichiarati più indicizzatori nella stessa classe, questi devono avere firme diverse.  
  
 Il valore di un indicizzatore non è classificato come variabile, pertanto non è possibile passarlo come parametro [ref](../../../csharp/language-reference/keywords/ref.md) o [out](../../../csharp/language-reference/keywords/out.md).  
  
 Per fornire all'indicizzatore un nome utilizzabile in altri linguaggi, è necessario specificare un attributo `name` nella dichiarazione.  Di seguito è riportato un esempio:  
  
```  
[System.Runtime.CompilerServices.IndexerName("TheItem")]  
public int this [int index]   // Indexer declaration  
{  
}  
```  
  
 Questo indicizzatore avrà il nome `TheItem`.  Se non si specifica l'attributo name, all'indicizzatore `Item` verrà assegnato il nome predefinito.  
  
## Esempio 1  
  
### Descrizione  
 Nell'esempio che segue viene illustrata la dichiarazione di un campo di matrice privato, `temps`, e di un indicizzatore.  L'indicizzatore consente l'accesso diretto all'istanza `tempRecord[i]`.  In alternativa, anziché utilizzare l'indicizzatore è possibile dichiarare la matrice come membro [public](../../../csharp/language-reference/keywords/public.md) ed accedere direttamente ai relativi membri `tempRecord.temps[i]`.  
  
 Si noti che, quando viene valutato l'accesso di un indicizzatore, ad esempio in un'istruzione `Console.Write`, viene richiamata la funzione di accesso [get](../../../csharp/language-reference/keywords/get.md).  Di conseguenza, se non esiste alcuna funzione di accesso `get`, si verificherà un errore in fase di compilazione.  
  
### Codice  
 [!code-cs[csProgGuideIndexers#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-indexers_1.cs)]  
  
## Indicizzazione mediante altri valori  
 In C\# non è necessario utilizzare un indice di tipo integer.  Ad esempio, può essere utile assegnare a un indicizzatore un valore stringa.  Un indicizzatore di questo tipo può essere implementato effettuando una ricerca della stringa all'interno della raccolta e restituendo il valore appropriato.  Poiché le funzioni di accesso possono essere sottoposte a overload, le versioni basate su valore stringa e integer possono coesistere.  
  
## Esempio 2  
  
### Descrizione  
 In questo esempio viene dichiarata una classe in cui sono archiviati i giorni della settimana.  Viene quindi dichiarata una funzione di accesso `get` che accetta una stringa e il nome del giorno e restituisce l'intero corrispondente.  Ad esempio, Sunday restituirà 0, Monday restituirà 1 e così via.  
  
### Codice  
 [!code-cs[csProgGuideIndexers#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-indexers_2.cs)]  
  
## Programmazione robusta  
 Di seguito sono indicate le due tecniche principali che consentono di migliorare la sicurezza e l'affidabilità degli indicizzatori.  
  
-   Assicurarsi di incorporare una strategia di gestione degli errori per gestire l'eventualità che nel codice client venga passato un valore di indice non valido.  Nel primo esempio riportato in precedenza in questo argomento, la classe TempRecord fornisce una proprietà Length che consente al codice client di verificare l'input prima di passarlo all'indicizzatore.  È anche possibile inserire il codice di gestione degli errori nell'indicizzatore stesso.  Assicurarsi di documentare per gli utenti eventuali eccezioni generate all'interno di una funzione di accesso dell'indicizzatore.  
  
-   Impostare il livello di accessibilità delle funzioni di accesso `get` e [set](../../../csharp/language-reference/keywords/set.md) in modo abbastanza restrittivo.  Questo aspetto è importante soprattutto per la funzione di accesso `set`.  Per ulteriori informazioni, vedere [Limitazione dell'accessibilità delle funzioni di accesso](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)