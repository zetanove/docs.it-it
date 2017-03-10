---
title: "Costanti (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, costanti"
  - "costanti [C#]"
ms.assetid: 1fb39621-1738-49b1-a1b3-8587f109123f
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# Costanti (Guida per programmatori C#)
Le costanti sono valori immutabili noti in fase di compilazione e non modificati per l’intera vita del programma.  Le costanti vengono dichiarate con il modificatore [const](../../../csharp/language-reference/keywords/const.md).  Solo i tipi incorporati in C\# \( <xref:System.Object?displayProperty=fullName>\) possono essere dichiarati come `const`.  Per un elenco dei tipi incorporati, vedere [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md).  I tipi definiti dall'utente, fra cui classi, strutture e matrici, non possono essere `const`.  Utilizzare il modificatore [readonly](../../../csharp/language-reference/keywords/readonly.md)per creare una classe, una matrice o uno struct inizializzato una sola volta in fase di esecuzione \(ad esempio in un costruttore\) e non modificabile successivamente.  
  
 In C\# non sono supportati metodi, proprietà o eventi `const`.  
  
 Il tipo enum consente di definire costanti denominate dei tipi incorporati interi \(ad esempio `int`, `uint`, `long`e così via\).  Per ulteriori informazioni, vedere [enum](../../../csharp/language-reference/keywords/enum.md).  
  
 Le costanti devono essere inizializzate al momento stesso della dichiarazione.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideObjects#64](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/constants_1.cs)]  
  
 In questo esempio, la costante `months` sarà sempre 12 e non potrà essere modificata, nemmeno dalla classe stessa.  In realtà, quando il compilatore incontra un identificatore costante nel codice sorgente C\# \(ad esempio, `months`\), lo sostituisce con il relativo valore letterale direttamente nel codice Microsoft Intermediate Language \(IL\) che produce.  Poiché non esiste alcun indirizzo di variabile associato con una costante in fase di esecuzione, i campi `const` non possono essere passati per riferimento e non possono sostituire un valore l\-value in un'espressione.  
  
> [!NOTE]
>  Porre attenzione nel fare riferimento a valori costanti definiti in altro codice, come ad esempio DLL.  Se una nuova versione della DLL definisce un nuovo valore per la costante, il programma manterrà ancora il vecchio valore letterale finché non verrà ricompilato con riferimento alla nuova versione.  
  
 È possibile dichiarare contemporaneamente più costanti dello stesso tipo. Esempio:  
  
 [!code-cs[csProgGuideObjects#65](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/constants_2.cs)]  
  
 L'espressione utilizzata per inizializzare una costante può fare riferimento a un'altra costante, purché non venga creato un riferimento circolare.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideObjects#66](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/constants_3.cs)]  
  
 Le costanti possono essere contrassegnate come [public](../../../csharp/language-reference/keywords/public.md), [private](../../../csharp/language-reference/keywords/private.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md) o `protected` `internal`.  Questi modificatori definiscono le modalità di accesso alla costante per gli utenti della classe.  Per ulteriori informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
 L’accesso alle costanti avviene come se fossero campi [statici](../../../csharp/language-reference/keywords/static.md), perché il valore della costante è lo stesso per tutte le istanze del tipo.  Non viene utilizzata la parola chiave `static` per dichiararle.  Nelle espressioni non contenute nella classe in cui è definita una costante, per accedere a quest'ultima è necessario utilizzare il nome della classe, seguito da un punto e dal nome della costante stessa.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideObjects#67](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/constants_4.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Tipi](../../../csharp/programming-guide/types/index.md)   
 [readonly](../../../csharp/language-reference/keywords/readonly.md)   
 [Immutabilità nella parte uno di C\#: tipi di immutabilità](http://go.microsoft.com/fwlink/?LinkId=112379)