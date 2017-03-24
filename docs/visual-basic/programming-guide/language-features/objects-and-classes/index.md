---
title: "Objects and Classes in Visual Basic | Microsoft Docs"
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
  - "classes [Visual Basic]"
  - "objects [Visual Basic]"
ms.assetid: c68c5752-1006-46e1-975a-6717b62a42fc
caps.latest.revision: 26
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 26
---
# Objects and Classes in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un *oggetto* è una combinazione di codice e dati che è possibile considerare come singola unità.  Un oggetto può essere una parte di un'applicazione, come un controllo o un form.  Anche un'intera applicazione può essere un oggetto.  
  
 Durante la creazione di un'applicazione in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] si utilizzano costantemente degli oggetti.  È possibile utilizzare oggetti forniti da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], come ad esempio controlli, form e oggetti di accesso ai dati.  È anche possibile utilizzare oggetti di altre applicazioni all'interno dell'applicazione [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] che si sta sviluppando.  È possibile inoltre creare oggetti personalizzati e definire per essi proprietà e metodi supplementari.  Per i programmi, gli oggetti svolgono la stessa funzione dei blocchi predefiniti prefabbricati: essi consentono di scrivere un pezzo di codice una sola volta e di riutilizzarlo ripetutamente.  
  
 In questo argomento vengono fornite informazioni dettagliate sugli oggetti.  
  
## Oggetti e classi  
 Ogni oggetto di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] è definito da una *classe* che ne descrive le variabili, le proprietà, le routine e gli eventi.  Gli oggetti sono istanze di classi. Una volta definita una classe, sarà possibile creare tutti gli oggetti necessari.  
  
 Per comprendere la relazione esistente tra un oggetto e la relativa classe di appartenenza, si pensi agli stampi per biscotti e ai biscotti.  La classe è lo stampo  che definisce le caratteristiche di ogni biscotto, quali dimensioni e forma.  La classe viene utilizzata per creare oggetti.  Gli oggetti sono i biscotti.  
  
 Per poter accedere ai membri di un oggetto, è prima necessario creare l'oggetto.  
  
#### Per creare un oggetto da una classe  
  
1.  Scegliere la classe da cui si desidera creare un oggetto.  
  
2.  Scrivere un'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) per creare una variabile a cui è possibile assegnare un'istanza di una classe.  La variabile dovrebbe essere del tipo della classe desiderata.  
  
    ```  
  
    Dim nextCustomer As customer   
    ```  
  
3.  Aggiungere la parola chiave [New Operator](../../../../visual-basic/language-reference/operators/new-operator.md) per inizializzare la variabile su una nuova istanza della classe.  
  
    ```  
    Dim nextCustomer As New customer  
    ```  
  
4.  È ora possibile accedere ai membri della classe mediante la variabile oggetto.  
  
    ```  
  
    nextCustomer.accountNumber = lastAccountNumber + 1  
    ```  
  
> [!NOTE]
>  Laddove possibile, è necessario dichiarare che la variabile appartiene al tipo di classe a cui si intende assegnarla.  Questa operazione viene definita *associazione anticipata*.  Se il tipo di classe non è noto in fase di compilazione, è possibile richiamare l'*associazione tardiva* dichiarando che la variabile è del [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md).  Questo tipo di associazione comporta tuttavia il rischio di un rallentamento delle prestazioni e di una limitazione dell'accesso ai membri dell'oggetto in fase di esecuzione.  Per ulteriori informazioni, vedere [Object Variable Declaration](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md).  
  
### Istanze multiple  
 Gli oggetti creati da una classe sono spesso identici.  Una volta definiti come singoli oggetti, è comunque possibile modificarne le variabili e le proprietà indipendentemente dalle altre istanze.  Se si aggiungono a un form tre caselle di controllo, ad esempio, ogni oggetto casella di controllo è un'istanza della classe <xref:System.Windows.Forms.CheckBox>.  I singoli oggetti <xref:System.Windows.Forms.CheckBox> condividono un insieme di caratteristiche e funzionalità, come proprietà, variabili, routine ed eventi, definite dalla classe.  Ognuno di essi, tuttavia, ha un proprio nome, può essere abilitato e disabilitato separatamente e può essere posizionato in un punto diverso del form.  
  
