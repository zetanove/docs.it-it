---
title: "Server-Side UI Automation Provider Implementation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "server-side UI Automation provider implementation"
  - "UI Automation, server-side provider implementation"
  - "provider implementation, UI Automation"
ms.assetid: 6acc6d08-bd67-4e2e-915c-9c1d34eb86fe
caps.latest.revision: 39
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 38
---
# Server-Side UI Automation Provider Implementation
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questa sezione viene descritto come implementare un provider di automazione interfaccia utente sul lato server per un controllo personalizzato.  
  
 L'implementazione per gli elementi [!INCLUDE[TLA#tla_wpf](../../../includes/tlasharptla-wpf-md.md)] e non [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] \(ad esempio quelli progettati per [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]\) è fondamentalmente diversa. Gli elementi [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] forniscono supporto per [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] tramite una classe derivata da <xref:System.Windows.Automation.Peers.AutomationPeer>. Gli elementi non [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] forniscono supporto tramite implementazioni di interfacce del provider.  
  
<a name="Security_Considerations"></a>   
## Considerazioni sulla sicurezza  
 I provider devono essere scritti in modo che possano operare in un ambiente parzialmente attendibile. Dato che UIAutomationClient.dll non è configurato per l'esecuzione con attendibilità parziale, il codice del provider non dovrebbe fare riferimento a tale assembly. In caso contrario, il codice potrebbe essere eseguito in un ambiente con attendibilità completa, ma poi generare errori in un ambiente parzialmente attendibile.  
  
 In particolare, non usare campi delle classi in UIAutomationClient.dll come quelle in <xref:System.Windows.Automation.AutomationElement>. Usare invece i campi equivalenti dalle classi in UIAutomationTypes.dll, come <xref:System.Windows.Automation.AutomationElementIdentifiers>.  
  
<a name="Provider_Implementation_by_WPF_Elements"></a>   
## Implementazione di provider da elementi di Windows Presentation Foundation  
 Per altre informazioni su questo argomento, vedere [Automazione interfaccia utente di un controllo personalizzato WPF](../../../docs/framework/wpf/controls/ui-automation-of-a-wpf-custom-control.md).  
  
<a name="Provider_Implementation_by_non_WPF_Elements"></a>   
## Implementazione di provider da elementi non WPF  
 I controlli personalizzati che non fanno parte del framework [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)], ma scritti in codice gestito \(in genere si tratta di controlli [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]\), offrono il supporto per [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] tramite l'implementazione di interfacce. Ogni elemento deve implementare almeno una delle interfacce elencate nella prima tabella nella sezione successiva. Inoltre, se l'elemento supporta uno o più pattern di controllo, deve implementare l'interfaccia appropriata per ognuno di essi.  
  
 Il progetto del provider [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] deve fare riferimento agli assembly seguenti:  
  
-   UIAutomationProviders.dll  
  
-   UIAutomationTypes.dll  
  
-   WindowsBase.dll  
  
   
  
<a name="Provider_Interfaces"></a>   
### Interfacce del provider  
 Ogni provider [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] deve implementare una delle interfacce seguenti.  
  
|Interfaccia|Descrizione|  
|-----------------|-----------------|  
|<xref:System.Windows.Automation.Provider.IRawElementProviderSimple>|Fornisce funzionalità per un controllo semplice ospitato in una finestra, incluso il supporto per pattern di controllo e proprietà.|  
|<xref:System.Windows.Automation.Provider.IRawElementProviderFragment>|Eredita da <xref:System.Windows.Automation.Provider.IRawElementProviderSimple>. Aggiunge la funzionalità per un elemento in un controllo complesso, inclusi lo spostamento all'interno del frammento, l'impostazione dello stato attivo e la restituzione del rettangolo delimitatore dell'elemento.|  
|<xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot>|Eredita da <xref:System.Windows.Automation.Provider.IRawElementProviderFragment>. Aggiunge la funzionalità per l'elemento radice in un controllo complesso, inclusi l'individuazione di un elemento figlio in corrispondenza delle coordinate specificate e l'impostazione dello stato attivo per l'intero controllo.|  
  
 Le interfacce seguenti offrono ulteriori funzionalità, ma la loro implementazione non è richiesta.  
  
