---
title: "Lifetime in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "static variables, lifetime"
  - "static variables, Visual Basic"
  - "declared elements, lifetime"
  - "Shared variable lifetime"
  - "lifetime, declared elements"
  - "lifetime, Visual Basic"
  - "lifetime"
ms.assetid: bd91e390-690a-469a-9946-8dca70bc14e7
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Lifetime in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

La *durata* di un elemento dichiarato è il periodo di tempo durante il quale l'elemento è disponibile per l'utilizzo.  Le variabili sono gli unici elementi che hanno una durata.  Per questo motivo, i parametri delle routine e i valori restituiti dalle funzioni vengono considerati dal compilatore come casi speciali di variabili.  La durata di una variabile è il periodo di tempo durante il quale la variabile può contenere un valore.  Il valore può variare durante la durata della variabile, ma essa conterrà sempre un valore.  
  
## Diversità di durata  
 La durata di *variabile membro* \(dichiarata a livello di modulo, all'esterno di una qualsiasi routine\) in genere corrisponde alla durata dell'elemento in cui è dichiarata.  Una variabile non condivisa dichiarata in una classe o in una struttura esiste come copia separata per ogni istanza della classe o della struttura in cui è dichiarata.  La durata di ognuna di queste variabili corrisponde a quella della relativa istanza.  In ogni caso, una variabile `Shared` ha un'unica durata, uguale al tempo di esecuzione dell'applicazione.  
  
 Una *variabile locale* \(dichiarata all'interno di una routine\) esiste solo mentre è in esecuzione la routine in cui è dichiarata.  Questo vale anche per i parametri della routine e per qualsiasi valore restituito dalle funzioni.  In ogni caso, se la routine ne chiama altre, le variabili locali mantengono il proprio valore durante l'esecuzione delle routine chiamate.  
  
## Inizio di durata  
 La durata di una variabile locale inizia quando il controllo accede alla routine nella quale è dichiarata.  Non appena la routine inizia l'esecuzione, ogni variabile locale viene inizializzata sul valore predefinito del relativo tipo di dati.  Quando rileva un'istruzione `Dim` che definisce i valori iniziali, la routine imposta le variabili su tali valori, anche se il codice ha già assegnato alle variabili altri valori.  
  
 Ogni membro di una variabile di struttura viene inizializzato come se fosse una variabile distinta.  Analogamente, ogni elemento di una variabile di matrice viene inizializzato singolarmente.  
  
 Le variabili dichiarate in un blocco all'interno di una routine, ad esempio un ciclo `For`, vengono inizializzate al momento dell'accesso alla routine.  Queste inizializzazioni si verificano anche se il blocco non verrà mai eseguito.  
  
## Fine di durata  
 Al termine di una routine i valori delle variabili locali non vengono mantenuti e la memoria assegnata a tali variabili viene recuperata da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  Alla successiva chiamata della routine, tutte le variabili locali verranno ricreate e reinizializzate.  
  
 Quando un'istanza di una classe o di una struttura termina, la memoria viene recuperata e i valori delle relative variabili non condivise vengono persi.  Ogni nuova istanza della classe o della struttura crea e reinizializza le proprie variabili non condivise.  Le variabili `Shared`, tuttavia, vengono mantenute fino al termine dell'esecuzione dell'applicazione.  
  
## Estensione di durata  
 Se una variabile locale viene dichiarata con la parola chiave `Static`, la variabile avrà una durata maggiore rispetto al tempo di esecuzione della relativa routine.  Nella seguente tabella viene illustrata la relazione tra la dichiarazione della routine e la durata di una variabile `Static`.  
  
|Posizione della routine e modalità di condivisione|Inizio della durata della variabile statica|Fine della durata della variabile statica|  
|--------------------------------------------------------|-------------------------------------------------|-----------------------------------------------|  
|In un modulo \(condiviso per impostazione predefinita\)|La prima volta che la routine viene chiamata|Al termine dell'esecuzione dell'applicazione|  
|In una classe, `Shared` \(la routine non è un membro di istanza\)|La prima volta che la routine viene chiamata su un'istanza specifica o sul nome della classe o della struttura|Al termine dell'esecuzione dell'applicazione|  
|In un'istanza di una classe, non `Shared` \(la routine è un membro di istanza\)|La prima volta che la routine viene chiamata sull'istanza specifica|Quando l'istanza viene rilasciata per la Garbage Collection|  
  
## Variabili statiche con lo stesso nome  
 È possibile dichiarare variabili statiche con lo stesso nome in più routine.  In questo caso, il compilatore di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] considera ognuna di queste variabili come un elemento distinto.  L'inizializzazione di una di queste variabili non ha effetto sul valore delle altre.  Lo stesso avviene se si definisce una routine con un gruppo di overload e si dichiara una variabile statica con lo stesso nome in ogni overload.  
  
## Elementi contenitore per variabili statiche  
 È possibile dichiarare una variabile locale statica all'interno di una classe, ossia all'interno di una routine di tale classe.  Non è tuttavia possibile dichiarare una variabile locale statica all'interno di una struttura, né come membro della struttura né come variabile locale di una routine all'interno di tale struttura.  
  
## Esempio  
  
### Descrizione  
 Nell'esempio riportato di seguito viene dichiarata una variabile con la parola chiave [Static](../../../../visual-basic/language-reference/modifiers/static.md).  La parola chiave `Dim` non è necessaria quando l'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) utilizza un modificatore quale `Static`.  
  
### Codice  
 [!code-vb[VbVbalrKeywords#13](../../../../visual-basic/language-reference/codesnippet/visualbasic/lifetime_1.vb)]  
  
### Commenti  
 Nell'esempio precedente la variabile `applesSold` continuerà a esistere anche dopo che la routine `runningTotal` avrà restituito un valore al codice chiamante.  Alla successiva chiamata di `runningTotal`, `applesSold` conserverà il valore precedentemente calcolato.  
  
 Se `applesSold` è stata dichiarata senza utilizzare la parola chiave `Static`, i valori precedentemente accumulati non verranno conservati tra le varie chiamate a `runningTotal`.  Alla successiva chiamata a `runningTotal`, la variabile `applesSold` verrà ricreata e inizializzata su 0, mentre la routine `runningTotal` restituirà semplicemente lo stesso valore con cui era stata chiamata.  
  
### Compilazione del codice  
 È possibile inizializzare il valore di una variabile locale statica come parte della sua dichiarazione.  Se si dichiara una matrice come `Static`, è possibile inizializzarne il numero di dimensioni, la lunghezza di ogni dimensione e i valori dei singoli elementi.  
  
### Sicurezza  
 Nell'esempio precedente è possibile ottenere la stessa durata dichiarando `applesSold` a livello di modulo.  Tuttavia, se si modifica in questo modo l'ambito di una variabile, la routine non avrà più accesso esclusivo a tale variabile.  Poiché altre routine possono accedere a `applesSold` e modificarne il valore, il totale parziale potrebbe non essere affidabile e la manutenzione del codice potrebbe risultare più difficoltosa.  
  
## Vedere anche  
 [Shared](../../../../visual-basic/language-reference/modifiers/shared.md)   
 [Nothing](../../../../visual-basic/language-reference/nothing.md)   
 [Declared Element Names](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [Access Levels in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Variables](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Static](../../../../visual-basic/language-reference/modifiers/static.md)