---
title: "Modelli di costruttore sicuri per DependencyObject | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modelli di costruttore per DependencyObject"
  - "DependencyObject, modelli di costruttore"
  - "FXCop (strumento)"
ms.assetid: f704b81c-449a-47a4-ace1-9332e3cc6d60
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Modelli di costruttore sicuri per DependencyObject
In genere, i costruttori di classe non devono chiamare callback quali metodi virtuali o delegati, in quanto possono essere chiamati come inizializzazione di base di costruttori per una classe derivata.  L'utilizzo di elementi virtuali può avvenire a un stato incompleto dell'inizializzazione di qualsiasi dato oggetto.  Tuttavia, il sistema di proprietà stesso chiama ed espone internamente i callback come parte del sistema di proprietà di dipendenza.  Un'operazione semplice quale l'impostazione del valore di una proprietà di dipendenza con la chiamata di <xref:System.Windows.DependencyObject.SetValue%2A> potrebbe includere un callback in un punto qualsiasi del processo di determinazione.  Per questa ragione, è necessario impostare i valori delle proprietà di dipendenza all'interno del corpo di un costruttore con una certa attenzione, in quanto tale operazione può divenire problematica se il tipo viene utilizzato come classe di base.  Di seguito, viene documentato un modello particolare per l'implementazione di costruttori <xref:System.Windows.DependencyObject> che evitano problemi specifici con gli stati delle proprietà di dipendenza e i callback inerenti.  
  
   
  
<a name="Property_System_Virtual_Methods"></a>   
## Metodi virtuali del sistema di proprietà  
 I metodi virtuali o callback seguenti vengono chiamati potenzialmente durante i calcoli della chiamata a <xref:System.Windows.DependencyObject.SetValue%2A> che imposta un valore della proprietà di dipendenza: <xref:System.Windows.ValidateValueCallback>, <xref:System.Windows.PropertyChangedCallback>, <xref:System.Windows.CoerceValueCallback>, <xref:System.Windows.DependencyObject.OnPropertyChanged%2A>.  Ognuno di questi metodi virtuali o callback serve a uno scopo particolare nell'espansione della versatilità del sistema di proprietà [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] e delle proprietà di dipendenza.  Per ulteriori informazioni sulla modalità di utilizzo di questi elementi virtuali allo scopo di personalizzare la determinazione del valore della proprietà, vedere [Callback e convalida delle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md).  
  
### Confronto tra l'imposizione della regola FXCop eMetodi virtuali del sistema di proprietà  
 Se si utilizza lo strumento Microsoft FXCop come parte del processo di compilazione e si effettua la derivazione da determinate classi del framework [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che chiamano il costruttore di base o si implementano le proprietà di dipendenza personalizzate sulle classi derivate, è possibile che si verifichi la violazione di una particolare regola FXCop.  La stringa del nome di questa violazione è:  
  
 `DoNotCallOverridableMethodsInConstructors`  
  
 Si tratta di una regola che fa parte dell'insieme di regole pubblico predefinito per FXCop.  È possibile che questa regola segnali una traccia tramite il sistema di proprietà di dipendenza che eventualmente chiama il metodo virtuale di un sistema di proprietà di dipendenza.  La violazione di questa regola potrebbe continuare ad apparire persino dopo avere seguito i modelli del costruttore raccomandati illustrati in questo argomento, pertanto potrebbe essere necessario disabilitare o eliminare la regola nella configurazione dell'insieme di regole FXCop.  
  
### La maggior parte dei problemi è causata dalla derivazione delle classi e dal mancato utilizzo delle classi esistenti  
 I problemi segnalati da questa regola si verificano quando una classe implementata con i metodi virtuali nella relativa sequenza di costruzione viene successivamente derivata.  Se la classe viene contrassegnata come sealed oppure si sa o si decide che la classe non sarà derivata, le considerazioni qui illustrate e i problemi che hanno motivato la regola FXCop non si applicano a questa situazione.  Tuttavia, se si stanno creando classi in modo che vengano utilizzate come classi di base, ad esempio se si stanno creando dei modelli o un insieme di librerie di controlli espandibile, è necessario seguire i modelli consigliati in questo argomento relativamente ai costruttori.  
  
### I costruttori predefiniti devono inizializzare tutti i valori richiesti dai callback  
 Tutti i membri dell'istanza utilizzati dagli override o dai callback della classe \(i callback dall'elenco della sezione relativa agli elementi virtuali del sistema di proprietà\) devono essere inizializzati all'interno del costruttore predefinito della classe, anche se alcuni di quei valori sono valori "reali" di parametri di costruttori non predefiniti.  
  
 L'esempio di codice seguente \(e gli esempi successivi\) è un esempio di pseudo codice C\# nel quale questa regola viene violata e in cui viene illustrato il problema:  
  
