---
title: "Structures and Classes (Visual Basic) | Microsoft Docs"
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
  - "classes [Visual Basic], vs. structures"
  - "structures"
  - "classes [Visual Basic]"
  - "structures, compared to classes"
  - "structures, structure variables"
  - "structure variables"
ms.assetid: a221e74a-ffcf-4bdc-a0f6-a088a9bf26cc
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Structures and Classes (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] la sintassi per le strutture e le classi è stata unificata, di conseguenza entrambe le entità supportano in gran parte le stesse funzionalità.  Vi sono tuttavia alcune differenze rilevanti tra strutture e classi.  
  
 Le classi hanno il vantaggio di essere tipi di riferimento: il passaggio di un riferimento risulta più efficace del passaggio di una variabile di struttura con tutti i dati.  D'altra parte, le strutture non richiedono allocazione di memoria nell'heap globale.  
  
 Poiché non è possibile ereditare da una struttura, utilizzare le strutture solo per gli oggetti che non è necessario estendere.  Utilizzare le strutture quando l'oggetto che si desidera creare ricorre a un'istanza di piccole dimensioni e confrontare le caratteristiche delle prestazioni delle classi con quelle delle strutture.  
  
## Analogie  
 Le strutture e le classi sono analoghe per quanto riguarda i seguenti aspetti:  
  
-   Entrambi sono tipi *contenitore* e contengono quindi altri tipi come membri.  
  
-   In entrambe sono presenti dei membri, che possono includere costruttori, metodi, proprietà, campi, costanti, enumerazioni, eventi e gestori eventi.  È importante tuttavia non confondere tali membri con gli *elementi* dichiarati di una struttura.  
  
-   I membri di entrambe possono disporre di livelli di accesso personalizzati.  È possibile, ad esempio, dichiarare un membro `Public` e un altro `Private`.  
  
-   Entrambe sono in grado di implementare interfacce.  
  
-   Entrambe sono in grado di utilizzare costruttori condivisi, con o senza parametri.  
  
-   Entrambe possono esporre una *proprietà predefinita*, purché essa accetti almeno un parametro.  
  
-   Entrambe possono dichiarare e generare eventi ed entrambe possono dichiarare delegati.  
  
## Differenze  
 Le strutture e le classi si differenziano per i seguenti aspetti:  
  
-   Le strutture sono *tipi di valore*, mentre le classi sono *tipi di riferimento*.  Una variabile di un tipo di struttura contiene i dati della struttura anziché un riferimento ai dati come avviene per un tipo di classe.  
  
-   Le strutture si avvalgono dell'allocazione dello stack, le classi dell'allocazione dell'heap.  
  
-   Per impostazione predefinita, tutti gli elementi di struttura sono `Public`, le variabili e le costanti di classe sono `Private` e gli altri membri di classe sono `Public`.  Tale comportamento relativo ai membri di classe garantisce la compatibilità con il sistema di impostazioni predefinite di Visual Basic 6.0.  
  
-   Una struttura deve includere almeno una variabile non condivisa o un evento non condiviso e non personalizzato, mentre una classe può essere completamente vuota.  
  
-   A differenza dei membri di classe, gli elementi di struttura non possono essere dichiarati come `Protected`.  
  
-   Una routine di struttura può gestire eventi solo se si tratta di una routine [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) `Sub` e solo mediante l'[AddHandler Statement](../../../../visual-basic/language-reference/statements/addhandler-statement.md). Qualsiasi routine di classe può gestire gli eventi utilizzando la parola chiave [Handles](../../../../visual-basic/language-reference/statements/handles-clause.md) o l'istruzione `AddHandler`.  Per ulteriori informazioni, vedere [Events](../../../../visual-basic/programming-guide/language-features/events/events.md).  
  
-   Diversamente dalle dichiarazioni delle variabili di classe, nelle dichiarazioni delle variabili di struttura non è possibile specificare inizializzatori o dimensioni iniziali per le matrici.  
  
