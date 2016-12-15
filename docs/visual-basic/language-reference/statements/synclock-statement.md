---
title: "SyncLock Statement | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.SyncLock"
  - "SyncLock"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "threading [Visual Basic], locks"
  - "SyncLock statement"
  - "locks, threads"
ms.assetid: 14501703-298f-4d43-b139-c4b6366af176
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# SyncLock Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Acquisisce un blocco esclusivo per un blocco di istruzioni prima di eseguire quest'ultimo.  
  
## Sintassi  
  
```  
SyncLock lockobject  
    [ block ]  
End SyncLock  
```  
  
## Parti  
 `lockobject`  
 Necessario.  Espressione che restituisce un riferimento a un oggetto.  
  
 `block`  
 Opzionale.  Blocco di istruzioni da eseguire quando viene acquisito il blocco.  
  
 `End SyncLock`  
 Consente di terminare un blocco `SyncLock`.  
  
## Note  
 L'istruzione `SyncLock` garantisce che più thread non eseguano contemporaneamente il blocco di istruzioni.  `SyncLock` impedisce a ciascun thread di accedere al blocco durante l'esecuzione di quest'ultimo da parte di altri thread.  
  
 `SyncLock` viene in genere utilizzato per evitare che i dati vengano aggiornati da più thread contemporaneamente.  Se le istruzioni che modificano i dati devono essere completate senza interruzioni, è opportuno inserirle in un blocco `SyncLock`.  
  
 Un blocco di istruzioni protetto da un blocco esclusivo viene talvolta definito *sezione critica*.  
  
## Regole  
  
-   Diramazione.  Non è consentita la diramazione in un blocco `SyncLock` dall'esterno del blocco.  
  
-   Valore dell'oggetto di blocco.  Il valore di `lockobject` non può essere `Nothing`.  Per utilizzare l'oggetto di blocco in un'istruzione `SyncLock`, è necessario prima crearlo.  
  
     Non è possibile modificare il valore di `lockobject` durante l'esecuzione di un blocco `SyncLock`.  Per il corretto funzionamento del meccanismo è necessario che l'oggetto di blocco rimanga invariato.  
  
-   Non è possibile utilizzare l'operatore [Attendere](../../../visual-basic/language-reference/operators/await-operator.md) in un blocco `SyncLock`.  
  
## Comportamento  
  
-   Meccanismo.  Quando un thread raggiunge l'istruzione `SyncLock`, valuta l'espressione `lockobject` e sospende l'esecuzione fino all'acquisizione di un blocco esclusivo sull'oggetto restituito dall'espressione.  Quando un altro thread raggiunge l'istruzione `SyncLock`, non acquisisce un blocco fino a quando il primo thread non esegue l'istruzione `End SyncLock`.  
  
-   Dati protetti.  Se `lockobject` è una variabile `Shared`, il blocco esclusivo impedisce a un thread di qualsiasi istanza della classe di eseguire il blocco di istruzioni `SyncLock` durante l'esecuzione di quest'ultimo da parte di altri thread.  In questo modo, i dati condivisi tra tutte le istanze risultano protetti.  
  
     Se `lockobject` è una variabile di istanza \(non `Shared`\), il blocco impedisce a un thread in esecuzione nell'istanza corrente di eseguire il blocco di istruzioni `SyncLock` contestualmente a un altro thread della stessa istanza.  In questo modo, i dati gestiti dalla singola istanza risultano protetti.  
  
-   Acquisizione e rilascio.  Un blocco di istruzioni `SyncLock` si comporta come una costruzione `Try...Finally` in cui il blocco di istruzioni `Try` acquisisce un blocco esclusivo su `lockobject` e il blocco di istruzioni `Finally` lo rilascia.  Per questo motivo, `SyncLock` garantisce il rilascio del blocco indipendentemente dalle modalità con cui viene terminato il blocco di istruzioni.  Ciò vale anche per le eccezioni non gestite.  
  