|Interfaccia|Descrizione|  
|-----------------|-----------------|  
|<xref:System.Windows.Automation.Provider.IRawElementProviderAdviseEvents>|Consente al provider di tenere traccia delle richieste per eventi.|  
|<xref:System.Windows.Automation.Provider.IRawElementProviderHwndOverride>|Abilita il riposizionamento degli elementi basati su finestra all'interno dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] di un frammento.|  
  
 Tutte le altre interfacce nello spazio dei nomi <xref:System.Windows.Automation.Provider> sono destinate al supporto dei pattern di controllo.  
  
<a name="Requirements_for_Non_WPF_Providers"></a>   
### Requisiti per i provider non WPF  
 Per comunicare con [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], il tuo controllo deve implementare le aree di funzionalità principali seguenti:  
  
|Funzionalità|Implementazione|  
|------------------|---------------------|  
|Esporre il provider a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|In risposta a un messaggio WM\_GETOBJECT inviato alla finestra del controllo, restituire l'oggetto che implementa <xref:System.Windows.Automation.Provider.IRawElementProviderSimple> \(o un'interfaccia derivata\). Per i frammenti, deve trattarsi del provider per la radice del frammento.|  
|Fornire i valori delle proprietà|Implementare <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPropertyValue%2A> per fornire i valori o eseguirne l'override.|  
|Consentire al client di interagire con il controllo|Implementare le interfacce che supportano pattern di controllo, ad esempio <xref:System.Windows.Automation.Provider.IInvokeProvider>. Restituire questi provider di pattern nell'implementazione di <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPatternProvider%2A>.|  
|Generare eventi|Chiamare uno dei metodi statici di <xref:System.Windows.Automation.Provider.AutomationInteropProvider> per generare un evento di cui un client può rimanere in ascolto.|  
|Abilitare la navigazione e lo spostamento dello stato attivo all'interno di un frammento|Implementare <xref:System.Windows.Automation.Provider.IRawElementProviderFragment> per ogni elemento all'interno del frammento. \(Non necessario per gli elementi che non fanno parte di un frammento\).|  
|Abilitare lo spostamento dello stato attivo e il posizionamento dell'elemento figlio in un frammento|Implementare <xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot>. \(Non necessario per gli elementi che non sono radici di frammenti\).|  
  
