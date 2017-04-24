---
title: "Spazi dei nomi XAML e mapping dello spazio dei nomi per XAML WPF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assembly, mapping di spazi dei nomi"
  - "classi, mapping di spazi dei nomi"
  - "classi personalizzate, mapping di spazi dei nomi"
  - "mapping di spazi dei nomi"
  - "spazi dei nomi (mapping)"
  - "spazi dei nomi"
  - "XAML, spazi dei nomi (mapping)"
  - "XAML, spazi dei nomi"
ms.assetid: 5c0854e3-7470-435d-9fe2-93eec9d3634e
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Spazi dei nomi XAML e mapping dello spazio dei nomi per XAML WPF
In questo argomento vengono illustrati la presenza e lo scopo dei due mapping dello spazio dei nomi XAML nel tag radice di ogni file XAML WPF.  Viene inoltre illustrato come produrre mapping simili per l'utilizzo di elementi definiti nel codice e\/o all'interno di assembly separati.  
  
   
  
## Definizione di spazio dei nomi XAML  
 Uno spazio dei nomi XAML è in realtà un'estensione del concetto di uno spazio dei nomi XML.  Le tecniche di specifica di uno spazio dei nomi XAML si basano sulla sintassi dello spazio dei nomi XML, sulla convenzione dell'utilizzo di URI come identificatori dello spazio dei nomi, sull'utilizzo di prefissi per fare riferimento a più spazi dei nomi dalla stessa origine del markup e così via.  Il concetto principale aggiunto alla definizione XAML dello spazio dei nomi XML consiste nel fatto che uno spazio dei nomi XAML implica un ambito di univocità per gli utilizzi del markup e influenza il modo in cui le entità del markup vengono potenzialmente supportate da spazi dei nomi e da assembly di riferimento CLR specifici.  Questa seconda considerazione viene inoltre influenzata dal concetto di un contesto dello schema XAML.  Tuttavia per quanto riguarda il funzionamento di WPF rispetto agli spazi dei nomi XAML, è possibile considerare gli spazi dei nomi XAML nei termini di uno spazio dei nomi XAML predefinito, dello spazio dei nomi del linguaggio XAML e di qualsiasi ulteriore spazio dei nomi XAML mappato direttamente dal markup XAML agli spazi dei nomi e agli assembly di riferimento CLR di supporto specifici.  
  
<a name="The_WPF_and_XAML_Namespace_Declarations"></a>   
## Dichiarazioni dello spazio dei nomi XAML e WPF  
 All'interno delle dichiarazioni dello spazio dei nomi nel tag radice di molti file XAML in genere sono presenti due dichiarazioni di spazi dei nomi XML.  La prima dichiarazione esegue il mapping dello spazio dei nomi del client WPF complessivo o del framework XAML come predefinito:  
  
 `xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`  
  
 La seconda dichiarazione esegue il mapping di uno spazio dei nomi XAML separato, in genere al prefisso `x:`.  
  
 `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`  
  
 La relazione tra queste dichiarazioni consiste nel fatto che il mapping del prefisso `x:` supporta intrinseci che fanno parte della definizione di linguaggio di XAML e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è un'implementazione che utilizza XAML come linguaggio e definisce un vocabolario degli oggetti per XAML.  Poiché gli utilizzi del vocabolario WPF sono in genere molto più frequenti degli utilizzi degli intrinseci XAML, il vocabolario WPF viene mappato come predefinito.  
  
 La convenzione del prefisso `x:` per il mapping del supporto degli intrinseci del linguaggio XAML viene rispettata dai modelli di progetto, dal codice di esempio e dalla documentazione delle funzionalità del linguaggio nel presente [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)].  Lo spazio dei nomi XAML definisce molte funzionalità di utilizzo comune, necessarie anche per le applicazioni WPF di base.  Ad esempio, per unire code\-behind a un file XAML tramite una classe parziale, è necessario denominare la classe come attributo `x:Class` nell'elemento radice del file XAML relativo.  In alternativa, per qualsiasi elemento definito in una pagina XAML a cui si desidera accedere come risorsa con chiave è necessario che l'attributo `x:Key` sia impostato sull'elemento in questione.  Per ulteriori informazioni su questi e altri aspetti di XAML, vedere [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md) o [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
