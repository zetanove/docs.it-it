---
title: "Campi (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "campi [C#]"
ms.assetid: 3cbb2f61-75f8-4cce-b4ef-f5d1b3de0db7
caps.latest.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 29
---
# Campi (Guida per programmatori C#)
Un *campo* è una variabile di qualsiasi tipo dichiarata direttamente in una [classe](../../../csharp/language-reference/keywords/class.md) o in una [struttura](../../../csharp/language-reference/keywords/struct.md).  I campi sono *membri* del rispettivo tipo contenitore.  
  
 Una classe o una struttura possono includere campi di istanza, campi statici o entrambi.  I campi di istanza sono specifici di un'istanza di un tipo.  Se si ha una classe T che include un campo di istanza F, è possibile creare due oggetti di tipo T e modificare il valore di F in ciascun oggetto senza influenzare il valore nell'altro oggetto.  Al contrario, un campo statico appartiene alla classe stessa e viene condiviso fra tutte le istanze di quella classe.  Le modifiche effettuate dall’istanza A saranno immediatamente visibili sulle istanze B e C, se queste accedono al campo.  
  
 Generalmente, i campi devono essere utilizzati solo per variabili con accesso privato o protetto.  I dati che la classe espone al codice client devono essere forniti tramite [metodi](../../../csharp/programming-guide/classes-and-structs/methods.md), [proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md) e [indicizzatori](../../../csharp/programming-guide/indexers/index.md).  Utilizzando questi costrutti per l’accesso indiretto ai campi interni, è possibile implementare una protezione contro il passaggio di valori di input non validi.  Un campo privato che archivia i dati esposti da una proprietà pubblica viene denominato *archivio di backup* o *campo sottostante*.  
  
 Generalmente, i campi archiviano dati che devono essere accessibili a più metodi della classe e che devono essere archiviati per periodi di tempo più lunghi della durata di qualsiasi metodo singolo.  Ad esempio, una classe che rappresenta una data di calendario potrebbe contenere tre campi integer: uno per il mese, uno per il giorno e uno per l'anno.  Le variabili che non vengono utilizzate fuori dall'ambito di un singolo metodo devono essere dichiarate come *variabili locali* all'interno del corpo del metodo stesso.  
  
 I campi vengono dichiarati all'interno del blocco della classe specificando il livello di accesso, quindi il tipo e infine il nome del campo.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideObjects#61](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/fields_1.cs)]  
  
 Per accedere a un campo di un oggetto, aggiungere un punto dopo il nome dell'oggetto, seguito dal nome del campo, come in `objectname.fieldname`.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideObjects#62](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/fields_2.cs)]  
  
 A un campo è possibile assegnare un valore iniziale nella relativa dichiarazione utilizzando l'operatore di assegnazione.  Per assegnare automaticamente il campo `day` a `"Monday"`, ad esempio, dichiarare `day` come indicato nell'esempio seguente:  
  
 [!code-cs[csProgGuideObjects#63](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/fields_3.cs)]  
  
 I campi vengono inizializzati immediatamente prima della chiamata al costruttore per l'istanza dell'oggetto.  Se il costruttore assegna il valore di un campo, verrà sovrascritto qualunque valore specificato nella dichiarazione del campo.  Per ulteriori informazioni, vedere [Utilizzo di costruttori](../../../csharp/programming-guide/classes-and-structs/using-constructors.md).  
  
> [!NOTE]
>  Un inizializzatore di campo non può fare riferimento ad altri campi di istanza.  
  
 I campi possono essere contrassegnati come [public](../../../csharp/language-reference/keywords/public.md), [private](../../../csharp/language-reference/keywords/private.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md) o `protected internal`.  Questi modificatori definiscono le modalità di accesso ai campi per gli utenti della classe.  Per ulteriori informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
 È possibile dichiarare un campo come [static](../../../csharp/language-reference/keywords/static.md).  In questo modo il campo risulterà sempre disponibile per i chiamanti, anche se non esistono istanze della classe.  Per ulteriori informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 È possibile dichiarare un campo come [readonly](../../../csharp/language-reference/keywords/readonly.md).  È possibile assegnare un valore a un campo in sola lettura solo durante l'inizializzazione oppure in un costruttore.  Un campo `static` `readonly` è molto simile a una costante, con la differenza che il compilatore C\# non ha accesso al valore di un campo di questo tipo in fase di compilazione, ma solo in fase di esecuzione.  Per ulteriori informazioni, vedere [Costanti](../../../csharp/programming-guide/classes-and-structs/constants.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Utilizzo di costruttori](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)