<a name="Property_Values_in_Non_WPF_Providers"></a>   
### Valori delle proprietà nei provider non WPF  
 I provider [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per i controlli personalizzati devono supportare determinate proprietà che possono essere usate dai sistemi di automazione ed anche dalle applicazioni client. Per gli elementi ospitati nelle finestre \(HWND\), [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] può recuperare alcune proprietà dal provider di finestra predefinito, ma deve ottenerne altre dal provider personalizzato.  
  
 I provider per i controlli basati su HWND in genere non richiedono di specificare le proprietà seguenti \(identificate da valori di campo\):  
  
-   <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>  
  
-   <xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>  
  
-   <xref:System.Windows.Automation.AutomationElementIdentifiers.ProcessIdProperty>  
  
-   <xref:System.Windows.Automation.AutomationElementIdentifiers.ClassNameProperty>  
  
-   <xref:System.Windows.Automation.AutomationElementIdentifiers.HasKeyboardFocusProperty>  
  
-   <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>  
  
-   <xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>  
  
-   <xref:System.Windows.Automation.AutomationElementIdentifiers.IsPasswordProperty>  
  
-   <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>  
  
-   <xref:System.Windows.Automation.AutomationElementIdentifiers.RuntimeIdProperty>  
  
> [!NOTE]
>  Il valore <xref:System.Windows.Automation.AutomationElementIdentifiers.RuntimeIdProperty> di un elemento semplice o di una radice di frammento ospitato in una finestra viene ottenuto dalla finestra. Tuttavia, gli elementi del frammento sotto la radice \(ad esempio voci di elenco in una casella di riepilogo\) devono fornire i propri identificatori. Per altre informazioni, vedere <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.GetRuntimeId%2A>.  
>   
>  Il valore <xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty> deve essere restituito per i provider ospitati in un controllo [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]. In questo caso, il provider di finestra predefinito potrebbe non essere in grado di recuperare il valore corretto.  
>   
>  Il valore <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> viene in genere fornito dal provider host. Ad esempio, se un controllo personalizzato è derivato da <xref:System.Windows.Forms.Control>, il nome è derivato dalla proprietà `Text` del controllo.  
  
 Per il codice di esempio, vedere [Return Properties from a UI Automation Provider](../../../docs/framework/ui-automation/return-properties-from-a-ui-automation-provider.md).  
  
<a name="Events_in_Non_WPF_Providers"></a>   
### Eventi nei provider non WPF  
 I provider [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] devono generare eventi per notificare alle applicazioni client le modifiche allo stato dell'interfaccia utente. Per generare gli eventi vengono usati i metodi seguenti.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.RaiseAutomationEvent%2A>|Genera vari eventi, inclusi gli eventi attivati dai pattern di controllo.|  
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.RaiseAutomationPropertyChangedEvent%2A>|Genera un evento in seguito alla modifica di una proprietà [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.RaiseStructureChangedEvent%2A>|Genera un evento in seguito alla modifica della struttura dell'albero [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], ad esempio per la rimozione o l'aggiunta di un elemento.|  
  
 Lo scopo di un evento è notificare al client qualcosa che si verifica nell'[!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)], indipendentemente dal fatto che l'attività sia attivata dal sistema [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] stesso. Ad esempio, l'evento identificato da <xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent> dovrebbe essere generato ogni volta che viene richiamato il controllo, sia tramite input diretto dell'utente o dall'applicazione client che chiama <xref:System.Windows.Automation.InvokePattern.Invoke%2A>.  
  
 Per ottimizzare le prestazioni, un provider può generare eventi in modo selettivo o non generarne affatto se nessuna applicazione client è registrata per riceverli. Per l'ottimizzazione vengono usati i metodi seguenti.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.ClientsAreListening%2A>|Questa proprietà statica specifica se tutte le applicazioni client hanno sottoscritto eventi [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.Provider.IRawElementProviderAdviseEvents>|L'implementazione del provider di questa interfaccia in una radice di frammento consente di ricevere notifica quando i client registrano e annullano la registrazione di gestori eventi per gli eventi nel frammento.|  
  
<a name="Non_WPF_Provider_Navigation"></a>   
### Navigazione per i provider non WPF  
 I provider per controlli semplici, ad esempio un pulsante personalizzato contenuto in una finestra \(HWND\) non devono supportare la navigazione all'interno dell'albero [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. La navigazione verso e dall'elemento viene gestita dal provider predefinito per la finestra host specificato nell'implementazione di <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A>. Quando si implementa un provider per un controllo personalizzato complesso, tuttavia, è necessario supportare la navigazione tra il nodo radice del frammento e i relativi discendenti, nonché tra nodi di pari livello.  
  
> [!NOTE]
>  Gli elementi di un frammento diversi dalla radice devono restituire un riferimento a `null` da <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A>, perché non sono ospitati direttamente in una finestra e nessun provider predefinito può supportare lo spostamento verso e da tali elementi.  
  
 La struttura del frammento è determinata dall'implementazione di <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.Navigate%2A>. Per ogni possibile direzione da ogni frammento, questo metodo restituisce l'oggetto provider per l'elemento in quella direzione. Se non è presente alcun elemento nella direzione specificata, il metodo restituisce un riferimento a `null`.  
  
 La radice del frammento supporta la navigazione solo verso gli elementi figlio. Ad esempio, una casella di riepilogo restituisce il primo elemento nell'elenco quando la direzione è <xref:System.Windows.Automation.Provider.NavigateDirection> e l'ultimo elemento quando la direzione è <xref:System.Windows.Automation.Provider.NavigateDirection>. La radice del frammento non supporta la navigazione verso un elemento padre o elementi di pari livello. Questa operazione viene gestita dal provider della finestra host.  
  
 Gli elementi di un frammento non radice devono supportare la navigazione verso l'elemento padre e verso eventuali elementi di pari livello e figli.  
  
<a name="Non_WPF_Provider_Reparenting"></a>   
### Associazione con un nuovo elemento padre per i provider non WPF  
 Le finestre popup sono in effetti finestre di primo livello, quindi per impostazione predefinita vengono visualizzate nell'albero [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] come figli del desktop. In molti casi, tuttavia, le finestre popup sono logicamente elementi figlio di un altro controllo. Ad esempio, l'elenco a discesa di una casella combinata è logicamente un elemento figlio della casella combinata. Analogamente, una finestra popup di menu è logicamente un elemento figlio del menu.[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] fornisce il supporto per l'associazione delle finestre popup con un nuovo elemento padre, in modo che vengano visualizzate come elementi figlio del controllo associato.  
  
 Per associare una finestra popup con un nuovo elemento padre:  
  
1.  Creare un provider per la finestra popup. È necessario che la classe della finestra popup sia nota in anticipo.  
  
2.  Implementare tutte le proprietà e i pattern come di consueto per tale popup, come se fosse un controllo.  
  
3.  Implementare la proprietà <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A> in modo che restituisca il valore ottenuto da <xref:System.Windows.Automation.Provider.AutomationInteropProvider.HostProviderFromHandle%2A>, dove il parametro è l'handle della finestra popup.  
  
4.  Implementare <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.Navigate%2A> per la finestra popup e il relativo elemento padre in modo che la navigazione venga gestita correttamente dall'elemento padre logico agli elementi figlio logici e tra gli elementi figlio di pari livello.  
  
 Quando [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] rileva la finestra popup, riconosce che la navigazione è diversa rispetto all'impostazione predefinita e ignora la finestra popup quando viene rilevata come un figlio del desktop. Al contrario, il nodo sarà raggiungibile solo tramite il frammento.  
  
 L'associazione con un nuovo elemento padre non è appropriata nei casi in cui un controllo può ospitare una finestra di qualsiasi classe. Ad esempio, un controllo Rebar può contenere qualsiasi tipo di HWND nelle proprie bande. Per gestire questi casi, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] supporta un tipo alternativo di rilocazione HWND, come descritto nella sezione successiva.  
  
<a name="Non_WPF_Provider_Repositioning"></a>   
### Riposizionamento per i provider non WPF  
 I frammenti di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] possono contenere due o più elementi contenuti ognuno in una finestra \(HWND\). Dato che ogni elemento HWND ha il proprio provider predefinito che considera HWND un elemento figlio di un HWND che lo contiene, l'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] visualizzerà, per impostazione predefinita, gli HWND nel frammento come elementi figlio della finestra padre. Nella maggior parte dei casi questo comportamento è utile, ma talvolta può generare confusione perché non corrisponde alla struttura logica della [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)].  
  
 Un esempio valido è un controllo Rebar. Un controllo Rebar contiene bande, ognuna delle quali può contenere a sua volta un controllo basato su HWND come una barra degli strumenti, una casella di modifica o una casella combinata. Il provider di finestra predefinito per l'HWND del controllo Rebar vede gli elementi HWND delle bande come elementi figlio e il provider del controllo Rebar considera le bande come elementi figlio. Poiché il provider HWND e il provider del controllo Rebar operano in tandem e combinano i rispettivi elementi figlio, sia le bande che i controlli basati su HWND vengono visualizzati come elementi figlio del controllo Rebar. Dal punto di vista logico, tuttavia, solo le bande devono apparire come elementi figlio del controllo Rebar e ogni provider di banda dovrebbe essere abbinato al provider HWND predefinito per il controllo che contiene.  
  
 A tale scopo, il provider di radice del frammento per il controllo Rebar espone un set di elementi figlio che rappresentano le bande. A ogni banda corrisponde un unico provider che può esporre proprietà e pattern. Nella sua implementazione di <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A>, il provider di bande restituisce il provider di finestra predefinito per il controllo HWND, ottenuto chiamando <xref:System.Windows.Automation.Provider.AutomationInteropProvider.HostProviderFromHandle%2A> e passando l'handle della finestra del controllo. Infine, il provider di radice del frammento per il controllo Rebar implementa l'interfaccia <xref:System.Windows.Automation.Provider.IRawElementProviderHwndOverride> e nella sua implementazione di <xref:System.Windows.Automation.Provider.IRawElementProviderHwndOverride.GetOverrideProviderForHwnd%2A> restituisce il provider di bande appropriato per il controllo contenuto nell'HWND specificato.  
  
## Vedere anche  
 [UI Automation Providers Overview](../../../docs/framework/ui-automation/ui-automation-providers-overview.md)   
 [Expose a Server\-side UI Automation Provider](../../../docs/framework/ui-automation/expose-a-server-side-ui-automation-provider.md)   
 [Return Properties from a UI Automation Provider](../../../docs/framework/ui-automation/return-properties-from-a-ui-automation-provider.md)   
 [Raise Events from a UI Automation Provider](../../../docs/framework/ui-automation/raise-events-from-a-ui-automation-provider.md)   
 [Enable Navigation in a UI Automation Fragment Provider](../../../docs/framework/ui-automation/enable-navigation-in-a-ui-automation-fragment-provider.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [Simple Provider Sample](http://msdn.microsoft.com/it-it/c10a6255-e8dc-494b-a051-15111b47984a)   
 [Fragment Provider Sample](http://msdn.microsoft.com/it-it/778ef1bc-8610-4bc9-886e-aeff94a8a13e)