## Membri degli oggetti  
 Un oggetto è un elemento di un'applicazione che rappresenta un'*istanza* di una classe.  I campi, le proprietà, i metodi e gli eventi sono i blocchi predefiniti degli oggetti e ne costituiscono i *membri*.  
  
### Accesso ai membri  
 Per accedere a un membro di un oggetto, è necessario specificare il nome della variabile oggetto, un punto \(`.`\) e il nome del membro, nell'ordine indicato.  Nell'esempio riportato di seguito viene impostata la proprietà <xref:System.Windows.Forms.Control.Text%2A> di un oggetto <xref:System.Windows.Forms.Label>.  
  
```  
warningLabel.Text = "Data not saved"  
```  
  
#### Elenco di membri IntelliSense  
 Quando si richiama l'opzione Elenca membri relativa a una classe, ad esempio quando si digita un punto \(`.`\) come operatore di accesso ai membri, IntelliSense elenca i membri della classe.  Se si digita il punto dopo il nome di una variabile dichiarata come istanza della classe, vengono elencati tutti i membri di istanza ma nessuno dei membri condivisi.  Se si digita il punto dopo il nome della classe, vengono elencati tutti i membri condivisi ma nessuno dei membri di istanza.  Per ulteriori informazioni, vedere [Utilizzo di IntelliSense](/visual-studio/ide/using-intellisense).  
  
### Campi e proprietà  
 I *campi* e le *proprietà* rappresentano le informazioni archiviate in un oggetto.  È possibile utilizzare istruzioni di assegnazione per recuperare e impostare i valori dei campi e delle proprietà, nello stesso modo in cui vengono recuperate e impostate le variabili locali di una routine.  Nell'esempio riportato di seguito viene recuperata la proprietà <xref:System.Windows.Forms.Control.Width%2A> e impostata la proprietà <xref:System.Windows.Forms.Control.ForeColor%2A> di un oggetto <xref:System.Windows.Forms.Label>.  
  
```  
Dim warningWidth As Integer = warningLabel.Width  
warningLabel.ForeColor = System.Drawing.Color.Red  
```  
  
 Un campo è anche detto *variabile membro*.  
  
 Utilizzare le routine delle proprietà nei casi seguenti:  
  
-   È necessario controllare quando e come un valore viene impostato o recuperato.  
  
-   La proprietà contiene un insieme di valori ben definito che è necessario convalidare.  
  
-   L'impostazione di un valore determina modifiche percettibili nello stato dell'oggetto, ad esempio a una proprietà `IsVisible`.  
  
-   L'impostazione della proprietà provoca modifiche ad altre variabili interne o ai valori di altre proprietà.  
  
-   È necessario eseguire una serie di passaggi prima dell'impostazione o del recupero della proprietà.  
  
 Utilizzare i campi nei seguenti casi:  
  
-   Il valore è di tipo auto\-convalidante.  Si verifica ad esempio un errore o una conversione automatica di dati se a una variabile `Boolean` viene assegnato un valore diverso da `True` o `False`.  
  
-   Tutti i valori nell'intervallo supportato dal tipo di dati sono validi,  ad esempio nel caso di molte proprietà di tipo `Single` o `Double`.  
  
-   La proprietà è un tipo di dati `String` e non vi è alcun vincolo sulla dimensione o il valore della stringa.  
  
-   Per ulteriori informazioni, vedere [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md).  
  
### Metodi  
 Un *metodo* è un'azione che può essere eseguita da un oggetto.  Ad esempio, <xref:System.Windows.Forms.ComboBox.ObjectCollection.Add%2A> è un metodo dell'oggetto <xref:System.Windows.Forms.ComboBox> che consente di aggiungere una nuova voce a una casella combinata.  
  
 Nell'esempio riportato di seguito viene illustrato il metodo <xref:System.Windows.Forms.Timer.Start%2A> di un oggetto <xref:System.Windows.Forms.Timer>.  
  
```  
Dim safetyTimer As New System.Windows.Forms.Timer  
safetyTimer.Start()  
```  
  
 Un metodo è semplicemente una *routine* esposta da un oggetto.  
  
 Per ulteriori informazioni, vedere [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md).  
  
