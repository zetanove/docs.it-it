---
title: "Object Lifetime: How Objects Are Created and Destroyed (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Constructor"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "destructors, object lifetime"
  - "Sub Finalize destructor"
  - "objects [Visual Basic], destroying"
  - "lifetime, objects"
  - "Sub New constructor, object lifetime"
  - "Finalize method, object lifetime"
  - "objects [Visual Basic], creating"
  - "Class_Terminate"
  - "Dispose method, object lifetime"
  - "Class_Initialize"
  - "object creation, object lifetime"
  - "parameterized constructors"
  - "objects [Visual Basic], lifetime"
  - "objects [Visual Basic], garbage collection"
  - "constructors [Visual Basic], object lifetime"
  - "Sub Dispose destructor"
  - "garbage collection, Visual Basic"
ms.assetid: f1ee8458-b156-44e0-9a8a-5dd171648cd8
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Object Lifetime: How Objects Are Created and Destroyed (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È stata creata un'istanza di una classe, un oggetto, mediante la parola chiave `New`.  Prima di usare i nuovi oggetti per la prima volta, è spesso necessario eseguire attività di inizializzazione.  Tra le attività di inizializzazione più comuni vi sono l'apertura dei file, la connessione a un database e la lettura dei valori delle chiavi del Registro di sistema.  In Visual Basic l'inizializzazione di nuovi oggetti viene controllata tramite routine definite *costruttori*, vale a dire metodi speciali che consentono il controllo dell'inizializzazione.  
  
 Dopo aver abbandona un ambito, un oggetto viene rilasciato da Common Language Runtime \(CLR\).  In Visual Basic il rilascio delle risorse di sistema viene controllato mediante routine denominate *distruttori*.  Sia i costruttori che i distruttori supportano la creazione di librerie di classi prevedibili e affidabili.  
  
## Uso di costruttori e distruttori  
 È possibile usare costruttori e distruttori per controllare la creazione e l'eliminazione di oggetti.  In Visual Basic le routine `Sub New` e `Sub Finalize` consentono di inizializzare ed eliminare in modo permanente gli oggetti sostituendo i metodi `Class_Initialize` e `Class_Terminate` usati in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 6.0 e nelle versioni precedenti.  
  
### Sub New  
 Il costruttore `Sub New` può essere eseguito solo una volta dopo la creazione di una classe.  Non può essere chiamato in modo esplicito in alcun punto che non sia la prima riga di codice di un altro costruttore, dalla stessa classe o da una classe derivata.  Inoltre, il codice nel metodo `Sub New` viene sempre eseguito prima di qualsiasi altro codice in una classe.  In [!INCLUDE[vbprvblong](../../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] e nelle versioni successive, se non si definisce in modo esplicito una routine `Sub New` per una classe, in fase di esecuzione viene creato implicitamente un costruttore `Sub New`.  
  
 Per creare un costruttore per una classe, creare una routine denominata `Sub New` in qualsiasi punto della definizione della classe.  Per creare un costruttore con parametri, specificare i nomi e i tipi di dati degli argomenti su `Sub New` analogamente a come si specificano argomenti per qualsiasi altra routine, come illustrato nel codice seguente:  
  
 [!code-vb[VbVbalrOOP#42](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/WhidbeyStuff.vb#42)]  
  
 I costruttori sono spesso in overload, come nell'esempio seguente:  
  
 [!code-vb[VbVbalrOOP#116](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/WhidbeyStuff.vb#116)]  
  
 Quando si definisce una classe derivata da un'altra classe, la prima riga di un costruttore deve essere una chiamata al costruttore della classe base, a meno che questa disponga di un costruttore accessibile che non accetta parametri.  Una chiamata della classe base che contiene questo costruttore sarebbe ad esempio `MyBase.New(s)`.  In caso contrario, l'oggetto `MyBase.New` è facoltativo e il runtime di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] lo chiama implicitamente.  
  
 Dopo aver scritto il codice per chiamare il costruttore di un oggetto padre, è possibile aggiungere un codice di inizializzazione alla routine `Sub New`.  La routine `Sub New` può accettare gli argomenti quando viene chiamata come costruttore con parametri.  Tali parametri vengono passati dalla routine che chiama il costruttore, ad esempio, `Dim AnObject As New ThisClass(X)`.  
  
### Sub Finalize  
 Prima di rilasciare oggetti, CLR richiede automaticamente al metodo `Finalize` gli oggetti che definiscono una routine `Sub Finalize`.  È possibile che il metodo `Finalize` contenga codice che è necessario eseguire subito prima dell'eliminazione permanente di un oggetto, ad esempio codice relativo alla chiusura di file e al salvataggio delle informazioni sullo stato.  L'esecuzione di `Sub Finalize` comporta una lieve riduzione delle prestazioni. Si consiglia quindi di definire un metodo `Sub Finalize` solo quando è necessario rilasciare in modo esplicito gli oggetti.  
  
> [!NOTE]
>  Il Garbage Collector in CLR non elimina, e non può eliminare, gli *oggetti non gestiti*, vale a dire gli oggetti che vengono eseguiti direttamente dal sistema operativo all'esterno dell'ambiente CLR.  Questo perché i diversi oggetti non gestiti devono essere eliminati in modi differenti.  Le informazioni non sono direttamente associate all'oggetto non gestito e devono quindi essere identificate nella documentazione relativa all'oggetto.  Se una classe usa oggetti non gestiti, è necessario eliminarli nel relativo metodo `Finalize`.  
  
 Il distruttore `Finalize` è un metodo protetto che può essere chiamato solo dalla classe a cui appartiene o dalle classi derivate.  Poiché `Finalize` viene chiamato automaticamente dal sistema quando viene eliminato in modo permanente un oggetto, si consiglia di non chiamare `Finalize` in modo esplicito dall'esterno dell'implementazione `Finalize` di una classe derivata.  
  
 A differenza del metodo `Class_Terminate` che viene eseguito subito dopo aver impostato un oggetto su Nothing, tra l'abbandono dell'ambito da parte di un oggetto e la chiamata del distruttore `Finalize` da parte di Visual Basic si verifica generalmente un ritardo.  [!INCLUDE[vbprvblong](../../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] e versioni successive supporta un altro tipo di distruttore, <xref:System.IDisposable.Dispose%2A>, che può essere chiamato in modo esplicito in qualsiasi momento per rilasciare subito le risorse.  
  
> [!NOTE]
>  Un distruttore `Finalize` non deve generare eccezioni, perché queste non possono essere gestite dall'applicazione e possono provocarne l'interruzione.  
  
### Uso dei metodi New e Finalize in una gerarchia di classi  
 Ogni volta che viene creata un'istanza di una classe, nel Common Language Runtime \(CLR\) viene effettuato un tentativo di eseguire una routine denominata `New`, se esiste in quell'oggetto.  `New` è un tipo di routine chiamato `constructor` che consente di inizializzare nuovi oggetti prima che venga eseguito qualsiasi altro codice in un oggetto.  Un costruttore `New` consente di aprire file, collegarsi a database, inizializzare variabili e svolgere ogni altra attività necessaria prima che un oggetto possa essere usato.  
  
 Quando viene creata un'istanza di una classe derivata, viene eseguito innanzitutto il costruttore `Sub New` della classe base, seguito dai costruttori delle classi derivate.  Nella prima riga del codice di un costruttore `Sub New`, infatti, viene usata la sintassi `MyBase.New()` per chiamare il costruttore della classe immediatamente superiore nella gerarchia delle classi.  Viene quindi eseguita la chiamata al costruttore `Sub New` di ogni classe della gerarchia fino al raggiungimento del costruttore della classe base.  A quel punto viene eseguito il codice del costruttore della classe base, seguito dal codice del costruttore di tutte le classi derivate. In ultimo viene eseguito il codice delle classi derivate di livello più basso.  
  
 ![Costruttori ed ereditarietà](../../../../visual-basic/programming-guide/language-features/objects-and-classes/media/vaconstructorsinheritance.gif "vaConstructorsInheritance")  
  
 Quando un oggetto non è più necessario, prima di liberare la memoria corrispondente viene chiamato il metodo <xref:System.Object.Finalize%2A> relativo a quell'oggetto.  Il metodo <xref:System.Object.Finalize%2A> è denominato `destructor`, perché consente di eseguire attività di pulizia, quali il salvataggio delle informazioni sullo stato, la chiusura dei file e delle connessioni ai database e altre attività necessarie prima del rilascio dell'oggetto.  
  
 ![Inheritance2 dei costruttori](../../../../visual-basic/programming-guide/language-features/objects-and-classes/media/vaconstructorsinheritance-2.gif "vaConstructorsInheritance\_2")  
  
## Interfaccia IDisposable  
 Le istanze di classe controllano spesso risorse non gestite da CLR, quali gli handle di Windows e le connessioni al database.  È necessario eliminare queste risorse in modo permanente nel metodo `Finalize` della classe per consentirne il rilascio quando il Garbage Collector rimuove l'oggetto.  Tuttavia, poiché il Garbage Collector elimina gli oggetti in modo permanente solo quando CLR richiede la disponibilità di maggiore memoria,  è possibile che le risorse vengano rilasciate solo molto tempo dopo l'abbandono dell'ambito da parte dell'oggetto.  
  
 A supporto del Garbage Collector, le classi possono implementare l'interfaccia <xref:System.IDisposable> per fornire un sistema di gestione attiva delle risorse di sistema.  <xref:System.IDisposable> dispone di un metodo, <xref:System.IDisposable.Dispose%2A> che i client chiamano dopo aver usato un oggetto.  È possibile usare il metodo <xref:System.IDisposable.Dispose%2A> per rilasciare immediatamente risorse ed eseguire attività quali la chiusura di file e le connessioni al database.  A differenza del distruttore `Finalize`, il metodo <xref:System.IDisposable.Dispose%2A> non viene chiamato automaticamente.  Quando si vogliono rilasciare immediatamente risorse, è necessario che i client di una classe chiamino in modo esplicito il metodo <xref:System.IDisposable.Dispose%2A>.  
  
### Implementazione di IDisposable  
 Una classe che implementa l'interfaccia <xref:System.IDisposable> deve includere il codice seguente:  
  
-   Campo che consente di controllare se l'oggetto è stato eliminato in modo permanente:  
  
    ```  
    Protected disposed As Boolean = False  
    ```  
  
-   Overload del metodo <xref:System.IDisposable.Dispose%2A> che consente di liberare le risorse della classe.  Questo metodo deve essere chiamato dai metodi <xref:System.IDisposable.Dispose%2A> e `Finalize` della classe base:  
  
    ```  
    Protected Overridable Sub Dispose(ByVal disposing As Boolean)  
        If Not Me.disposed Then  
            If disposing Then  
                ' Insert code to free managed resources.  
            End If  
            ' Insert code to free unmanaged resources.  
        End If  
        Me.disposed = True  
    End Sub  
    ```  
  
-   Implementazione di <xref:System.IDisposable.Dispose%2A> che contiene solo il codice seguente:  
  
    ```  
    Public Sub Dispose() Implements IDisposable.Dispose  
        Dispose(True)  
        GC.SuppressFinalize(Me)  
    End Sub  
    ```  
  
-   Override del metodo `Finalize` che contiene solo il codice seguente:  
  
    ```  
    Protected Overrides Sub Finalize()  
        Dispose(False)  
        MyBase.Finalize()  
    End Sub  
    ```  
  
### Derivazione da una classe che implementa IDisposable  
 Non è necessario eseguire l'override di tutti i metodi di base in una classe derivata da una classe base che implementa l'interfaccia <xref:System.IDisposable>, a meno che tale classe non usi risorse aggiuntive che devono essere eliminate in modo permanente.  In questo caso, la classe derivata deve eseguire l'override del metodo `Dispose(disposing)` della classe base per eliminare in modo permanente le risorse della classe derivata.  Inoltre, tale override deve chiamare il metodo `Dispose(disposing)` della classe base.  
  
```  
Protected Overrides Sub Dispose(ByVal disposing As Boolean)  
    If Not Me.disposed Then  
        If disposing Then  
            ' Insert code to free managed resources.  
        End If  
        ' Insert code to free unmanaged resources.  
    End If  
    MyBase.Dispose(disposing)  
End Sub  
```  
  
 Una classe derivata non deve eseguire l'override del metodi <xref:System.IDisposable.Dispose%2A> e `Finalize` della classe base.  Infatti, quando questi metodi vengono chiamati da un'istanza della classe derivata, la relativa implementazione della classe base chiama l'override del metodo `Dispose(disposing)` della classe derivata.  
  
## Garbage Collection e il distruttore Finalize  
 In [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] viene usato il sistema di *Garbage Collection basata su tracciatura dei riferimenti* che prevede il rilascio periodico delle risorse inutilizzate.  Per la gestione delle risorse, in Visual Basic 6.0 e nelle versioni precedenti veniva usato un sistema diverso, definito *conteggio dei riferimenti*.  Anche se in entrambi i casi viene eseguita automaticamente la stessa funzione, vi sono alcune importanti differenze.  
  
 Mediante il metodo CLR gli oggetti vengono eliminati periodicamente quando il sistema stabilisce che non sono più necessari.  Gli oggetti vengono rilasciati più rapidamente quando le risorse di sistema sono insufficienti e con una frequenza minore in caso contrario.  Il ritardo tra il momento in cui un oggetto abbandona l'ambito e il relativo rilascio da parte di CLR indica che, a differenza di quanto avveniva in Visual Basic 6.0 e nelle versioni precedenti, non è possibile stabilire esattamente quando l'oggetto verrà eliminato in modo permanente.  In una situazione di questo tipo si dice che gli oggetti hanno una *durata non deterministica*.  Nella maggior parte dei casi la durata non deterministica non influisce sulla modalità di scrittura delle applicazioni, purché si ricordi che è possibile che il distruttore `Finalize` non venga eseguito immediatamente dopo la perdita di ambito di un oggetto.  
  
 Un'altra differenza tra i sistemi di Garbage Collection riguarda l'uso di `Nothing`.  Per poter usare il conteggio dei riferimenti, in Visual Basic 6.0 e nelle versioni precedenti, a volte veniva assegnato `Nothing` alle variabili oggetto in modo da rilasciare i riferimenti contenuti in tali variabili.  Se la variabile conteneva l'ultimo riferimento all'oggetto, le risorse dell'oggetto venivano rilasciate immediatamente.  Anche se in alcuni casi questa routine può risultare ancora utile, la sua esecuzione nelle versioni successive di Visual Basic non risulta mai nel rilascio immediato delle risorse da parte dell'oggetto a cui si fa riferimento.  Per rilasciare subito le risorse, usare il metodo <xref:System.IDisposable.Dispose%2A> dell'oggetto, se disponibile.  Si consiglia di impostare una variabile su `Nothing` solo nel caso in cui la durata della variabile risulti lunga in relazione al tempo necessario per l'individuazione degli oggetti isolati tramite le operazioni del Garbage Collector.  
  
## Vedere anche  
 <xref:System.IDisposable.Dispose%2A>   
 [Initialization and Termination of Components](../Topic/Initialization%20and%20Termination%20of%20Components.md)   
 [New Operator](../../../../visual-basic/language-reference/operators/new-operator.md)   
 [Cleaning Up Unmanaged Resources](../Topic/Cleaning%20Up%20Unmanaged%20Resources.md)   
 [Nothing](../../../../visual-basic/language-reference/nothing.md)