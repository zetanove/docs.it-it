---
title: Durata in Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- static variables, lifetime
- static variables, Visual Basic
- declared elements, lifetime
- Shared variable lifetime
- lifetime, declared elements
- lifetime, Visual Basic
- lifetime
ms.assetid: bd91e390-690a-469a-9946-8dca70bc14e7
caps.latest.revision: 14
author: stevehoag
ms.author: shoag
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: fa0cbdf4a8fe5e8fc41e4e4f373c79451fb7b75f
ms.lasthandoff: 03/13/2017

---
# <a name="lifetime-in-visual-basic"></a>Durata in Visual Basic
Il *durata* di un elemento dichiarato è il periodo di tempo durante il quale essa è disponibile per l'utilizzo. Le variabili sono gli unici elementi che hanno una durata. A questo scopo, il compilatore considera i parametri delle procedure e funzione restituisce come casi speciali di variabili. La durata di una variabile rappresenta il periodo di tempo durante i quali può contenere un valore. Tale valore può cambiare nel corso della durata, ma contiene sempre un valore.  
  
## <a name="different-lifetimes"></a>Durata diversa  
 Oggetto *variabile membro* (dichiarato a livello di modulo, all'esterno di qualsiasi routine) ha in genere la stessa durata dell'elemento in cui è dichiarata. Una variabile non condivisa dichiarata in una classe o struttura esiste come una copia separata per ogni istanza della classe o struttura in cui è dichiarata. Ognuna di queste variabili ha la stessa durata della relativa istanza. Tuttavia, un `Shared` variabile ha un'unica durata, la durata di esecuzione dell'applicazione.  
  
 Oggetto *variabile locale* (dichiarato all'interno di una routine) esiste solo durante l'esecuzione della routine in cui è dichiarata. Questo vale anche per i parametri della routine e a qualsiasi funzione restituito. Tuttavia, se tale routine chiama altre procedure, le variabili locali mantengono i propri valori durante l'esecuzione delle routine chiamate.  
  
## <a name="beginning-of-lifetime"></a>Inizio della durata  
 La durata di una variabile locale inizia quando il controllo entra la procedura in cui è dichiarata. Ogni variabile locale viene inizializzata sul valore predefinito per il tipo di dati non appena inizia la procedura in esecuzione. Quando la procedura rileva un `Dim` istruzione che specifica i valori iniziali, imposta le variabili su tali valori, anche se il codice aveva già assegnato altri valori.  
  
 Ogni membro di una variabile di struttura viene inizializzato come se fosse una variabile separata. Analogamente, ogni elemento di una variabile di matrice viene inizializzato singolarmente.  
  
 Le variabili dichiarate all'interno di un blocco all'interno di una routine (ad esempio un `For` ciclo) vengono inizializzati alla routine. Queste inizializzazioni effettive verrà mai eseguito il blocco o meno.  
  
## <a name="end-of-lifetime"></a>Fine del ciclo di vita  
 Al termine di una routine, i valori delle variabili locali non vengono conservati e [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] recupera la memoria. Al successivo che si chiama la routine, tutte le variabili locali vengono ricreate e reinizializzate.  
  
 Al termine di un'istanza di una classe o struttura, le variabili non perdono la memoria e i relativi valori. Ogni nuova istanza della classe o struttura crea e reinizializza le variabili non condivise. Tuttavia, `Shared` le variabili vengono mantenute fino a quando l'esecuzione dell'applicazione.  
  
## <a name="extension-of-lifetime"></a>Estensione della durata  
 Se si dichiara una variabile locale con il `Static` (parola chiave), la sua durata è maggiore rispetto al tempo di esecuzione della relativa routine. Nella tabella seguente viene illustrato come la dichiarazione della routine determina per quanto tempo un `Static` variabile esista.  
  
|Posizione della routine e condivisione|Inizio della durata della variabile statica|Fine della durata della variabile statica|  
|------------------------------------|-------------------------------------|-----------------------------------|  
|In un modulo (condiviso per impostazione predefinita)|La prima volta che viene chiamata la routine|Al termine dell'esecuzione dell'applicazione|  
|In una classe, `Shared` (procedura non è un membro di istanza)|La prima volta la procedura viene chiamata su un'istanza specifica o al nome di classe o struttura stessa|Al termine dell'esecuzione dell'applicazione|  
|In un'istanza di una classe, non `Shared` (la routine è un membro di istanza)|La prima volta la routine viene chiamata sull'istanza specifica|Quando l'istanza viene rilasciata per la garbage collection (GC)|  
  
## <a name="static-variables-of-the-same-name"></a>Variabili statiche con lo stesso nome  
 È possibile dichiarare le variabili statiche con lo stesso nome in più di una procedura. In tal caso, il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore considera ognuna di queste variabili per un elemento distinto. L'inizializzazione di una di queste variabili non influenza i valori degli altri. Lo stesso vale se si definisce una routine con un set di overload e dichiara una variabile statica con lo stesso nome in ogni overload.  
  
## <a name="containing-elements-for-static-variables"></a>Contenente gli elementi per le variabili statiche  
 È possibile dichiarare una variabile locale statica all'interno di una classe, vale a dire all'interno di una routine in tale classe. Tuttavia, è possibile dichiarare una variabile locale statica all'interno di una struttura, come un membro della struttura o come una variabile locale di una procedura all'interno di tale struttura.  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente viene dichiarata una variabile con il [statico](../../../../visual-basic/language-reference/modifiers/static.md) (parola chiave). (Si noti che non è necessario il `Dim` (parola chiave) quando il [Dim (istruzione)](../../../../visual-basic/language-reference/statements/dim-statement.md) utilizza un modificatore, ad esempio `Static`.)  
  
### <a name="code"></a>Codice  
 [!code-vb[13 VbVbalrKeywords](../../../../visual-basic/language-reference/codesnippet/VisualBasic/lifetime_1.vb)]  
  
### <a name="comments"></a>Commenti  
 Nell'esempio precedente, la variabile `applesSold` continua a esistere dopo la procedura `runningTotal` restituisce al codice chiamante. La volta successiva che `runningTotal` viene chiamato, `applesSold` mantiene il valore calcolato in precedenza.  
  
 Se `applesSold` fosse stato dichiarato senza l'utilizzo di `Static`, i valori precedentemente accumulati non verranno conservati tra le chiamate a `runningTotal`. La volta successiva che `runningTotal` è stato chiamato, `applesSold` verrà ricreata e inizializzata su 0, e `runningTotal` restituirà semplicemente lo stesso valore con cui è stato chiamato.  
  
### <a name="compiling-the-code"></a>Compilazione del codice  
 È possibile inizializzare il valore di una variabile locale statica come parte della relativa dichiarazione. Se si dichiara una matrice come `Static`, è possibile inizializzare il rango (numero di dimensioni), la lunghezza di ogni dimensione e i valori dei singoli elementi.  
  
### <a name="security"></a>Sicurezza  
 Nell'esempio precedente, è possibile ottenere la stessa durata dichiarando `applesSold` a livello di modulo. Se si modifica l'ambito di una variabile in questo modo, tuttavia, la procedura non avrebbe accesso esclusivo a essa. Poiché in grado di accedere ad altre procedure `applesSold` e modificarne il valore, il totale parziale potrebbe non essere affidabile e il codice potrebbe essere più difficile da gestire.  
  
## <a name="see-also"></a>Vedere anche  
 [Condiviso](../../../../visual-basic/language-reference/modifiers/shared.md)   
 [Nothing](../../../../visual-basic/language-reference/nothing.md)   
 [Nomi elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Riferimenti a elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Ambito in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [Livelli di accesso in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Variabili](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [Dichiarazione di variabile](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Risoluzione dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Static](../../../../visual-basic/language-reference/modifiers/static.md)
