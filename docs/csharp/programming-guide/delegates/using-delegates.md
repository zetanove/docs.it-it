---
title: "Utilizzo di delegati (Guida per programmatori C#) | Microsoft Docs"
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
  - "delegati [C#], modalità di utilizzo"
ms.assetid: 99a2fc27-a32e-4a34-921c-e65497520eec
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Utilizzo di delegati (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un [delegato](../../../csharp/language-reference/keywords/delegate.md) è un tipo che incapsula in modo sicuro un metodo, simile a un puntatore a funzione in C e C\+\+.  A differenza dei puntatori a funzione, tuttavia, i delegati sono orientati a oggetti, indipendenti dai tipi e sicuri.  Il tipo delegato è definito dal nome del delegato.  Nell'esempio seguente viene dichiarato un delegato denominato `Del` che può incapsulare un metodo che accetta una [stringa](../../../csharp/language-reference/keywords/string.md) come argomento e restituisce [void](../../../csharp/language-reference/keywords/void.md):  
  
 [!code-cs[csProgGuideDelegates#21](../../../csharp/programming-guide/delegates/codesnippet/CSharp/using-delegates_1.cs)]  
  
 Un oggetto delegato viene normalmente creato fornendo il nome del metodo di cui il delegato eseguirà il wrapping, o con un [metodo anonimo](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md).  Una volta che viene creata un'istanza di un delegato, una chiamata al metodo effettuata al delegato verrà passata dal delegato a tale metodo.  I parametri passati al delegato dal chiamante vengono passati al metodo e il valore restituito, se presente, dal metodo viene restituito al chiamante dal delegato.  Questa operazione è nota come richiamare il delegato.  È possibile richiamare un delegato per cui è stata creata un'istanza come se fosse il metodo di wrapping stesso.  Ad esempio:  
  
 [!code-cs[csProgGuideDelegates#22](../../../csharp/programming-guide/delegates/codesnippet/CSharp/using-delegates_2.cs)]  
  
 [!code-cs[csProgGuideDelegates#23](../../../csharp/programming-guide/delegates/codesnippet/CSharp/using-delegates_3.cs)]  
  
 Tipi delegati vengono derivati dalla classe <xref:System.Delegate> di.NET Framework.  I tipi delegati sono [sealed](../../../csharp/language-reference/keywords/sealed.md), ovvero non possono essere usati, e non è possibile derivare classi personalizzate da <xref:System.Delegate>.  Poiché l'istanza del delegato è un oggetto, può essere passata come parametro o assegnata a una proprietà.  In questo modo un metodo può accettare un delegato come parametro e chiamare il delegato in un secondo momento.  Questa operazione è nota come callback asincrono ed è un metodo comune per notificare un chiamante al termine di un processo lungo.  Quando un delegato viene usato in questo modo, per il codice che usa il delegato non è richiesta alcuna conoscenza dell'implementazione del metodo in uso.  La funzionalità è simile all'incapsulamento fornito dalle interfacce.  
  
 Un altro utilizzo comune dei callback è la definizione di un metodo di confronto personalizzato e il passaggio di tale delegato a un metodo di ordinamento.  Consente al codice del chiamante di entrare a far parte dell'algoritmo di ordinamento.  Nell'esempio di metodo seguente viene usato il tipo `Del` come parametro:  
  
 [!code-cs[csProgGuideDelegates#24](../../../csharp/programming-guide/delegates/codesnippet/CSharp/using-delegates_4.cs)]  
  
 È quindi possibile passare il delegato creato in precedenza a tale metodo:  
  
 [!code-cs[csProgGuideDelegates#25](../../../csharp/programming-guide/delegates/codesnippet/CSharp/using-delegates_5.cs)]  
  
 e visualizzare il seguente output sulla console:  
  
 `The number is: 3`  
  
 Usando il delegato come astrazione, non è necessario chiamare direttamente la console da `MethodWithCallback`, ovvero questo non deve essere progettato tenendo presente una console.  `MethodWithCallback` si limita a preparare una stringa e a passarla a un altro metodo.  Questa operazione è particolarmente efficace perché un metodo delegato può usare qualsiasi numero di parametri.  
  
 Quando viene creato un delegato per eseguire il wrapping di un metodo di istanza, il delegato fa riferimento sia all'istanza sia al metodo.  Un delegato non ha alcuna conoscenza del tipo di istanza a parte il metodo di cui esegue il wrapping, perciò un delegato può fare riferimento a qualsiasi tipo di oggetto a condizione che vi sia un metodo su tale oggetto che corrisponda alla firma del delegato.  Quando viene creato un delegato per eseguire il wrapping di un metodo statico, fa riferimento solo al metodo.  Si considerino le dichiarazioni seguenti:  
  
 [!code-cs[csProgGuideDelegates#26](../../../csharp/programming-guide/delegates/codesnippet/CSharp/using-delegates_6.cs)]  
  
 Insieme al metodo statico `DelegateMethod` illustrato in precedenza, ci sono tre metodi di cui è possibile eseguire il wrapping in un'istanza di `Del`.  
  
 Un delegato può chiamare più di un metodo, quando viene richiamato.  Questo processo viene definito multicasting.  Per aggiungere un ulteriore metodo all'elenco dei metodi del delegato \(l'elenco chiamate\), è necessario semplicemente aggiungere due delegati usando gli operatori addizione o di assegnazione di addizione \("\+" o "\+\="\).  Ad esempio:  
  
 [!code-cs[csProgGuideDelegates#27](../../../csharp/programming-guide/delegates/codesnippet/CSharp/using-delegates_7.cs)]  
  
 A questo punto `allMethodsDelegate` contiene tre metodi nel relativo elenco chiamate: `Method1`, `Method2` e `DelegateMethod`.  I tre delegati originali, `d1`, `d2` e `d3`, rimangono invariati.  Quando si richiama `allMethodsDelegate`, tutti e tre i metodi vengono chiamati nell'ordine.  Se il delegato usa parametri di riferimento, il riferimento viene passato in sequenza a ciascuno dei tre metodi a turno e le eventuali modifiche apportate da un solo metodo saranno visibili al metodo successivo.  Quando uno dei metodi genera un'eccezione non rilevata all'interno del metodo, tale eccezione viene passata al chiamante del delegato e non verrà chiamato nessun metodo successivo nell'elenco chiamate.  Se il delegato ha un valore restituito e\/o i parametri out, restituisce il valore restituito e i parametri dell'ultimo metodo richiamato.  Per rimuovere un metodo dall'elenco chiamate, usare l'operatore di decremento o l'operatore di decremento di assegnazione \("\-" o "\-\="'\).  Ad esempio:  
  
 [!code-cs[csProgGuideDelegates#28](../../../csharp/programming-guide/delegates/codesnippet/CSharp/using-delegates_8.cs)]  
  
 Poiché i tipi delegati vengono derivati da `System.Delegate`, i metodi e le proprietà definiti da tale classe possono essere chiamati sul delegato.  Ad esempio, per trovare il numero di metodi nell'elenco chiamate di un delegato, è possibile scrivere:  
  
 [!code-cs[csProgGuideDelegates#29](../../../csharp/programming-guide/delegates/codesnippet/CSharp/using-delegates_9.cs)]  
  
 I delegati con più metodi nel relativo elenco chiamate derivano da <xref:System.MulticastDelegate>, cioè una sottoclasse di `System.Delegate`.  Il codice sopra riportato funziona in entrambi i casi, perché entrambe le classi supportano `GetInvocationList`.  
  
 I delegati multicast vengono ampiamente usati nella gestione degli eventi.  Gli oggetti di origine evento inviano notifiche di eventi agli oggetti destinatario registrati per ricevere l'evento.  Per registrarsi a un evento, il destinatario crea un metodo che può gestire l'evento, quindi crea un delegato per il metodo e passa il delegato all'origine evento.  L'origine chiama il delegato quando si verifica l'evento.  Il delegato chiama quindi il metodo di gestione eventi sul destinatario, recapitando i dati dell'evento.  Il tipo delegato per un determinato evento è definito dall'origine evento.  Per altre informazioni, vedere [Eventi](../../../csharp/programming-guide/events/index.md).  
  
 Se si confrontano delegati di due tipi diversi assegnati in fase di compilazione si avrà un errore di compilazione.  Se le istanze dei delegati sono staticamente del tipo `System.Delegate`, il confronto è consentito, ma restituirà false in fase di esecuzione.  Ad esempio:  
  
 [!code-cs[csProgGuideDelegates#30](../../../csharp/programming-guide/delegates/codesnippet/CSharp/using-delegates_10.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Utilizzo della varianza nei delegati](../Topic/Using%20Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)   
 [Varianza nei delegati](../Topic/Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)   
 [Utilizzo della varianza per i delegati generici Func e Action](../Topic/Using%20Variance%20for%20Func%20and%20Action%20Generic%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)