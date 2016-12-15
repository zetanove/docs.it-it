---
title: "Visual Basic Coding Conventions | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "coding conventions, Visual Basic"
  - "examples [Visual Basic], coding conventions"
  - "Visual Basic code, conventions"
ms.assetid: c1df130b-fec6-49a5-becf-0a7e494a1d0f
caps.latest.revision: 48
caps.handback.revision: 48
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic Coding Conventions
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Microsoft sviluppa esempi e documentazione che si attengono alle linee guida di questo argomento.  Se si seguono le stesse convenzioni di codifica, si possono ottenere i vantaggi seguenti:  
  
-   Il codice deve avere un aspetto coerente, in modo che chi legge possa concentrarsi meglio sul contenuto, anziché sul layout.  
  
-   I lettori comprendono il codice più rapidamente, grazie alla possibilità di formulare presupposti basati sulle esperienze precedenti.  
  
-   È possibile copiare, modificare e gestire il codice più facilmente.  
  
-   Si garantisce che il codice dimostra le "procedure consigliate" per Visual Basic.  
  
## Convenzioni di denominazione  
  
-   Per informazioni sulle linee guida relative alla denominazione, vedere l'argomento [Convenzioni di denominazione](../Topic/Naming%20Guidelines.md).  
  
-   Non utilizzare "My" o "my" come parte di un nome di variabile,  Questa pratica crea confusione con gli oggetti `My`.  
  
-   Non è necessario modificare i nomi degli oggetti con il codice generato automaticamente per adattarli alle linee guida.  
  
## Convenzioni di layout  
  
-   Inserire le tabulazioni come spazi e utilizzare i rientri automatici con rientri a quattro spazi.  
  
-   Utilizzare **Riformattazione del listato di codice** per riformattare il codice nell'editor di codice.  Per ulteriori informazioni, vedere [Opzioni, Editor di testo, Base \(Visual Basic\)](/visual-studio/ide/reference/options-text-editor-basic-visual-basic).  
  
-   Utilizzare una sola istruzione per riga.  Non utilizzare il carattere separatore di riga di Visual Basic \(:\).  
  
-   Evitare di utilizzare il carattere esplicito "\_" di continuazione di riga a favore della continuazione di riga implicita quando il linguaggio lo consente.  
  
-   Utilizzare una sola dichiarazione per riga.  
  
-   Se tramite l'opzione **Riformatta il listato di codice** le righe di continuazione non vengono formattate automaticamente, impostare manualmente il rientro delle righe di continuazione di un punto di tabulazione.  Tuttavia, allineare sempre a sinistra gli elementi in un elenco.  
  
    ```  
    a As Integer,  
    b As Integer  
    ```  
  
-   Aggiungere almeno una riga vuota tra le definizioni di metodi e di proprietà.  
  
## Convenzioni relative ai commenti  
  
-   Inserire i commenti in una riga distinta, anziché alla fine di una riga di codice.  
  
-   Iniziare il testo del commento con una lettera maiuscola e terminarlo con un punto.  
  
