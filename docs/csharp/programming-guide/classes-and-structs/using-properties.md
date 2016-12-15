---
title: "Utilizzo delle propriet&#224; (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "get (funzione di accesso) [C#]"
  - "proprietà [C#], informazioni sulle proprietà"
  - "set (funzione di accesso) [C#]"
ms.assetid: f7f67b05-0983-4cdb-96af-1855d24c967c
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Utilizzo delle propriet&#224; (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nelle proprietà vengono combinati alcuni aspetti dei campi e dei metodi.  Dal punto di vista dell'utente di un oggetto, una proprietà è un campo e l'accesso alla proprietà richiede esattamente la stessa sintassi.  Dal punto di vista del responsabile dell'implementazione di una classe, una proprietà è costituita da uno o due blocchi di codice che rappresentano una funzione di accesso [get](../../../csharp/language-reference/keywords/get.md) e\/o [set](../../../csharp/language-reference/keywords/set.md).  Il blocco di codice relativo alla funzione di accesso `get` viene eseguito quando la proprietà viene letta, mentre il blocco di codice relativo alla funzione di accesso `set` viene eseguito quando viene assegnato un nuovo valore alla proprietà.  Una proprietà in cui non è definita la funzione di accesso `set` è considerata in sola lettura.  Una proprietà in cui non è definita la funzione di accesso `get` è considerata in sola scrittura.  Una proprietà con entrambe le funzioni di accesso è considerata di lettura\/scrittura.  
  
 Al contrario dei campi, le proprietà non sono classificate come variabili.  Pertanto, non è possibile passare una proprietà come parametro [ref](../../../csharp/language-reference/keywords/ref.md) o [out](../../../csharp/language-reference/keywords/out.md).  
  
 Le proprietà possono essere utilizzate per diversi scopi, ad esempio per convalidare i dati prima di consentire una modifica, per esporre in modo trasparente i dati in una classe in cui tali dati vengono in realtà recuperati da un'altra origine, ad esempio un database, per eseguire un'azione in caso di modifica dei dati, ad esempio la generazione di un evento, o per modificare il valore di altri campi.  
  
 Le proprietà vengono dichiarate all'interno del blocco della classe specificando il livello di accesso del campo, seguito dal tipo e dal nome della proprietà e da un blocco di codice in cui sono dichiarate le funzioni di accesso `get` e\/o `set`.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideProperties#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_1.cs)]  
  
 In questo esempio `Month` viene dichiarato come proprietà in modo che la funzione di accesso `set` possa assicurare che il valore `Month` sia impostato tra 1 e 12.  La proprietà `Month` utilizza un campo privato per tenere traccia del valore effettivo.  La posizione reale dei dati di una proprietà è spesso indicata con il termine "archivio di backup" della proprietà. In genere, le proprietà utilizzano campi privati come archivio di backup.  L'utilizzo dei campi privati assicura che il campo possa essere modificato soltanto chiamando la proprietà.  Per ulteriori informazioni sulle restrizioni per l'accesso pubblico e privato, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
 Le proprietà implementate automaticamente forniscono sintassi semplificata per le dichiarazioni di proprietà semplici.  Per ulteriori informazioni, vedere [Proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md).  
  
## Funzione di accesso get  
 Il corpo della funzione di accesso `get` è simile a quello di un metodo.  Tale funzione deve restituire un valore del tipo di proprietà.  L'esecuzione della funzione di accesso `get` equivale alla lettura del valore del campo.  Ad esempio, durante la restituzione della variabile privata dalla funzione di accesso `get`, se le ottimizzazioni sono attivate, la chiamata al metodo della funzione di accesso `get` viene resa inline dal compilatore, in modo da evitare un sovraccarico per la chiamata al metodo.  Tuttavia, un metodo virtuale della funzione di accesso `get` non può essere reso inline poiché il compilatore non conosce, in fase di compilazione, quale metodo può essere effettivamente chiamato in fase di esecuzione.  Di seguito è riportata una funzione di accesso `get` che restituisce il valore di un campo privato `name`:  
  
 [!code-cs[csProgGuideProperties#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_2.cs)]  
  
 Quando si fa riferimento alla proprietà, eccetto come destinazione di un'assegnazione, viene chiamata la funzione di accesso `get` per leggere il valore della proprietà.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideProperties#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_3.cs)]  
  
 La funzione di accesso `get` deve terminare con un'istruzione [return](../../../csharp/language-reference/keywords/return.md) o [throw](../../../csharp/language-reference/keywords/throw.md) e il controllo non può uscire dal corpo della funzione di accesso.  
  
 È preferibile evitare di cambiare lo stato dell'oggetto tramite la funzione di accesso `get`.  Ad esempio, la seguente funzione di accesso produce l'effetto collaterale di cambiare lo stato dell'oggetto ogni volta che si accede al campo `number`.  
  
 [!code-cs[csProgGuideProperties#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_4.cs)]  
  
 La funzione di accesso `get` può essere utilizzata per restituire il valore del campo oppure per calcolarlo e restituirlo.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideProperties#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_5.cs)]  
  
 Nel segmento di codice precedente, se non si assegna un valore alla proprietà `Name`, verrà restituito il valore NA.  
  
## Funzione di accesso set  
 La funzione di accesso `set` è simile a un metodo che restituisce un valore di tipo [void](../../../csharp/language-reference/keywords/void.md).  Utilizza un parametro implicito denominato `value`, il cui tipo corrisponde al tipo della proprietà.  Nell'esempio di codice riportato di seguito viene aggiunta una funzione di accesso `set` alla proprietà `Name`:  
  
 [!code-cs[csProgGuideProperties#12](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_6.cs)]  
  
 Quando si assegna un valore alla proprietà, la funzione di accesso `set` viene richiamata tramite un argomento che fornisce il nuovo valore.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideProperties#13](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_7.cs)]  
  
 Non è possibile utilizzare il nome del parametro implicito \(`value`\) per una dichiarazione di variabile locale in una funzione di accesso `set`.  
  
## Note  
 Le proprietà possono essere contrassegnate come `public`, `private`, `protected`, `internal` o `protected internal`.  Questi modificatori di accesso definiscono il modo in cui gli utenti della classe possono accedere alla proprietà.  Le funzioni di accesso `get` e `set` per la stessa proprietà possono avere modificatori di accesso differenti.  Ad esempio, la funzione di accesso `get` può essere `public` per consentire l'accesso in sola lettura dall'esterno del tipo, mentre la funzione di accesso `set` può essere `private` o `protected`.  Per ulteriori informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
 Una proprietà può essere dichiarata statica utilizzando la parola chiave `static`.  In questo modo la proprietà sarà sempre disponibile ai chiamanti, anche se non esiste alcuna istanza della classe.  Per ulteriori informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 Una proprietà può essere contrassegnata come virtuale utilizzando la parola chiave [virtual](../../../csharp/language-reference/keywords/virtual.md).  In questo modo le classi derivate possono eseguire l'override del comportamento della proprietà utilizzando la parola chiave [override](../../../csharp/language-reference/keywords/override.md).  Per ulteriori informazioni sulle opzioni, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md).  
  
 Una proprietà che esegue l'override di una proprietà virtuale può anche essere contrassegnata come [sealed](../../../csharp/language-reference/keywords/sealed.md), per indicare alle classi derivate che la proprietà non è più virtuale.  Infine, una proprietà può essere dichiarata [abstract](../../../csharp/language-reference/keywords/abstract.md).  Ciò significa che non vi è implementazione nella classe e che le classi derivate devono scrivere la propria implementazione.  Per ulteriori informazioni sulle opzioni, vedere [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
> [!NOTE]
>  Non è possibile utilizzare un modificatore [virtuale](../../../csharp/language-reference/keywords/virtual.md), [abstract](../../../csharp/language-reference/keywords/abstract.md) o [override](../../../csharp/language-reference/keywords/override.md) su una funzione di accesso di una proprietà [statica](../../../csharp/language-reference/keywords/static.md).  
  
## Esempio  
 Nell'esempio seguente vengono illustrate le proprietà di istanza, static e in sola lettura.  Viene inoltre accettato l'inserimento del nome del dipendente \(employee\) dalla tastiera, incrementato `NumberOfEmployees` di 1, quindi vengono visualizzati il nome e il numero del dipendente.  
  
 [!code-cs[csProgGuideProperties#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_8.cs)]  
  
## Esempio  
 In questo esempio viene illustrato come accedere a una proprietà in una classe base nascosta da un'altra proprietà con lo stesso nome in una classe derivata.  
  
 [!code-cs[csProgGuideProperties#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_9.cs)]  
  
 Di seguito sono indicati alcuni aspetti importanti dell'esempio precedente.  
  
-   La proprietà `Name` nella classe derivata nasconde la proprietà `Name` nella classe base.  In questo caso, il modificatore `new` viene utilizzato nella dichiarazione della proprietà nella classe derivata:  
  
     [!code-cs[csProgGuideProperties#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_10.cs)]  
  
-   Il cast `(Employee)` è utilizzato per accedere alla proprietà nascosta nella classe base:  
  
     [!code-cs[csProgGuideProperties#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_11.cs)]  
  
     Per ulteriori informazioni su come nascondere i membri, vedere [Modificatore new](../../../csharp/language-reference/keywords/new-modifier.md).  
  
## Esempio  
 Nell'esempio che segue le due classi `Cube` e `Square` implementano una classe astratta `Shape` ed eseguono l'override della proprietà astratta `Area`.  Si noti l'uso del modificatore [override](../../../csharp/language-reference/keywords/override.md) nelle proprietà.  Il programma accetta il membro side come un input e calcola le aree del quadrato e del cubo.  Inoltre, accetta l'area come un input e calcola il membro side corrispondente per il quadrato e il cubo.  
  
 [!code-cs[csProgGuideProperties#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_12.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Proprietà dell'interfaccia](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)   
 [Proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)