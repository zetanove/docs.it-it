---
title: "Automazione interfaccia utente di un controllo personalizzato WPF | Microsoft Docs"
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
  - "controlli personalizzati [WPF], l'applicazione di automazione interfaccia utente"
  - "accessibilità [WPF], l'applicazione a controlli personalizzati"
  - "miglioramento dell'accesso facilitato controlli personalizzati [WPF]"
  - "Automazione interfaccia utente [WPF], utilizzo con controlli personalizzati"
ms.assetid: 47b310fc-fbd5-4ce2-a606-22d04c6d4911
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 34
---
# Automazione interfaccia utente di un controllo personalizzato WPF
[!INCLUDE[TLA#tla_uiautomation](../../../../includes/tlasharptla-uiautomation-md.md)]fornisce una singola interfaccia generalizzata che i client possono utilizzare per esaminare o gestire le interfacce utente di una varietà di piattaforme e Framework di automazione. [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]Abilita le applicazioni di accessibilità, ad esempio gli screen reader per esaminare gli elementi dell'interfaccia utente e simularne l'interazione dell'utente da altro codice sia il codice di qualità (test). Per informazioni su [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] per tutte le piattaforme, vedere Accesso facilitato.  
  
 In questo argomento viene descritto come implementare un provider di automazione interfaccia utente lato server per un controllo personalizzato che viene eseguito in un'applicazione WPF. WPF supporta [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] una struttura ad albero di oggetti peer di automazione che affianca la struttura ad albero di elementi dell'interfaccia utente. Codice di test e le applicazioni che forniscono funzionalità di accessibilità possono utilizzare gli oggetti peer di automazione direttamente (per il codice in-process) o tramite l'interfaccia generalizzata fornita da [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)].  
  
 
  
<a name="AutomationPeerClasses"></a>   
## <a name="automation-peer-classes"></a>Classi Peer di automazione  
 Supporto di controlli WPF [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] tramite una struttura di classi peer che derivano da <xref:System.Windows.Automation.Peers.AutomationPeer>. Per convenzione, i nomi delle classi peer iniziano con il nome di classe di controllo e terminano con "AutomationPeer". Ad esempio, <xref:System.Windows.Automation.Peers.ButtonAutomationPeer> è la classe peer per la <xref:System.Windows.Controls.Button> classe del controllo. Le classi peer equivalgono approssimativamente alle [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] tipi di controllo ma sono specifiche [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] elementi. Codice di automazione che accede alle applicazioni WPF tramite il [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] interfaccia non utilizza direttamente i peer di automazione, ma il codice di automazione nello stesso spazio di processo può utilizzare direttamente peer di automazione.  
  
<a name="BuiltInAutomationPeerClasses"></a>   
## <a name="built-in-automation-peer-classes"></a>Classi Peer di automazione incorporato  
 Gli elementi implementano una classe peer di automazione se accettano l'attività dell'interfaccia da parte dell'utente, o se contengono informazioni necessarie per gli utenti di applicazioni di lettura dello schermo. Non tutti gli elementi visivi di WPF sono peer di automazione. Esempi di classi che implementano i peer di automazione sono <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.TextBox>, e <xref:System.Windows.Controls.Label>. Esempi di classi che implementano i peer di automazione sono classi che derivano da <xref:System.Windows.Controls.Decorator>, ad esempio <xref:System.Windows.Controls.Border>e le classi basate su <xref:System.Windows.Controls.Panel>, ad esempio <xref:System.Windows.Controls.Grid> e <xref:System.Windows.Controls.Canvas>.  
  
 La base <xref:System.Windows.Controls.Control> classe dispone di una classe peer corrispondente. Se è necessaria una classe peer corrispondente a un controllo personalizzato che deriva da <xref:System.Windows.Controls.Control>, è necessario derivare la classe peer personalizzata da <xref:System.Windows.Automation.Peers.FrameworkElementAutomationPeer>.  
  
<a name="SecurityConsiderations"></a>   
## <a name="security-considerations-for-derived-peers"></a>Considerazioni sulla sicurezza per peer derivati  
 Peer di automazione devono essere eseguiti in un ambiente parzialmente attendibile. Il codice nell'assembly UIAutomationClient non è configurato per l'esecuzione in un ambiente parzialmente attendibile e il codice di peer di automazione non deve fare riferimento a tale assembly. Utilizzare invece le classi nell'assembly UIAutomationTypes. Ad esempio, è necessario utilizzare il <xref:System.Windows.Automation.AutomationElementIdentifiers> dell'assembly UIAutomationTypes, che corrisponde alla classe di <xref:System.Windows.Automation.AutomationElement> classe nell'assembly UIAutomationClient. È possibile fare riferimento all'assembly UIAutomationTypes nel codice di peer di automazione.  
  
<a name="PeerNavigation"></a>   
## <a name="peer-navigation"></a>Spostamento tra peer  
 Dopo aver individuato un peer di automazione, il codice in-process può passare la struttura ad albero peer chiamando l'oggetto <xref:System.Windows.Automation.Peers.AutomationPeer.GetChildren%2A> e <xref:System.Windows.Automation.Peers.AutomationPeer.GetParent%2A> metodi. Lo spostamento tra [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] elementi all'interno di un controllo è supportato dall'implementazione del peer di <xref:System.Windows.Automation.Peers.AutomationPeer.GetChildrenCore%2A> metodo. Il sistema di automazione interfaccia utente chiama questo metodo per compilare una struttura ad albero di sottoelementi contenuti all'interno di un controllo. ad esempio, elementi dell'elenco in una casella di riepilogo. Il valore predefinito <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetChildrenCore%2A?displayProperty=fullName> metodo attraversa la struttura ad albero di elementi per creare la struttura dei peer di automazione. Controlli personalizzati di eseguire l'override del metodo per esporre gli elementi figlio ai client di automazione, restituendo i peer di automazione di elementi che contengono le informazioni o consentono l'interazione dell'utente.  
  
<a name="Customizations"></a>   
## <a name="customizations-in-a-derived-peer"></a>Personalizzazioni in un Peer derivato  
 Tutte le classi che derivano da <xref:System.Windows.UIElement> e <xref:System.Windows.ContentElement> contengono il metodo virtuale protetto <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A>. WPF chiama <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> per ottenere l'oggetto peer di automazione per ogni controllo. Codice di automazione possa utilizzare il peer per ottenere informazioni sulle funzionalità e caratteristiche di un controllo e per simulare l'utilizzo interattivo. È necessario eseguire l'override di un controllo personalizzato che supporta l'automazione <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> e restituire un'istanza di una classe che deriva da <xref:System.Windows.Automation.Peers.AutomationPeer>. Ad esempio, se un controllo personalizzato deriva il <xref:System.Windows.Controls.Primitives.ButtonBase> (classe), quindi l'oggetto restituito da <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> deve derivare da <xref:System.Windows.Automation.Peers.ButtonBaseAutomationPeer>.  
  
 Quando si implementa un controllo personalizzato, è necessario sostituire i metodi "Core" dalla classe peer di automazione di base che descrivono il comportamento specifico per il controllo personalizzato e univoco.  
  
### <a name="override-oncreateautomationpeer"></a>Override di OnCreateAutomationPeer  
 Eseguire l'override di <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> metodo per il controllo personalizzato in modo che restituisca l'oggetto provider, che deve derivare direttamente o indirettamente da <xref:System.Windows.Automation.Peers.AutomationPeer>.  
  
### <a name="override-getpattern"></a>Override di GetPattern  
 Peer di automazione semplificano alcuni aspetti di implementazione di server-side [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] provider, ma i peer di automazione di controlli personalizzati devono comunque gestire le interfacce dei pattern. Come i provider non WPF, i peer supportano i pattern di controllo fornendo le implementazioni di interfacce di <xref:System.Windows.Automation.Provider?displayProperty=fullName> spazio dei nomi, ad esempio <xref:System.Windows.Automation.Provider.IInvokeProvider>. Le interfacce di pattern di controllo possono essere implementate dal peer stesso o da un altro oggetto. Implementazione del peer <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> restituisce l'oggetto che supporta il modello specificato. [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]codice chiama il <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> (metodo) e specifica un <xref:System.Windows.Automation.Peers.PatternInterface> valore di enumerazione. La sostituzione di <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> deve restituire l'oggetto che implementa il pattern specificato. Se il controllo non ha un'implementazione personalizzata di un modello, è possibile chiamare l'implementazione del tipo di base di <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> per recuperare la relativa implementazione o null se il modello non è supportato per questo tipo di controllo. Ad esempio, è possibile impostare un controllo NumericUpDown personalizzato su un valore all'interno di un intervallo, in modo relativo [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] peer implementi il <xref:System.Windows.Automation.Provider.IRangeValueProvider> interfaccia. L'esempio seguente viene illustrato come del peer <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> metodo sottoposto a override per rispondere a un <xref:System.Windows.Automation.Peers.PatternInterface?displayProperty=fullName> valore.  
  
 [!code-csharp[CustomControlNumericUpDown#GetPattern](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#getpattern)]
 [!code-vb[CustomControlNumericUpDown#GetPattern](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#getpattern)]  
  
 Oggetto <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> metodo può anche specificare un sottoelemento come provider del pattern. Il codice seguente illustra come <xref:System.Windows.Controls.ItemsControl> i trasferimenti di scorrere la gestione del pattern per il peer di interno <xref:System.Windows.Controls.ScrollViewer> controllo.  
  
```csharp  
public override object GetPattern(PatternInterface patternInterface)  
{  
    if (patternInterface == PatternInterface.Scroll)  
    {  
        ItemsControl owner = (ItemsControl) base.Owner;  
  
        // ScrollHost is internal to the ItemsControl class  
        if (owner.ScrollHost != null)  
        {  
            AutomationPeer peer = UIElementAutomationPeer.CreatePeerForElement(owner.ScrollHost);  
            if ((peer != null) && (peer is IScrollProvider))  
            {  
                peer.EventsSource = this;  
                return (IScrollProvider) peer;  
            }  
        }  
    }  
    return base.GetPattern(patternInterface);  
}  
```  
  
```vb  
Public Class Class1  
    Public Overrides Function GetPattern(ByVal patternInterface__1 As PatternInterface) As Object  
        If patternInterface1 = PatternInterface.Scroll Then  
            Dim owner As ItemsControl = DirectCast(MyBase.Owner, ItemsControl)  
  
            ' ScrollHost is internal to the ItemsControl class  
            If owner.ScrollHost IsNot Nothing Then  
                Dim peer As AutomationPeer = UIElementAutomationPeer.CreatePeerForElement(owner.ScrollHost)  
                If (peer IsNot Nothing) AndAlso (TypeOf peer Is IScrollProvider) Then  
                    peer.EventsSource = Me  
                    Return DirectCast(peer, IScrollProvider)  
                End If  
            End If  
        End If  
        Return MyBase.GetPattern(patternInterface1)  
    End Function  
End Class  
```  
  
 Per specificare un sottoelemento per la gestione del pattern, questo codice recupera l'oggetto del sottoelemento, crea un peer tramite il <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.CreatePeerForElement%2A> (metodo), imposta il <xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A> proprietà del nuovo peer sul peer corrente e restituisce il nuovo peer. L'impostazione <xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A> su un sottoelemento impedisce il sottoelemento nella struttura a albero peer e definisce tutti gli eventi generati dal sottoelemento come provenienti dal controllo specificato <xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A>. Il <xref:System.Windows.Controls.ScrollViewer> controllo non viene visualizzato nella struttura ad albero di automazione e gli eventi di scorrimento che genera sembrano provenire dal <xref:System.Windows.Controls.ItemsControl> oggetto.  
  
### <a name="override-core-methods"></a>Eseguire l'override di metodi "Core"  
 Il codice di automazione ottiene informazioni sul controllo chiamando i metodi pubblici della classe peer. Per fornire informazioni sul controllo, l'override di ogni metodo il cui nome termina con "Core" quando l'implementazione del controllo differisce da quella fornita dalla classe peer di automazione di base. Come minimo, il controllo deve implementare il <xref:System.Windows.Automation.Peers.AutomationPeer.GetClassNameCore%2A> e <xref:System.Windows.Automation.Peers.AutomationPeer.GetAutomationControlTypeCore%2A> metodi, come illustrato nell'esempio seguente.  
  
 [!code-csharp[CustomControlNumericUpDown#CoreOverrides](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#coreoverrides)]
 [!code-vb[CustomControlNumericUpDown#CoreOverrides](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#coreoverrides)]  
  
 L'implementazione di <xref:System.Windows.Automation.Peers.AutomationPeer.GetAutomationControlTypeCore%2A> descrive il controllo restituendo un <xref:System.Windows.Automation.ControlType> valore. Sebbene sia possibile restituire <xref:System.Windows.Automation.ControlType.Custom?displayProperty=fullName>, è necessario restituire uno dei tipi più specifici di controllo se il controllo viene descritto in modo accurato. Un valore restituito di <xref:System.Windows.Automation.ControlType.Custom?displayProperty=fullName> richiede un lavoro aggiuntivo per il provider di implementare [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)], e [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] prodotti client sono in grado di anticipare la struttura di controllo, l'interazione della tastiera e possibili pattern di controllo.  
  
 Implementare il <xref:System.Windows.Automation.Peers.AutomationPeer.IsContentElementCore%2A> e <xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A> metodi per indicare se il controllo contiene dati o svolge un ruolo interattivo nell'interfaccia utente (o entrambi). Per impostazione predefinita, entrambi i metodi restituiscono `true`. Queste impostazioni migliorano l'utilizzabilità di strumenti di automazione, ad esempio gli screen reader, che possono utilizzare questi metodi per filtrare l'albero di automazione. Se il <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> la gestione a un peer, il peer del sottoelemento metodo trasferimenti pattern <xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A> metodo può restituire false per nascondere il peer del sottoelemento dalla struttura ad albero di automazione. Ad esempio, lo scorrimento in un <xref:System.Windows.Controls.ListBox> viene gestita da un <xref:System.Windows.Controls.ScrollViewer>e peer di automazione per <xref:System.Windows.Automation.Peers.PatternInterface?displayProperty=fullName> restituito dal <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> metodo il <xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer> associato il <xref:System.Windows.Automation.Peers.ListBoxAutomationPeer>. Pertanto, il <xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A> metodo il <xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer> restituisce `false`, in modo che il <xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer> non viene visualizzato nella struttura ad albero di automazione.  
  
 Il peer di automazione deve fornire i valori predefiniti appropriati per il controllo. Si noti che il codice XAML che fa riferimento al controllo possono eseguire l'override delle implementazioni peer dei metodi di base includendo <xref:System.Windows.Automation.AutomationProperties> attributi. Ad esempio, il codice XAML seguente crea un pulsante che dispone di due personalizzato [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] proprietà.  
  
```xaml  
<Button AutomationProperties.Name="Special"   
    AutomationProperties.HelpText="This is a special button."/>  
```  
  
### <a name="implement-pattern-providers"></a>Implementare i provider di Pattern  
 Le interfacce implementate da un provider personalizzato sono dichiarate in modo esplicito se l'elemento proprietario deriva direttamente da <xref:System.Windows.Controls.Control>. Ad esempio, il codice seguente viene dichiarato un peer per un <xref:System.Windows.Controls.Control> che implementa un valore di intervallo.  
  
```csharp  
public class RangePeer1 : FrameworkElementAutomationPeer, IRangeValueProvider { }  
```  
  
```vb  
Public Class RangePeer1  
    Inherits FrameworkElementAutomationPeer  
    Implements IRangeValueProvider  
End Class  
```  
  
 Se il controllo proprietario deriva da un tipo specifico di controllo, ad esempio <xref:System.Windows.Controls.Primitives.RangeBase>, il peer può essere derivato da una classe peer derivata equivalente. In questo caso, il peer deriva da <xref:System.Windows.Automation.Peers.RangeBaseAutomationPeer>, che fornisce un'implementazione di base di <xref:System.Windows.Automation.Provider.IRangeValueProvider>. Il codice seguente viene illustrata la dichiarazione di tale peer.  
  
```csharp  
public class RangePeer2 : RangeBaseAutomationPeer { }  
```  
  
```vb  
Public Class RangePeer2  
    Inherits RangeBaseAutomationPeer  
End Class  
```  
  
 Per un esempio di implementazione, vedere [controllo personalizzato NumericUpDown con esempio di supporto di automazione dell'interfaccia utente e tema](http://go.microsoft.com/fwlink/?LinkID=160025).  
  
### <a name="raise-events"></a>Generazione di eventi  
 Client di automazione possono sottoscrivere gli eventi di automazione. Controlli personalizzati devono segnalare le modifiche allo stato del controllo chiamando la <xref:System.Windows.Automation.Peers.AutomationPeer.RaiseAutomationEvent%2A> metodo. Analogamente, quando un valore della proprietà viene modificato, chiamare il <xref:System.Windows.Automation.Peers.AutomationPeer.RaisePropertyChangedEvent%2A> metodo. Il codice seguente viene illustrato come ottenere l'oggetto peer dal codice del controllo e chiamare un metodo per generare un evento. Come ottimizzazione, il codice determina se sono presenti listener per questo tipo di evento. La generazione dell'evento solo quando sono presenti listener evita l'inutile e consente il controllo rimane attiva.  
  
 [!code-csharp[CustomControlNumericUpDown#RaiseEventFromControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#raiseeventfromcontrol)]
 [!code-vb[CustomControlNumericUpDown#RaiseEventFromControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#raiseeventfromcontrol)]  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di automazione interfaccia utente](../../../../docs/framework/ui-automation/ui-automation-overview.md)   
 [Controllo personalizzato NumericUpDown con esempio di supporto di automazione dell'interfaccia utente e tema](http://go.microsoft.com/fwlink/?LinkID=160025)   
 [Implementazione del Provider di automazione interfaccia utente lato server](../../../../docs/framework/ui-automation/server-side-ui-automation-provider-implementation.md)