-   Inserire uno spazio tra il delimitatore di commento \('\) e il testo del commento.  
  
     [!code-vb[VbVbalrGuidelines#2](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_1.vb)]  
  
-   Non racchiudere i commenti in blocchi formattati di asterischi.  
  
## Struttura del programma  
  
-   Quando si utilizza il metodo `Main`, utilizzare il costrutto predefinito per le nuove applicazioni console e utilizzare `My` per gli argomenti della riga di comando.  
  
     [!code-vb[VbVbalrGuidelines#3](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_2.vb)]  
  
## Istruzioni relative al linguaggio  
  
### Tipo di dati String  
  
-   Per concatenare le stringhe, utilizzare una e commerciale \(&\).  
  
     [!code-vb[VbVbalrGuidelines#4](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_3.vb)]  
  
-   Per accodare stringhe nei cicli, utilizzare l'oggetto <xref:System.Text.StringBuilder>.  
  
     [!code-vb[VbVbalrGuidelines#5](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_4.vb)]  
  
### Delegati di tipo relaxed nei gestori eventi  
 Non qualificare esplicitamente gli argomenti \(Object e EventArgs\) nei gestori eventi.  Se non si utilizzano gli argomenti dell'evento che vengano passati a un evento \(ad esempio mittente come Object e come EventArgs\), utilizzare i delegati di tipo relaxed e omettere gli argomenti dell'evento nel codice:  
  
 [!code-vb[VbVbalrGuidelines#7](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_5.vb)]  
  
### Tipi di dati senza segno  
  
-   Utilizzare `Integer` anziché tipi senza segno, ad eccezione dei casi in cui sono necessari.  
  
### Matrici  
  
-   Utilizzare la sintassi breve quando si inizializzano matrici nella riga della dichiarazione.  Ad esempio, utilizzare la seguente sintassi.  
  
     [!code-vb[VbVbalrGuidelines#8](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_6.vb)]  
  
     Non utilizzare la seguente sintassi.  
  
     [!code-vb[VbVbalrGuidelines#9](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_7.vb)]  
  
-   Inserire l'identificatore di matrici nel tipo e non nella variabile:  Ad esempio, utilizzare la seguente sintassi:  
  
     [!code-vb[VbVbalrGuidelines#11](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_8.vb)]  
  
     Non utilizzare la seguente sintassi:  
  
     [!code-vb[VbVbalrGuidelines#10](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_9.vb)]  
  
-   Utilizzare la sintassi { } quando si dichiarano e si inizializzano le matrici dei tipi di dati di base.  Ad esempio, utilizzare la seguente sintassi:  
  
     [!code-vb[VbVbalrGuidelines#12](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_10.vb)]  
  
     Non utilizzare la seguente sintassi:  
  
     [!code-vb[VbVbalrGuidelines#13](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_11.vb)]  
  
### Utilizzare la parola chiave With  
 Quando si effettua una serie di chiamate a un oggetto, è consigliabile utilizzare la parola chiave `With`.  
  
 [!code-vb[VbVbalrGuidelines#15](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_12.vb)]  
  
### Utilizzo delle istruzioni Try...Catch e Using quando si utilizza Gestione delle eccezioni  
 Non utilizzare la proprietà `On Error Goto`.  
  
### Utilizzo della parola chiave IsNot  
 Utilizzare la parola chiave `IsNot` anziché `Not...Is Nothing`.  
  
### Parola chiave New  
  
-   Utilizzare la creazione di istanze breve.  Ad esempio, utilizzare la seguente sintassi:  
  
     [!code-vb[VbVbalrGuidelines#21](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_13.vb)]  
  
     La riga precedente è equivalente a:  
  
     [!code-vb[VbVbalrGuidelines#22](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_14.vb)]  
  
-   Per i nuovi oggetti, utilizzare inizializzatori di oggetti anziché il costruttore senza parametri:  
  
     [!code-vb[VbVbalrGuidelines#23](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_15.vb)]  
  
### Gestione di eventi  
  
-   Utilizzare `Handles` invece di `AddHandler`:  
  
     [!code-vb[VbVbalrGuidelines#24](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_16.vb)]  
  
-   Utilizzare `AddressOf` e non creare l'istanza del delegato in modo esplicito:  
  
     [!code-vb[VbVbalrGuidelines#25](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_17.vb)]  
  
-   Quando si definisce un evento, utilizzare la sintassi breve e lasciare che il delegato venga definito dal compilatore:  
  
     [!code-vb[VbVbalrGuidelines#26](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_18.vb)]  
  
-   Non verificare se un evento è `Nothing` \(null\) prima di chiamare il metodo `RaiseEvent`.  Il metodo `RaiseEvent` esegue una ricerca per  `Nothing` prima di generare l'evento.  
  
### Utilizzo di membri condivisi  
 Per la chiamata a membri `Shared`, utilizzare il nome della classe anziché una variabile di istanza.  
  
### Utilizzo di valori letterali XML  
 I valori letterali XML semplificano le attività più comuni nell'utilizzo di XML \(caricamento, query, trasformazione e così via\).  Quando si utilizza XML a fini di sviluppo, attenersi alle seguenti linee guida:  
  
-   Utilizzare i valori letterali XML per creare documenti e frammenti XML anziché chiamare direttamente API XML.  
  
-   Importare spazi dei nomi XML a livello di file o di progetto per sfruttare le ottimizzazioni delle prestazioni per i valori letterali XML.  
  
-   Utilizzare le proprietà axis XML per accedere a elementi e attributi in un documento XML.  
  
-   Utilizzare le espressioni incorporate per includere valori e creare XML da valori esistenti anziché utilizzare le chiamate API, ad esempio il metodo `Add`:  
  
     [!code-vb[VbVbalrGuidelines#27](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_19.vb)]  
  
### Query LINQ  
  
-   Utilizzare nomi significativi per le variabili di query:  
  
     [!code-vb[VbVbalrGuidelines#28](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_20.vb)]  
  
-   Fornire nomi per gli elementi delle query, in modo che i nomi di proprietà dei tipi anonimi vengano convertiti in maiuscole in modo corretto utilizzando la convenzione Pascal:  
  
     [!code-vb[VbVbalrGuidelines#29](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_21.vb)]  
  
-   Rinominare le proprietà quando i nomi potrebbero risultare ambigui nel risultato.  Ad esempio, se la query restituisce il nome di un cliente e l'ID di un ordine, anziché lasciarli come `Name` e `ID` nei risultati, sarà bene rinominarli come indicato di seguito:  
  
     [!code-vb[VbVbalrGuidelines#30](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_22.vb)]  
  
-   Utilizzare l'inferenza dei tipi nella dichiarazione di variabili di query e variabili di intervallo:  
  
     [!code-vb[VbVbalrGuidelines#31](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_23.vb)]  
  
-   Allineare le clausole di query sotto l'istruzione `From`:  
  
     [!code-vb[VbVbalrGuidelines#32](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_24.vb)]  
  
-   Utilizzare le clausole `Where` prima di altre clausole di query, in modo che le ultime clausole di query agiscano su un insieme di dati filtrato:  
  
     [!code-vb[VbVbalrGuidelines#33](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_25.vb)]  
  
-   Utilizzare la clausola `Join` per definire un'operazione di join in modo esplicito anziché utilizzare la clausola `Where` per definire l'operazione di join in modo implicito:  
  
     [!code-vb[VbVbalrGuidelines#34](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_26.vb)]  
  
## Vedere anche  
 [Secure Coding Guidelines](../Topic/Secure%20Coding%20Guidelines.md)