<a name="Mapping_To_Custom_Classes_and_Assemblies"></a>   
## Mapping a classi e assembly personalizzati  
 È possibile eseguire il mapping di spazi dei nomi XML ad assembly utilizzando una serie di token all'interno di una dichiarazione di prefisso `xmlns`, eseguendo una procedura analoga a quella del mapping degli spazi dei nomi WPF e XAML degli intrinseci XAML standard ai prefissi.  
  
 La sintassi accetta i token denominati e i valori riportati di seguito:  
  
 `clr-namespace:` lo spazio dei nomi CLR dichiarato nell'assembly che contiene i tipi pubblici da esporre come elementi.  
  
 `assembly=`: l'assembly che contiene l'intero spazio dei nomi [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] a cui si fa riferimento, o parte di esso.  Il valore è dato in genere dal nome dell'assembly, non dal percorso, e non include l'estensione \(ad esempio, dll o exe\).  Il percorso dell'assembly deve essere stabilito come riferimento al progetto nel file di progetto che contiene il codice XAML di cui si sta tentando di eseguire il mapping.  Per incorporare il controllo delle versioni e la firma con nome sicuro, il valore dell'`assembly` può essere dato da una stringa, come definito nell'oggetto <xref:System.Reflection.AssemblyName>, anziché da un semplice nome di stringa.  
  
 Si noti che il carattere che separa il token `clr-namespace`  dal valore è il segno di due punti \(:\), mentre il carattere che separa il token `assembly` dal valore è un segno di uguale \(\=\).  Il carattere da utilizzare tra i due token è il segno di punto e virgola.  Non includere inoltre spazi vuoti in alcun punto della dichiarazione.  
  
### Esempio base di mapping personalizzato  
 Nel codice seguente viene definita una classe personalizzata di esempio:  
  
```csharp  
namespace SDKSample {  
    public class ExampleClass : ContentControl {  
        public ExampleClass() {  
        ...  
        }  
    }  
}  
```  
  
```vb  
Namespace SDKSample  
    Public Class ExampleClass  
        Inherits ContentControl  
         ...  
        Public Sub New()  
        End Sub  
    End Class  
End Namespace  
```  
  
 La classe personalizzata viene quindi compilata in una libreria che, in base alle impostazioni del progetto \(non visualizzate\), è denominata `SDKSampleLibrary`.  
  
 Per fare riferimento a tale classe personalizzata, è anche necessario includerla come riferimento per il progetto corrente, operazione in genere effettuata tramite l'interfaccia utente di Esplora soluzioni in Visual Studio.  
  
 Ora che si dispone di una libreria contenente una classe e di un riferimento a questa nelle impostazioni del progetto, è possibile aggiungere il mapping del prefisso seguente come parte dell'elemento radice in XAML:  
  
 `xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary"`  
  
 Riepilogando, il seguente codice XAML include il mapping personalizzato insieme al mapping predefinito e al mapping del prefisso x: consueti nel tag radice, quindi utilizza un riferimento con prefisso per creare un'istanza di `ExampleClass` in tale interfaccia utente:  
  
```xaml  
<Page x:Class="WPFApplication1.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"   
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary">  
  ...  
  <custom:ExampleClass/>  
...  
</Page>  
```  
  
### Mapping ad assembly correnti  
 È possibile omettere `assembly` se `clr-namespace` a cui si fa riferimento è definito all'interno dello stesso assembly del codice dell'applicazione che fa riferimento alle classi personalizzate.  In alternativa, una sintassi equivalente appropriata consiste nello specificare `assembly=` senza token di stringa dopo il segno di uguale.  
  
 Non è possibile utilizzare le classi personalizzate come elemento radice di una pagina se definite nello stesso assembly.  Non è necessario eseguire il mapping delle classi parziali, ma solo di quelle che non costituiscono la classe parziale di una pagina dell'applicazione se si intende fare riferimento a esse come elementi in XAML.  
  