### Eventi  
 Un evento è un'azione che viene riconosciuta da un oggetto, come il clic del mouse o la pressione di un tasto, e alla quale è possibile rispondere mediante un codice scritto appositamente.  Gli eventi possono verificarsi come conseguenza di un'azione utente o un codice di programma oppure possono essere generati dal sistema.  Il codice che segnala un evento è detto codice che *genera* l'evento mentre il codice che risponde a un evento è detto codice che *gestisce* l'evento.  
  
 È inoltre possibile sviluppare eventi personalizzati generati dai propri oggetti e gestiti da altri oggetti.  Per ulteriori informazioni, vedere [Events](../../../../visual-basic/programming-guide/language-features/events/events.md).  
  
### Membri di istanza e membri condivisi  
 Quando si crea un oggetto da una classe, il risultato è un'istanza della classe.  I membri non dichiarati con la parola chiave [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) sono *membri di istanza* e appartengono soltanto alla particolare istanza.  Un membro di istanza appartenente a una determinata istanza è indipendente dallo stesso membro appartenente a un'altra istanza della stessa classe.  Una variabile membro di istanza, ad esempio, può avere valori differenti in istanze differenti.  
  
 I membri dichiarati con la parola chiave `Shared` sono *membri condivisi* e appartengono all'intera classe e non a una particolare istanza.  Un membro condiviso viene definito una sola volta, indipendentemente dal numero di istanze della relativa classe create \(anche se non viene creata alcuna istanza\).  Una variabile membro condiviso, ad esempio, può avere un unico valore, che può essere utilizzato da tutte le parti di codice che possono accedere alla classe.  
  
#### Accesso a membri non condivisi  
  
###### Per accedere a un membro non condiviso di un oggetto  
  
1.  Accertarsi che l'oggetto sia stato creato a partire dalla rispettiva classe e che sia stato assegnato a una variabile oggetto.  
  
    ```  
    Dim secondForm As New System.Windows.Forms.Form  
    ```  
  
2.  Nell'istruzione che consente l'accesso al membro inserire il nome della variabile oggetto, quindi l'*operatore di accesso ai membri* \(`.`\) e infine il nome del membro.  
  
    ```  
    secondForm.Show()  
    ```  
  
#### Accesso a membri condivisi  
  
###### Per accedere a un membro condiviso di un oggetto  
  
-   Inserire il nome della classe, quindi l'*operatore di accesso ai membri* \(`.`\) e infine il nome del membro.  È necessario accedere sempre a un membro `Shared` dell'oggetto tramite il nome della classe.  
  
    ```  
    MsgBox("This computer is called " & Environment.MachineName)  
    ```  
  
-   In alternativa, se è già stato creato un oggetto a partire dalla classe, è possibile accedere a un membro `Shared` tramite la variabile dell'oggetto.  
  
### Differenze tra classi e moduli  
 La differenza principale tra classi e moduli consiste nella possibilità di creare istanze delle classi come oggetti, che non esiste per i moduli standard.  Poiché è presente una sola copia di dati di un modulo standard, quando una variabile pubblica viene modificata in un modulo standard da una parte del programma tutte le altre parti del programma ricevono lo stesso valore, per l'eventualità che la variabile venga letta successivamente.  I dati degli oggetti, invece, sono separati per ciascun oggetto per il quale sia stata creata un'istanza.  A differenza dei moduli standard inoltre le classi possono implementare interfacce.  
  
> [!NOTE]
>  Quando si applica un modificatore `Shared` a un membro di classe, il modificatore viene associato alla classe stessa piuttosto che a una particolare istanza della classe.  L'accesso al membro avviene direttamente tramite il nome della classe, nello stesso modo in cui si accede ai membri del modulo.  
  
 Le classi e i moduli utilizzano inoltre ambiti diversi per i rispettivi membri.  I membri definiti in una classe vengono inseriti in un ambito limitato a una specifica istanza della classe ed esistono solo per la durata dell'oggetto.  Per accedere ai membri di una classe dall'esterno di una classe, è necessario utilizzare nomi completi nel formato *Object*.*Member*.  
  
 D'altra parte, i membri dichiarati all'interno di un modulo hanno accesso pubblico per impostazione predefinita e ad essi può accedere qualsiasi codice che abbia accesso al modulo.  Le variabili presenti in un modulo standard sono quindi effettivamente variabili globali, in quanto sono visibili da qualunque punto del progetto ed esistono per la durata del programma.  
  
