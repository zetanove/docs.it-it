---
title: "Classi generiche (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, classi generiche"
  - "generics [C#], classi"
ms.assetid: 27d6f256-cd61-41e3-bc6e-b990a53b0224
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# Classi generiche (Guida per programmatori C#)
Le classi generiche incapsulano operazioni non specifiche di un particolare tipo di dati.  Le classi generiche vengono comunemente utilizzate con le raccolte quali elenchi collegati, tabelle hash, stack, code, strutture ad albero e così via.  Le operazioni come l'aggiunta e la rimozione di elementi dalla raccolta vengono eseguite fondamentalmente in modo analogo, indipendentemente dal tipo di dati archiviati.  
  
 Per la maggior parte degli scenari in cui sono necessarie classi di raccolte, è consigliabile utilizzare quelle fornite nella libreria di classi .NET Framework.  Per ulteriori informazioni sull'utilizzo di queste classi, vedere [Generics nella libreria di classi .NET Framework](../../../csharp/programming-guide/generics/generics-in-the-net-framework-class-library.md).  
  
 Le classi generiche vengono in genere create a partire da una classe concreta esistente e modificando uno alla volta i tipi nei parametri di tipo fino a raggiungere l'equilibrio ottimale tra generalizzazione e possibilità di utilizzo.  Quando si creano classi generiche personalizzate, è importante valutare:  
  
-   Quali sono i tipi da generalizzare in parametri di tipo.  
  
     Di norma, maggiore è il numero di tipi ai quali è possibile applicare parametri, maggiore sarà la flessibilità e la possibilità di riutilizzo del codice.  Tuttavia, un'eccessiva generalizzazione può creare un codice che presenta difficoltà di lettura e di comprensione per altri sviluppatori.  
  
-   Quali sono i vincoli, se presenti, da applicare ai parametri di tipo \(vedere [Vincoli sui parametri di tipo](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)\).  
  
     Una buona regola è applicare il massimo numero di vincoli possibili che consentano ancora di gestire i tipi che è necessario gestire.  Ad esempio, se la classe generica deve essere utilizzata esclusivamente con tipi riferimento, applicare il vincolo della classe.  In questo modo si impedirà l'utilizzo involontario della classe con tipi di valore, sarà possibile utilizzare l'operatore `as` su `T` e verificare la presenza di valori null.  
  
-   Se eseguire il factoring del comportamento generico in classi e sottoclassi base.  
  
     Poiché le classi generiche possono essere utilizzate come classi di base, in questo caso vengono applicate le stesse considerazioni di progettazione delle classi non generiche.  Vedere le regole sull'ereditarietà dalle classi generiche di base più avanti in questo argomento.  
  
-   Se implementare una o più interfacce generiche.  
  
     Ad esempio, se si sta progettando una classe che verrà utilizzata per creare elementi una raccolta basata su generics, potrebbe essere necessario implementare un'interfaccia come <xref:System.IComparable%601> in cui `T` rappresenta il tipo della classe.  
  
 Per un esempio di classe generica semplice, vedere [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md).  
  
 Le regole per i vincoli e per i parametri di tipo presentano numerose implicazioni per il comportamento delle classi generiche, soprattutto per quanto riguarda l'ereditarietà e l'accessibilità ai membri.  Prima di procedere, è necessario comprendere alcuni termini.  Per una classe generica il codice client `Node<T>,` può fare riferimento alla classe specificando un argomento di tipo, per creare un tipo costruito chiuso \(`Node<int>`\)  oppure può mantenere il parametro di tipo non specificato, ad esempio quando viene specificata una classe generica di base, per creare un tipo costruito aperto \(`Node<T>`\).  Le classi generiche possono ereditare da classi base concrete, costruite chiuse o costruite aperte:  
  
 [!code-cs[csProgGuideGenerics#16](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-classes_1.cs)]  
  
 Le classi non generiche, ovvero concrete, possono ereditare da classi di base costruite chiuse, ma non da classi costruite aperte o da parametri di tipo poiché il codice client non è in grado di fornire l'argomento di tipo necessario per creare l'istanza della classe di base in fase di esecuzione.  
  
 [!code-cs[csProgGuideGenerics#17](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-classes_2.cs)]  
  
 Le classi generiche che ereditano da tipi costruiti aperti devono fornire argomenti di tipo per tutti i parametri di tipo delle classi base non condivisi dalla classe che eredita, come illustrato nel codice riportato di seguito:  
  
 [!code-cs[csProgGuideGenerics#18](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-classes_3.cs)]  
  
 Le classi generiche che ereditano da tipi costruiti aperti devono specificare i vincoli che rappresentano un superset dei vincoli del tipo base o che implicano gli stessi:  
  
 [!code-cs[csProgGuideGenerics#19](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-classes_4.cs)]  
  
 I tipi generici possono utilizzare più vincoli e parametri di tipo, come riportato di seguito:  
  
 [!code-cs[csProgGuideGenerics#20](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-classes_5.cs)]  
  
 I tipi costruiti aperti o costruiti chiusi possono essere utilizzati come parametri di metodo:  
  
 [!code-cs[csProgGuideGenerics#21](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-classes_6.cs)]  
  
 Se una classe generica implementa un'interfaccia, è possibile eseguire il cast di tutte le istanze della classe a tale interfaccia.  
  
 Le classi generiche sono invariabili.  In altre parole, se un parametro di input specifica `List<BaseClass>`, si verificherà un errore in fase di compilazione se si tenta di fornire `List<DerivedClass>`.  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Generics](../../../csharp/programming-guide/generics/index.md)   
 [Salvataggio dello stato degli enumeratori](http://go.microsoft.com/fwlink/?LinkId=112390)   
 [Puzzle relativo all'eredità, parte uno](http://go.microsoft.com/fwlink/?LinkId=112380)