<a name="Mapping_CLR_Namespaces_to_XML_Namespaces_in_an"></a>   
## Mapping di spazi dei nomi CLR a spazi dei nomi XML in un assembly  
 WPF definisce un attributo CLR che viene utilizzato dai processori XAML per eseguire il mapping di più spazi dei nomi CLR a un singolo spazio dei nomi XAML.  L'attributo <xref:System.Windows.Markup.XmlnsDefinitionAttribute> viene posizionato al livello dell'assembly nel codice sorgente che produce l'assembly.  Nel codice sorgente dell'assembly WPF questo attributo viene utilizzato per eseguire il mapping di diversi spazi dei nomi comuni, quali <xref:System.Windows> e <xref:System.Windows.Controls>, allo spazio dei nomi [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)].  
  
 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> accetta due parametri: il nome dello spazio dei nomi XML\/XAML e quello dello spazio dei nomi CLR.  Possono esistere più <xref:System.Windows.Markup.XmlnsDefinitionAttribute> per eseguire il mapping di più spazi dei nomi CLR allo stesso spazio dei nomi XML.  Dopo avere eseguito il mapping, è possibile fare riferimento ai membri degli spazi dei nomi senza nome completo fornendo l'istruzione `using` appropriata nella pagina code\-behind di classe parziale.  Per informazioni dettagliate, vedere <xref:System.Windows.Markup.XmlnsDefinitionAttribute>.  
  
## Spazi dei nomi della finestra di progettazione e altri prefissi di modelli XAML  
 Se si lavora con ambienti di sviluppo e\/o con strumenti di progettazione per XAML WPF, si può notare che all'interno del markup XAML esistono altri spazi dei nomi XAML definiti o altri prefissi.  
  
 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] utilizza uno spazio dei nomi della finestra di progettazione in genere mappato al prefisso `d:`.  I più recenti modelli di progetto per WPF potrebbero eseguire preventivamente il mapping di questo spazio dei nomi XAML per supportare lo scambio di XAML tra [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] e altri ambienti di progettazione.  Questo spazio dei nomi XAML di progettazione è utilizzato per trasmettere lo stato di progettazione durante la sequenza di andata e ritorno dell'interfaccia utente basata su XAML nella finestra di progettazione.  Questo spazio dei nomi viene utilizzato inoltre per funzionalità quali `d:IsDataSource` che consentono origini dati di runtime in una finestra di progettazione.  
  
 Un altro prefisso che si potrebbe vedere mappato è `mc:`.  `mc:` è finalizzato alla compatibilità del markup e utilizza un modello di compatibilità del markup non necessariamente specifico di XAML.  In alcuni casi, è possibile utilizzare le funzionalità di compatibilità del markup per scambiare XAML tra framework o tra altri limiti di implementazione di supporto, per lavorare tra contesti di schemi XAML, per fornire compatibilità per modalità limitate nelle finestre di progettazione e così via.  Per ulteriori informazioni sui concetti di compatibilità del markup e sulla modalità di relazione con WPF, vedere [Funzionalità del linguaggio per la compatibilità dei markup \(mc:\)](../../../../docs/framework/wpf/advanced/markup-compatibility-mc-language-features.md).  
  
## WPF e caricamento di assembly  
 Il contesto dello schema XAML per WPF è integrato al modello dell'applicazione WPF, in cui si utilizza il concetto di <xref:System.AppDomain> definito da CLR.  La sequenza riportata di seguito descrive come un contesto dello schema XAML interpreta la modalità di caricamento degli assembly o di ricerca dei tipi in fase di esecuzione o di progettazione, in base all'utilizzo da parte di WPF di <xref:System.AppDomain> e altri fattori.  
  
1.  Scorrere <xref:System.AppDomain> cercando un assembly già caricato che corrisponde a tutti gli aspetti del nome, a partire dall'assembly caricato più recentemente.  
  
2.  Se il nome è completo, chiamare <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName> sul nome completo.  
  
3.  Se la combinazione nome breve e token di chiave pubblica di un nome completo corrisponde all'assembly da cui è stato caricato il markup, restituire tale assembly.  
  
4.  Utilizzare nome breve e token di chiave pubblica per chiamare <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>.  
  
5.  Se il nome non è completo, chiamare <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>.  
  
 Per il codice XAML separato non viene utilizzato il passaggio 3. Non è presente alcun assembly da cui effettuare il caricamento.  
  
 Il codice XAML compilato per WPF \(generato tramite XamlBuildTask\) non utilizza gli assembly già caricati da <xref:System.AppDomain> \(passaggio 1\).  Inoltre, il nome non deve mai essere non qualificato dall'output XamlBuildTask, pertanto il passaggio 5 non viene applicato.  
  
 Il codice BAML \(generato tramite PresentationBuildTask\) utilizza tutti i passaggi, sebbene non debba contenere nomi di assembly non qualificati.  
  
## Vedere anche  
 [Informazioni sugli spazi dei nomi XML](http://go.microsoft.com/fwlink/?LinkId=98069)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)