-   Le strutture sono in grado di ereditare implicitamente dalla classe <xref:System.ValueType?displayProperty=fullName>, ma non da altri tipi. Le classi sono in grado di ereditare da qualsiasi classe diversa da <xref:System.ValueType?displayProperty=fullName>.  
  
-   Le strutture non sono ereditabili, mentre le classi lo sono.  
  
-   Poiché le strutture non vengono mai terminate, Common Language Runtime \(CLR\) non chiama mai il metodo <xref:System.Object.Finalize%2A> per una struttura. Le classi vengono terminate dal Garbage Collector, che chiama <xref:System.Object.Finalize%2A> per una classe quando viene rilevato che non sono presenti riferimenti attivi.  
  
-   A differenza di una classe, una struttura non richiede un costruttore.  
  
-   I costruttori non condivisi sono consentiti nelle strutture solo nel caso in cui accettino parametri. Tali costruttori sono consentiti nelle classi, con o senza parametri.  
  
 Ogni struttura dispone di un costruttore pubblico implicito senza parametri.  Tale costruttore consente di inizializzare tutti i dati della struttura sui rispettivi valori predefiniti.  Non è possibile ridefinire questa caratteristica.  
  
## Istanze e variabili  
 Poiché le strutture sono tipi valore, ogni struttura disponibile è associata in modo permanente a un'istanza di struttura individuale.  Le classi sono invece tipi di riferimento e la variabile oggetto è in grado di fare riferimento a varie istanze di classe in momenti diversi.  Tale differenza influisce sull'utilizzo di classi e strutture nei modi seguenti:  
  
-   **Inizializzazione.** Una variabile di struttura include implicitamente un'inizializzazione degli elementi che utilizzano il costruttore senza parametri della struttura.  `Dim s As struct1` equivale quindi a `Dim s As struct1 = New struct1()`.  
  
-   **Assegnazione di variabili.** Quando si assegna una variabile di struttura a un'altra o si passa un'istanza di struttura a un argomento di routine, i valori correnti di tutti gli elementi variabile vengono copiati nella nuova struttura.  Quando si assegna una variabile oggetto a un'altra o si passa una variabile oggetto a una routine, viene copiato solo il puntatore di riferimento.  
  
-   **Assegnazione di Nothing.** È possibile assegnare il valore [Nothing](../../../../visual-basic/language-reference/nothing.md) a una variabile di struttura, anche se l'istanza risulterà ancora associata alla variabile.  Sarà comunque possibile chiamarne i metodi e accedere ai relativi elementi dati, sebbene gli elementi variabile vengano reinizializzati in seguito all'assegnazione.  
  
     Se invece si imposta una variabile oggetto su `Nothing`, si dissocia tale variabile da qualunque istanza di classe e non sarà possibile accedere ad alcun membro mediante la variabile fino a quando non verrà assegnata un'altra istanza a tale variabile.  
  
-   **Istanze multiple.** È possibile che a una variabile oggetto siano associate istanze di classe differenti in diversi momenti e che più variabili oggetto facciano riferimento alla stessa istanza di classe contemporaneamente.  Le modifiche apportate ai valori dei membri di classe influiscono su tali membri quando vi si accede mediante un'altra variabile che punta alla stessa istanza.  
  
     Gli elementi di struttura, tuttavia, sono isolati all'interno della relativa istanza.  Le modifiche apportate ai valori di tali membri non vengono riflesse in altre variabili di struttura, né in altre istanze della stessa dichiarazione `Structure`.  
  
-   **Uguaglianza.** È necessario eseguire il test di uguaglianza di due strutture elemento per elemento.  Per confrontare due variabili oggetto utilizzare il metodo <xref:System.Object.Equals%2A>.  <xref:System.Object.Equals%2A> indica se le due variabili puntano alla stessa istanza.  
  
## Vedere anche  
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Composite Data Types](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Structures](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Structures and Other Programming Elements](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)   
 [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)