---
title: Orientato a oggetti di programmazione (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 49794de4-64c3-473c-b8ed-fe98835df69c
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d5491b3bd5a25908194d02063f688a319509bb77
ms.lasthandoff: 03/13/2017

---
# <a name="object-oriented-programming-visual-basic"></a>Programmazione orientata agli oggetti (Visual Basic)
Visual Basic fornisce supporto completo perla programmazione orientata agli oggetti inclusi incapsulamento, ereditarietà e polimorfismo.  
  
 *Incapsulamento* indica che un gruppo di proprietà correlate, metodi e gli altri membri vengono considerati come una singola unità o un oggetto.  
  
 *Ereditarietà* descrive la possibilità di creare nuove classi basate su una classe esistente.  
  
 *Polimorfismo* significa che è possibile avere più classi che possono essere utilizzate in modo intercambiabile, anche se ciascuna classe implementa le stesse proprietà o metodi in modi diversi.  
  
 In questa sezione vengono descritti i concetti seguenti:  
  
-   [Classi e oggetti](#Classes)  
  
    -   [Membri di classe](#Members)  
  
         [Proprietà e campi](#Properties)  
  
         [Metodi](#Methods)  
  
         [Costruttori](#Constructors)  
  
         [Distruttori](#Destructors)  
  
         [Eventi](#Events)  
  
         [Classi annidate](#NestedClasses)  
  
    -   [Modificatori di accesso e livelli di accesso](#AccessModifiers)  
  
    -   [Creazione di classi](#InstantiatingClasses)  
  
    -   [Le classi condivise e i membri](#Static)  
  
    -   [Tipi anonimi](#AnonymousTypes)  
  
-   [Ereditarietà](#Inheritance)  
  
    -   [Override di membri](#Overriding)  
  
-   [Interfacce](#Interfaces)  
  
-   [Generics](#Generics)  
  
-   [Delegati](#Delegates)  
  
##  <a name="Classes"></a>Classi e oggetti  
 Le condizioni di *classe* e *oggetto* vengono talvolta utilizzati in modo intercambiabile, ma in realtà, le classi descrivono il *tipo* degli oggetti, mentre gli oggetti sono utilizzabili *istanze* delle classi. L'atto di creare un oggetto viene pertanto chiamato *la creazione di istanze*. Rifacendoci all'analogia precedente, la classe corrisponde al progetto iniziale e l'oggetto all'edificio realizzato in base a tale progetto.  
  
 Per definire una classe:  
  
```vb  
Class SampleClass  
End Class  
```  
  
 Visual Basic fornisce inoltre una versione ridotta delle classi chiamate *strutture* che sono utili quando è necessario creare una matrice di oggetti di grandi dimensioni e si desidera utilizzare una quantità eccessiva di memoria per tale.  
  
 Per definire una struttura:  
  
```vb  
Structure SampleStructure  
End Structure  
```  
  
 Per altre informazioni, vedere:  
  
-   [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)  
  
-   [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
###  <a name="Members"></a>Membri di classe  
 Ogni classe può avere diversi *i membri della classe* che includono proprietà che descrivono dati relativi a classi, metodi che definiscono il comportamento della classe e gli eventi che forniscono la comunicazione tra classi e oggetti diversi.  
  
####  <a name="Properties"></a>Proprietà e campi  
 I campi e le proprietà rappresentano le informazioni contenute in un oggetto. I campi sono simili a variabili in quanto possono essere letti o impostati direttamente.  
  
 Per definire un campo:  
  
```vb  
Class SampleClass  
    Public SampleField As String  
End Class  
```  
  
 Le proprietà dispongono di routine Get e Set, che forniscono un maggiore controllo sul modo in cui i valori vengono impostati o restituiti.  
  
 Visual Basic consente di creare un campo privato per archiviare il valore della proprietà o utilizzare le cosiddette proprietà implementate automaticamente che creano automaticamente questo campo e forniscono la logica di base per le routine di proprietà.  
  
 Per definire una proprietà implementata automaticamente:  
  
```vb  
Class SampleClass  
    Public Property SampleProperty as String  
End Class  
```  
  
 Se è necessario eseguire alcune operazioni aggiuntive per la lettura e la scrittura del valore della proprietà, definire un campo per archiviare il valore della proprietà e fornire la logica di base per archiviarlo e recuperarlo:  
  
```vb  
Class SampleClass  
    Private m_Sample As String  
    Public Property Sample() As String  
        Get  
            ' Return the value stored in the field.  
            Return m_Sample  
        End Get  
        Set(ByVal Value As String)  
            ' Store the value in the field.  
            m_Sample = Value  
        End Set  
    End Property  
End Class  
```  
  
 La maggior parte delle proprietà dispone di metodi o di routine per impostare e ottenere il valore della proprietà. È possibile, tuttavia, creare proprietà di sola lettura o di sola scrittura per impedirne la modifica o la lettura. In Visual Basic è possibile utilizzare le parole chiave `ReadOnly` e `WriteOnly`. Proprietà implementate automaticamente, tuttavia, non può essere in sola lettura o in sola lettura.  
  
 Per altre informazioni, vedere:  
  
-   [Istruzione Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
-   [Istruzione Get](../../../visual-basic/language-reference/statements/get-statement.md)  
  
-   [Istruzione Set](../../../visual-basic/language-reference/statements/set-statement.md)  
  
-   [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)  
  
-   [WriteOnly](../../../visual-basic/language-reference/modifiers/writeonly.md)  
  
####  <a name="Methods"></a>Metodi  
 Oggetto *metodo* che un oggetto può eseguire l'azione.  
  
> [!NOTE]
>  In Visual Basic, è possibile creare un metodo in due modi: se il metodo non restituisce un valore, viene utilizzata l'istruzione `Sub`, se invece un metodo restituisce un valore, viene utilizzata l'istruzione `Function`.  
  
 Per definire un metodo di una classe:  
  
```vb  
Class SampleClass  
    Public Function SampleFunc(ByVal SampleParam As String)  
        ' Add code here  
    End Function  
End Class  
```  
  
 Una classe può avere diverse implementazioni, o *overload*, dello stesso metodo che differiscono per il numero di parametri o tipi di parametro.  
  
 Per essere in rapporto di overload con un metodo:  
  
```vb  
Overloads Sub Display(ByVal theChar As Char)  
    ' Add code that displays Char data.  
End Sub  
Overloads Sub Display(ByVal theInteger As Integer)  
    ' Add code that displays Integer data.  
End Sub  
```  
  
 Nella maggior parte dei casi si dichiara un metodo all'interno di una definizione della classe. Tuttavia, Visual Basic supporta anche *metodi di estensione* che consente di aggiungere metodi a una classe esistente di fuori della definizione effettiva della classe.  
  
 Per altre informazioni, vedere:  
  
-   [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
-   [Istruzione Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
-   [Overload](../../../visual-basic/language-reference/modifiers/overloads.md)  
  
-   [Metodi di estensione](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)  
  
####  <a name="Constructors"></a>Costruttori  
 I costruttori sono metodi di classe che vengono eseguiti automaticamente durante la creazione di un oggetto di un tipo specifico. I costruttori in genere inizializzano i membri dati del nuovo oggetto. Un costruttore può essere eseguito solo una volta alla creazione di una classe. Inoltre, il codice nel costruttore viene sempre eseguito prima di qualsiasi altro codice in una classe. Tuttavia, è possibile creare più overload del costruttore esattamente come per qualsiasi altro metodo.  
  
 Per definire un costruttore per una classe:  
  
```vb  
Class SampleClass  
    Sub New(ByVal s As String)  
        // Add code here.  
    End Sub  
End Class  
```  
  
 Per ulteriori informazioni, vedere: [la durata degli oggetti: come gli oggetti sono creare e distruggere](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md).  
  
####  <a name="Destructors"></a>Distruttori  
 I distruttori sono utilizzati per distruggere istanze di classi. In .NET Framework, il Garbage Collector gestisce l'allocazione e il rilascio di memoria per gli oggetti gestiti di un'applicazione. Potrebbero, tuttavia, essere necessari distruttori per pulire eventuali risorse non gestite create dall'applicazione. Può esistere un solo distruttore per classe.  
  
 Per ulteriori informazioni sui distruttori e garbage collection in .NET Framework, vedere [operazione di Garbage Collection](../../../standard/garbagecollection/index.md).  
  
####  <a name="Events"></a>Eventi  
 Tramite gli eventi una classe o un oggetto sono in grado di segnalare ad altre classi o oggetti una situazione di interesse. La classe che invia (o genera) l'evento viene chiamata il *publisher* e le classi che ricevono (o gestiscono) l'evento sono chiamate *sottoscrittori*. Per ulteriori informazioni sugli eventi, come essi vengono generati e gestiti, vedere [eventi](http://msdn.microsoft.com/library/b6f65241-e0ad-4590-a99f-200ce741bb1f).  
  
-   Per dichiarare gli eventi, utilizzare il [istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md).  
  
-   Per generare eventi, utilizzare il [istruzione RaiseEvent](../../../visual-basic/language-reference/statements/raiseevent-statement.md).  
  
-   Per specificare i gestori eventi utilizzando una modalità dichiarativa, utilizzare il [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md) istruzione e [gestisce](../../../visual-basic/language-reference/statements/handles-clause.md) clausola.  
  
-   Per poter aggiungere, rimuovere e modificare il gestore dell'evento associato a un evento, utilizzare il [AddHandler (istruzione)](../../../visual-basic/language-reference/statements/addhandler-statement.md) e [RemoveHandler (istruzione)](../../../visual-basic/language-reference/statements/removehandler-statement.md) con il [AddressOf (operatore)](../../../visual-basic/language-reference/operators/addressof-operator.md).  
  
####  <a name="NestedClasses"></a>Classi annidate  
 Una classe definita all'interno di un'altra classe è denominata *nidificate*. Per impostazione predefinita, la classe annidata è privata.  
  
```vb  
Class Container  
    Class Nested  
    ' Add code here.  
    End Class  
End Class  
```  
  
 Per creare un'istanza della classe annidata, utilizzare il nome della classe dei contenitori seguita dal punto, quindi dal nome della classe annidata:  
  
```vb  
Dim nestedInstance As Container.Nested = New Container.Nested()  
```  
  
###  <a name="AccessModifiers"></a>Modificatori di accesso e livelli di accesso  
 Tutte le classi e membri di classe possono specificare quale livello di accesso forniscono alle altre classi utilizzando *modificatori di accesso*.  
  
 Sono disponibili i seguenti modificatori di accesso:  
  
|Modificatore di Visual Basic|Definizione|  
|---------------------------|----------------|  
|[Public](../../../visual-basic/language-reference/modifiers/public.md)|Il tipo o il membro è accessibile da altro codice nello stesso assembly o in un altro assembly che vi fa riferimento.|  
|[Private](../../../visual-basic/language-reference/modifiers/private.md)|Il tipo o il membro è accessibile solo dal codice nella stessa classe.|  
|[Protected](../../../visual-basic/language-reference/modifiers/protected.md)|Il tipo o il membro è accessibile solo dal codice nella stessa classe o in una classe derivata.|  
|[Friend](../../../visual-basic/language-reference/modifiers/friend.md)|Il tipo o il membro è accessibile dal codice nello stesso assembly ma non da un altro assembly.|  
|`Protected Friend`|Il tipo o il membro è accessibile dal codice nello stesso assembly o da una classe derivata in un altro assembly.|  
  
 Per ulteriori informazioni, vedere [livelli di accesso in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
###  <a name="InstantiatingClasses"></a>Creazione di classi  
 Per creare un oggetto, è necessario creare un'istanza di una classe.  
  
```vb  
Dim sampleObject as New SampleClass()  
```  
  
 Dopo avere creato un'istanza di una classe, è possibile assegnare i valori alle proprietà e ai campi dell'istanza e richiamare i metodi della classe.  
  
```vb  
' Set a property value.  
sampleObject.SampleProperty = "Sample String"  
' Call a method.  
sampleObject.SampleMethod()  
```  
  
 Per assegnare i valori alle proprietà durante il processo di creazione dell'istanza della classe, utilizzare gli inizializzatori di oggetto:  
  
```vb  
Dim sampleObject = New SampleClass With   
    {.FirstProperty = "A", .SecondProperty = "B"}  
```  
  
 Per altre informazioni, vedere:  
  
-   [Operatore New](../../../visual-basic/language-reference/operators/new-operator.md)  
  
-   [Inizializzatori di oggetto: tipi denominati e tipi anonimi](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)  
  
###  <a name="Static"></a>Le classi condivise e i membri  
 Un membro condiviso della classe è una proprietà, procedura o campo condiviso da tutte le istanze di una classe.  
  
 Per definire un membro condiviso:  
  
```vb  
Class SampleClass  
    Public Shared SampleString As String = "Sample String"  
End Class  
```  
  
 Per accedere al membro condiviso, utilizzare il nome della classe senza creare un oggetto di questa classe:  
  
```vb  
MsgBox(SampleClass.SampleString)  
```  
  
 Moduli condivisi in Visual Basic condiviso solo membri e non possono essere creata un'istanza. Membri condivisi non possono accedere inoltre non condivisi di proprietà, campi o metodi  
  
 Per altre informazioni, vedere:  
  
-   [Shared](../../../visual-basic/language-reference/modifiers/shared.md)  
  
-   [Istruzione Module](../../../visual-basic/language-reference/statements/module-statement.md)  
  
###  <a name="AnonymousTypes"></a>Tipi anonimi  
 I tipi anonimi consentono di creare oggetti senza scrivere una definizione della classe per il tipo di dati. La classe viene generata direttamente dal compilatore. La classe non ha un nome utilizzabile e contiene le proprietà specificate nella dichiarazione dell'oggetto.  
  
 Per creare un'istanza di un tipo anonimo:  
  
```vb  
' sampleObject is an instance of a simple anonymous type.  
Dim sampleObject =   
    New With {Key .FirstProperty = "A", .SecondProperty = "B"}  
```  
  
 Per ulteriori informazioni, vedere: [tipi anonimi](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
##  <a name="Inheritance"></a>Ereditarietà  
 L'ereditarietà permette di creare una nuova classe che riutilizza, estende e modifica il comportamento definito in un'altra classe. La classe i cui membri vengono ereditati è denominata la *classe di base*, mentre la classe che eredita tali membri è denominata la *derivata*. Tuttavia, tutte le classi in Visual Basic ereditano in modo implicito dalla <xref:System.Object>classe che supporta la gerarchia di classi .NET e fornisce servizi di basso livello per tutte le classi.</xref:System.Object>  
  
> [!NOTE]
>  Visual Basic non supporta l'ereditarietà multipla. Vale a dire, è possibile specificare solo una classe base per una classe derivata.  
  
 Per ereditare da una classe base:  
  
```vb  
Class DerivedClass  
    Inherits BaseClass  
End Class  
```  
  
 Per impostazione predefinita, tutte le classi possono essere ereditate. Tuttavia, è possibile specificare se una classe non deve essere utilizzata come classe base oppure creare una classe utilizzabile solo come classe base.  
  
 Per specificare che una classe non può essere utilizzata come classe base:  
  
```vb  
NotInheritable Class SampleClass  
End Class  
```  
  
 Per specificare che una classe può essere utilizzata solo come classe base e che non è possibile crearne un'istanza:  
  
```vb  
MustInherit Class BaseClass  
End Class  
```  
  
 Per altre informazioni, vedere:  
  
-   [Istruzione Inherits](../../../visual-basic/language-reference/statements/inherits-statement.md)  
  
-   [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)  
  
-   [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)  
  
###  <a name="Overriding"></a>Override di membri  
 Per impostazione predefinita, in una classe derivata vengono ereditati tutti i membri della classe base relativa. Se si desidera modificare il comportamento del membro ereditato, è necessario eseguirne l'override. È possibile definire una nuova implementazione del metodo, della proprietà o dell'evento nella classe derivata.  
  
 I seguenti modificatori consentono di controllare le modalità di override di proprietà e metodi:  
  
|Modificatore di Visual Basic|Definizione|  
|---------------------------|----------------|  
|[Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)|Consente a un membro della classe di essere sottoposto a override in una classe derivata.|  
|[Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)|Esegue l'override di un membro virtuale (sottoponibile a override) definito nella classe base.|  
|[NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)|Consente di impedire l'override di un membro in una classe che eredita.|  
|[MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)|Richiede che un membro della classe venga sottoposto a override nella classe derivata.|  
|[Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)|Nasconde un membro ereditato da una classe base.|  
  
##  <a name="Interfaces"></a>Interfacce  
 Le interfacce, come le classi, consentono di definire un insieme di proprietà, metodi ed eventi. A differenza delle classi, però, le interfacce non forniscono l'implementazione. Esse sono infatti implementate dalle classi e definite come entità distinte da queste. Un'interfaccia rappresenta un contratto, in quanto è necessario che una classe che implementa un'interfaccia implementi ogni aspetto esattamente come è stato definito.  
  
 Per definire un'interfaccia:  
  
```vb  
Public Interface ISampleInterface  
    Sub DoSomething()  
End Interface  
```  
  
 Per implementare un'interfaccia in una classe:  
  
```vb  
Class SampleClass  
    Implements ISampleInterface  
    Sub DoSomething  
        ' Method implementation.  
    End Sub  
End Class  
```  
  
 Per altre informazioni, vedere:  
  
-   [Interfacce](../../../visual-basic/programming-guide/language-features/interfaces/index.md)  
  
-   [Istruzione Interface](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
-   [Istruzione Implements](../../../visual-basic/language-reference/statements/implements-statement.md)  
  
##  <a name="Generics"></a>Generics  
 Classi, strutture, interfacce e metodi in .NET Framework possono includere *parametri di tipo* che definiscono i tipi di oggetti che possono archiviare o utilizzare. L'esempio più comune di generics è una raccolta, dove è possibile specificare il tipo di oggetti da archiviare in una raccolta.  
  
 Per definire una classe generica:  
  
```vb  
Class SampleGeneric(Of T)  
    Public Field As T  
End Class  
```  
  
 Per creare un'istanza di una classe generica:  
  
```vb  
Dim sampleObject As New SampleGeneric(Of String)  
sampleObject.Field = "Sample string"  
```  
  
 Per altre informazioni, vedere:  
  
-   [Generics](https://msdn.microsoft.com/library/ms172192)  
  
-   [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)  
  
##  <a name="Delegates"></a>Delegati  
 Oggetto *delegare* è un tipo che definisce una firma di metodo e può fornire un riferimento a qualsiasi metodo con una firma compatibile. Tramite il delegato è possibile invocare (o chiamare) il metodo. I delegati vengono utilizzati per passare metodi come argomenti ad altri metodi.  
  
> [!NOTE]
>  I gestori di evento non sono altro che metodi richiamati tramite delegati. Per ulteriori informazioni sull'utilizzo dei delegati nella gestione degli eventi, vedere [eventi](http://msdn.microsoft.com/library/b6f65241-e0ad-4590-a99f-200ce741bb1f).  
  
 Per creare un delegato:  
  
```vb  
Delegate Sub SampleDelegate(ByVal str As String)  
```  
  
 Per creare un riferimento a un metodo che corrisponde alla firma specificata dal delegato:  
  
```vb  
Class SampleClass  
    ' Method that matches the SampleDelegate signature.  
    Sub SampleSub(ByVal str As String)  
        ' Add code here.  
    End Sub  
    ' Method that instantiates the delegate.  
    Sub SampleDelegateSub()  
        Dim sd As SampleDelegate = AddressOf SampleSub  
        sd("Sample string")  
    End Sub  
End Class  
```  
  
 Per altre informazioni, vedere:  
  
-   [Delegati](../../../visual-basic/programming-guide/language-features/delegates/index.md)  
  
-   [Istruzione Delegate](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
-   [Operatore AddressOf](../../../visual-basic/language-reference/operators/addressof-operator.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori Visual Basic](../../../visual-basic/programming-guide/index.md)