```  
public class MyClass : DependencyObject  
{  
    public MyClass() {}  
    public MyClass(object toSetWobble)  
        : this()  
    {  
        Wobble = toSetWobble; //this is backed by a DependencyProperty  
        _myList = new ArrayList();    // this line should be in the default ctor  
    }  
    public static readonly DependencyProperty WobbleProperty =   
        DependencyProperty.Register("Wobble", typeof(object), typeof(MyClass));  
    public object Wobble  
    {  
        get { return GetValue(WobbleProperty); }  
        set { SetValue(WobbleProperty, value); }  
    }  
    protected override void OnPropertyChanged(DependencyPropertyChangedEventArgs e)  
    {  
        int count = _myList.Count;    // null-reference exception  
    }  
    private ArrayList _myList;  
}  
```  
  
 Quando il codice dell'applicazione chiama `new MyClass(objectvalue)`, questo a sua volta chiama il costruttore predefinito e i costruttori della classe di base.  Successivamente imposta `Property1 = object1`, che chiama il metodo virtuale `OnPropertyChanged` sull'oggetto <xref:System.Windows.DependencyObject> `MyClass` proprietario.  L'override fa riferimento a `_myList`, che non è stato ancora inizializzato.  
  
 Un modo per evitare questi problemi consiste nell'assicurarsi che i callback utilizzino solo altre proprietà di dipendenza e che ciascuna di tali proprietà di dipendenza disponga di un valore predefinito stabilito come parte dei relativi metadati registrati.  
  
<a name="Safe_Constructor_Patterns"></a>   
## Modelli di costruttore sicuri  
 Per evitare i rischi di un'inizializzazione incompleta nel caso in cui la classe sia utilizzata come classe di base, seguire questi modelli:  
  
#### Costruttori predefiniti che chiamano l'inizializzazione di base  
 Implementare questi costruttori che chiamano l'impostazione predefinita di base:  
  
```  
public MyClass : SomeBaseClass {  
    public MyClass() : base() {  
        // ALL class initialization, including initial defaults for   
        // possible values that other ctors specify or that callbacks need.  
    }  
}  
```  
  
#### Costruttori non predefiniti \(a scelta\), che non corrispondono ad alcuna firma di base  
 Se questi costruttori utilizzano dei parametri per impostare le proprietà di dipendenza nell'inizializzazione, chiamare innanzitutto il costruttore predefinito della propria classe per l'inizializzazione, quindi utilizzare i parametri per impostare le proprietà di dipendenza.  Tali proprietà potrebbero essere proprietà di dipendenza definite dalla classe o proprietà di dipendenza ereditate dalle classi di base; tuttavia, in entrambi i casi utilizzare il modello seguente:  
  
```  
public MyClass : SomeBaseClass {  
    public MyClass(object toSetProperty1) : this() {  
        // Class initialization NOT done by default.  
        // Then, set properties to values as passed in ctor parameters.  
        Property1 = toSetProperty1;  
    }  
}  
```  
  
#### Costruttori non predefiniti \(a scelta\), che corrispondono alle firme di base  
 Anziché chiamare il costruttore di base con la stessa applicazione di parametri, chiamare nuovamente il costruttore predefinito della propria classe.  Non chiamare l'inizializzatore di base; al contrario, è necessario chiamare `this()`.  A questo punto riprodurre il comportamento del costruttore originale utilizzando i parametri passati come valori per l'impostazione delle proprietà rilevanti.  Per informazioni sulla definizione delle proprietà che si desidera impostare tramite determinati parametri, utilizzare la documentazione originale del costruttore di base:  
  
```  
public MyClass : SomeBaseClass {  
    public MyClass(object toSetProperty1) : this() {  
        // Class initialization NOT done by default.  
        // Then, set properties to values as passed in ctor parameters.  
        Property1 = toSetProperty1;  
    }  
}  
```  
  
#### Deve corrispondere a tutte le firme  
 Per i casi in cui il tipo di base dispone di più firme, è necessario associare tutte le firme possibili a un'implementazione personalizzata del costruttore che utilizza il modello di chiamata del costruttore predefinito della classe consigliato prima di impostare ulteriori proprietà.  
  
#### Impostazione delle proprietà di dipendenza con SetValue  
 Questi stessi modelli si applicano se si sta impostando una proprietà che non dispone di un wrapper per un'impostazione pratica delle proprietà, per cui i valori vengono impostati con <xref:System.Windows.DependencyObject.SetValue%2A>.  Le chiamate a <xref:System.Windows.DependencyObject.SetValue%2A> che passano tramite parametri di costruttore devono inoltre chiamare il costruttore predefinito della classe per l'inizializzazione.  
  
## Vedere anche  
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Sicurezza della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-security.md)