## Riutilizzo di classi e oggetti  
 Grazie agli oggetti è possibile dichiarare variabili e routine una sola volta e quindi riutilizzarle ogni volta che ve ne sia la necessità.  Se, ad esempio, si desidera aggiungere un correttore ortografico a un'applicazione, è possibile definire tutte le variabili e le funzioni di supporto per fornire all'applicazione la funzionalità del correttore ortografico.  Se il controllo ortografico viene creato come classe, sarà possibile riutilizzarlo in altre applicazioni aggiungendo un riferimento all'assembly compilato  oppure sarà possibile risparmiare lavoro utilizzando la classe di un correttore ortografico già sviluppata da altri programmatori.  
  
 In [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] vengono forniti numerosi esempi di componenti disponibili per l'utilizzo.  Nell'esempio seguente viene utilizzata la classe <xref:System.TimeZone> nello spazio dei nomi <xref:System>.  <xref:System.TimeZone> fornisce i membri che consentono di recuperare le informazioni sul fuso orario del computer corrente.  
  
```  
Public Sub examineTimeZone()  
    Dim tz As System.TimeZone = System.TimeZone.CurrentTimeZone  
    Dim s As String = "Current time zone is "  
    s &= CStr(tz.GetUtcOffset(Now).Hours) & " hours and "  
    s &= CStr(tz.GetUtcOffset(Now).Minutes) & " minutes "  
    s &= "different from UTC (coordinated universal time)"  
    s &= vbCrLf & "and is currently "  
    If tz.IsDaylightSavingTime(Now) = False Then s &= "not "  
    s &= "on ""summer time""."  
    MsgBox(s)  
End Sub  
```  
  
 Nell'esempio precedente la prima [Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) dichiara una variabile oggetto di tipo <xref:System.TimeZone> e la assegna a un oggetto <xref:System.TimeZone> restituito dalla proprietà <xref:System.TimeZone.CurrentTimeZone%2A>.  
  
## Relazioni tra oggetti  
 Gli oggetti possono essere posti in relazione tra loro in molti modi.  Esistono due tipi principali di relazione, ovvero *gerarchica* e *di contenimento*.  
  
### Relazione gerarchica  
 Tra le classi che derivano da altre classi fondamentali e queste ultime esiste una *relazione gerarchica*.  Le gerarchie delle classi sono utili per descrivere gli elementi che sono un sottotipo di una classe più generale.  
  
 Nell'esempio riportato di seguito si supponga di voler definire un tipo speciale di classe <xref:System.Windows.Forms.Button> che si comporti come una normale classe <xref:System.Windows.Forms.Button> ma che esponga anche un metodo che consente di invertire i colori di sfondo e di primo piano.  
  
##### Per definire una classe derivata da una classe già esistente  
  
1.  Utilizzare un'[Class Statement](../../../../visual-basic/language-reference/statements/class-statement.md) per definire una classe dalla quale creare l'oggetto richiesto.  
  
     `Public Class reversibleButton`  
  
     Assicurarsi che l'ultima riga di codice nella classe sia seguita da un'istruzione `End Class`.  Per impostazione predefinita, quando si immette un'istruzione `Class` l'ambiente di sviluppo integrato \(IDE\) genera automaticamente un'istruzione `End Class`.  
  
2.  Aggiungere un'[Inherits Statement](../../../../visual-basic/language-reference/statements/inherits-statement.md) subito dopo l'istruzione `Class`.  Specificare la classe dalla quale deriva la nuova classe.  
  
     `Inherits System.Windows.Forms.Button`  
  
     La nuova classe eredita tutti i membri definiti dalla classe base.  
  