-   Chiamate Framework.  Il blocco di istruzioni `SyncLock` acquisisce e rilascia il blocco esclusivo effettuando chiamate ai metodi `Enter` ed `Exit` della classe `Monitor` nello spazio dei nomi <xref:System.Threading>.  
  
## Tecniche di programmazione  
 L'espressione `lockobject` dovrebbe sempre restituire un oggetto appartenente esclusivamente alla classe utilizzata.  Per la protezione di dati appartenenti all'istanza corrente è necessario dichiarare una variabile oggetto `Private`, mentre per la protezione di dati comuni a tutte le istanze è necessario dichiarare una variabile oggetto `Private Shared`.  
  
 Si consiglia di non utilizzare la parola chiave `Me` per fornire un oggetto di blocco per i dati di istanza.  Se nel codice esterno alla classe utilizzata è presente un riferimento a un'istanza di tale classe, è possibile utilizzare il riferimento come oggetto di blocco per un blocco di istruzioni `SyncLock` completamente diverso, in modo da proteggere dati differenti.  In questo modo, la classe utilizzata e l'altra classe possono bloccarsi reciprocamente impedendo l'esecuzione dei rispettivi blocchi di istruzioni `SyncLock` non correlati.  Analogamente, il blocco su una stringa può generare problemi poiché qualsiasi altro codice nel processo che utilizza la stessa stringa condividerà lo stesso blocco.  
  
 Si consiglia inoltre di non utilizzare il metodo `Me.GetType` per fornire un oggetto di blocco per i dati condivisi.  `GetType`, infatti, restituisce sempre lo stesso oggetto `Type` per un determinato nome di classe.  Il codice esterno può chiamare `GetType` sulla classe e ottenere lo stesso oggetto di blocco che si sta utilizzando.  In questo modo, le due classi si bloccano reciprocamente impedendo l'esecuzione dei rispettivi blocchi di istruzioni `SyncLock`.  
  
## Esempi  
  
### Descrizione  
 Nell'esempio riportato di seguito viene illustrata una classe che gestisce un semplice elenco di messaggi.  I messaggi sono inclusi in una matrice e l'ultimo elemento utilizzato della matrice è incluso in una variabile.  La routine `addAnotherMessage` incrementa l'ultimo elemento e memorizza il nuovo messaggio.  Queste due operazioni sono protette dalle istruzioni `SyncLock` e `End SyncLock`. Dopo che l'ultimo elemento è stato incrementato, infatti, il nuovo messaggio deve essere memorizzato prima che un altro thread possa incrementare di nuovo l'ultimo elemento.  
  
 Se la classe `simpleMessageList` condivide un unico elenco di messaggi tra tutte le istanze, le variabili `messagesList` e `messagesLast` verranno dichiarate come `Shared`.  In questo caso, anche la variabile `messagesLock` deve essere `Shared`, in modo che ogni istanza possa utilizzare un unico oggetto di blocco.  
  
### Codice  
 [!code-vb[VbVbalrThreading#1](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/synclock-statement_1.vb)]  
  
### Descrizione  
 Nell'esempio riportato di seguito vengono utilizzati dei thread e `SyncLock`.  Finché l'istruzione `SyncLock` è presente, il blocco di istruzioni costituisce una sezione critica e `balance` non risulterà mai un numero negativo.  È possibile commentare `SyncLock` e le istruzioni `End SyncLock` per vedere l'effetto di nascondere la parola chiave `SyncLock`.  
  
### Codice  
 [!code-vb[VbVbalrThreading#21](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/synclock-statement_2.vb)]  
  
### Commenti  
  
## Vedere anche  
 <xref:System.Threading>   
 <xref:System.Threading.Monitor>   
 [Sincronizzazione di thread](../Topic/Thread%20Synchronization%20\(C%23%20and%20Visual%20Basic\).md)   
 [Threading](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md)