3.  Aggiungere il codice per i membri aggiuntivi esposti dalla classe derivata.  Ad esempio, è possibile aggiungere un metodo `reverseColors`. La classe derivata potrebbe essere simile alla seguente:  
  
    ```  
    Public Class reversibleButton  
        Inherits System.Windows.Forms.Button  
        Public Sub reverseColors()   
            Dim saveColor As System.Drawing.Color = Me.BackColor  
            Me.BackColor = Me.ForeColor  
            Me.ForeColor = saveColor  
        End Sub  
    End Class   
    ```  
  
     Se si crea un oggetto dalla classe `reversibleButton`, tale oggetto potrà accedere a tutti i membri della classe <xref:System.Windows.Forms.Button>, nonché al metodo `reverseColors` e a qualsiasi altro nuovo membro definito in `reversibleButton`.  
  
 Le classi derivate ereditano i membri della classe su cui sono basate, consentendo di raggiungere una maggiore complessità mano a mano che si avanza nella gerarchia.  Per ulteriori informazioni, vedere [Inheritance Basics](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md).  
  
#### Compilazione del codice  
 Assicurarsi che il compilatore possa accedere alla classe dalla quale si desidera derivare la nuova classe.  A tale scopo è possibile fornire il nome completo della classe, come nell'esempio precedente, oppure specificare il relativo spazio dei nomi in un'[Imports Statement \(.NET Namespace and Type\)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  Se la classe si trova in un progetto differente, può essere necessario aggiungere un riferimento a tale progetto.  Per ulteriori informazioni, vedere [Gestione dei riferimenti in un progetto](/visual-studio/ide/managing-references-in-a-project).  
  
### Relazione di contenimento  
 Gli oggetti possono anche avere tra loro una *relazione di contenimento*.  Gli oggetti contenitore incapsulano logicamente altri oggetti.  L'oggetto <xref:System.OperatingSystem> ad esempio contiene logicamente un oggetto <xref:System.Version>, che restituisce tramite la proprietà <xref:System.OperatingSystem.Version%2A>.  Tenere presente che l'oggetto contenitore non contiene fisicamente altri oggetti.  
  
#### Raccolte  
 Un tipo particolare di contenimento degli oggetti è rappresentato dalle *raccolte*.  Le raccolte sono gruppi di oggetti simili che possono essere enumerati.  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] supporta una sintassi specifica nell'[Istruzione For Each...Next](../../../../visual-basic/language-reference/statements/for-each-next-statement.md) che consente di scorrere gli elementi di una raccolta.  Inoltre, le raccolte consentono spesso di utilizzare una <xref:Microsoft.VisualBasic.Collection.Item%2A> per recuperare gli elementi in base al relativo indice o mediante l'associazione a una stringa univoca.  Le raccolte possono risultare di più semplice utilizzo rispetto alle matrici in quanto consentono di aggiungere o rimuovere elementi senza ricorrere agli indici.  Grazie alla loro facilità d'uso spesso vengono utilizzate per memorizzare form e controlli.  
  
## Argomenti correlati  
 [Walkthrough: Defining Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/walkthrough-defining-classes.md)  
 Viene fornita una descrizione dettagliata sulla creazione di una classe.  
  
 [Overloaded Properties and Methods](../../../../visual-basic/programming-guide/language-features/objects-and-classes/overloaded-properties-and-methods.md)  
 Proprietà in overload e metodi  
  
 [Inheritance Basics](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)  
 Vengono illustrati modificatori di ereditarietà, override di metodi e proprietà, MyClass e MyBase.  
  
 [Object Lifetime: How Objects Are Created and Destroyed](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)  
 Vengono illustrate la creazione e l'eliminazione delle istanze di classe.  
  
 [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)  
 Viene descritto come creare e utilizzare i tipi anonimi, che consentono di creare oggetti senza scrivere una definizione della classe per il tipo di dati.  
  
 [Object Initializers: Named and Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)  
 Vengono discussi gli inizializzatori di oggetto, utilizzati per creare istanze di tipi denominati e anonimi utilizzando un'unica espressione.  
  
 [Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)  
 Viene descritto come dedurre nomi e tipi di proprietà nelle dichiarazioni di tipo anonimo  Vengono forniti esempi di inferenze riuscite e non riuscite.