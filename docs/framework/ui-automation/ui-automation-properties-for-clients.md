---
title: "UI Automation Properties for Clients | Microsoft Docs"
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
  - "properties, UI Automation clients"
  - "UI Automation, client properties"
ms.assetid: 255905af-0b17-485c-93d4-8a2db2a6524b
caps.latest.revision: 17
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 17
---
# UI Automation Properties for Clients
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questa panoramica sono presentate le proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] così come vengono esposte nelle applicazioni client di automazione interfaccia utente.  
  
 Le proprietà sugli oggetti <xref:System.Windows.Automation.AutomationElement> contengono informazioni sugli elementi dell'[!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)], in genere i controlli. Le proprietà di un oggetto <xref:System.Windows.Automation.AutomationElement> sono generiche, ovvero non sono specifiche di un tipo di controllo. Molte di queste proprietà sono esposte nella struttura <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation>.  
  
 Anche i pattern di controllo hanno proprietà. Le proprietà dei pattern di controllo sono specifiche del modello. Ad esempio, <xref:System.Windows.Automation.ScrollPattern> dispone di proprietà che forniscono a un'applicazione client informazioni sulla possibilità di scorrere una finestra in senso verticale o orizzontale, sulle dimensioni correnti della visualizzazione e sulle posizioni di scorrimento. I pattern di controllo espongono tutte le proprietà tramite una struttura, ad esempio <xref:System.Windows.Automation.ScrollPattern.ScrollPatternInformation>.  
  
 Le proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] sono di sola lettura. Per impostare le proprietà di un controllo, è necessario usare i metodi del pattern di controllo appropriato. Ad esempio, usare il metodo <xref:System.Windows.Automation.ScrollPattern.Scroll%2A> per modificare i valori di posizione di una finestra a scorrimento.  
  
 Per migliorare le prestazioni, è possibile memorizzare nella cache i valori di proprietà di controlli e pattern di controllo quando vengono recuperati oggetti <xref:System.Windows.Automation.AutomationElement>. Per altre informazioni, vedere [Caching in UI Automation Clients](../../../docs/framework/ui-automation/caching-in-ui-automation-clients.md).  
  
<a name="Property_IDs"></a>   
## ID di proprietà  
 Gli [!INCLUDE[TLA#tla_id#plural](../../../includes/tlasharptla-idsharpplural-md.md)] di proprietà sono valori univoci e costanti incapsulati in oggetti <xref:System.Windows.Automation.AutomationProperty>. Le applicazioni client di automazione interfaccia utente ottengono questi [!INCLUDE[TLA2#tla_id#plural](../../../includes/tla2sharptla-idsharpplural-md.md)] dalla classe <xref:System.Windows.Automation.AutomationElement> o dalla classe di pattern di controllo appropriata, ad esempio <xref:System.Windows.Automation.ScrollPattern>. I provider di automazione interfaccia utente li ottengono da <xref:System.Windows.Automation.AutomationElementIdentifiers> o da una delle classi di identificatori di pattern di controllo, ad esempio <xref:System.Windows.Automation.ScrollPatternIdentifiers>.  
  
 La proprietà <xref:System.Windows.Automation.AutomationIdentifier.Id%2A> numerica di un oggetto <xref:System.Windows.Automation.AutomationProperty> viene usata dai provider per identificare le proprietà sulle quali vengono eseguite query nel metodo  <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPropertyValue%2A?displayProperty=fullName>. In genere, non è necessario che le applicazioni client esaminino la proprietà <xref:System.Windows.Automation.AutomationIdentifier.Id%2A>. La proprietà <xref:System.Windows.Automation.AutomationIdentifier.ProgrammaticName%2A> viene usata solo a scopi di debug e diagnostica.  
  
<a name="Property_Conditions"></a>   
## Condizioni della proprietà  
 Gli [!INCLUDE[TLA2#tla_id#plural](../../../includes/tla2sharptla-idsharpplural-md.md)] di proprietà vengono usati nella costruzione di oggetti <xref:System.Windows.Automation.PropertyCondition> impiegati per trovare oggetti <xref:System.Windows.Automation.AutomationElement>. Ad esempio, può essere necessario trovare un oggetto <xref:System.Windows.Automation.AutomationElement> con un determinato nome o tutti i controlli abilitati. Ogni <xref:System.Windows.Automation.PropertyCondition> specifica un identificatore <xref:System.Windows.Automation.AutomationProperty> e il valore a cui deve corrispondere la proprietà.  
  
 Per altre informazioni, vedere gli argomenti di riferimento riportati di seguito:  
  
-   <xref:System.Windows.Automation.AutomationElement.FindFirst%2A>  
  
-   <xref:System.Windows.Automation.AutomationElement.FindAll%2A>  
  
-   <xref:System.Windows.Automation.TreeWalker.Condition%2A>  
  
<a name="Retrieving_Properties"></a>   
## Recupero di proprietà  
 Alcune proprietà di <xref:System.Windows.Automation.AutomationElement> e tutte le proprietà di una classe di pattern di controllo sono esposte come proprietà annidate della proprietà `Current` o `Cached` dell'oggetto <xref:System.Windows.Automation.AutomationElement> o dell'oggetto del pattern di controllo.  
  
 Inoltre, qualsiasi proprietà di <xref:System.Windows.Automation.AutomationElement> o del pattern di controllo, inclusa una proprietà non disponibile nella struttura <xref:System.Windows.Automation.AutomationElement.Cached%2A> o <xref:System.Windows.Automation.AutomationElement.Current%2A>, può essere recuperata usando uno dei metodi seguenti:  
  
-   <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A>  
  
-   <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A>  
  
 Questi metodi offrono prestazioni leggermente superiori, oltre all'accesso alla gamma completa di proprietà.  
  
 Nell'esempio di codice seguente sono mostrate due modalità di recupero di una proprietà su un oggetto <xref:System.Windows.Automation.AutomationElement>.  
  
 [!code-csharp[UIAClient_snip#121](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#121)]
 [!code-vb[UIAClient_snip#121](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#121)]  
  
 Per recuperare proprietà di pattern di controllo supportate dall'oggetto <xref:System.Windows.Automation.AutomationElement>, non è necessario recuperare l'oggetto del pattern di controllo. È sufficiente passare al metodo uno degli identificatori di proprietà di modello.  
  
 Nell'esempio di codice seguente sono mostrate due modalità di recupero di una proprietà su un pattern di controllo.  
  
 [!code-csharp[UIAClient_snip#122](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#122)]
 [!code-vb[UIAClient_snip#122](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#122)]  
  
 I metodi `Get` restituiscono un oggetto <xref:System.Object>. L'applicazione deve eseguire il cast dell'oggetto restituito al tipo corretto prima di usare il valore.  
  
<a name="_Default_Property_Values"></a>   
## Valori di proprietà predefiniti  
 Se un provider di automazione interfaccia utente non implementa una proprietà, il sistema di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] è in grado di fornire un valore predefinito. Ad esempio, se il provider per un controllo non supporta la proprietà identificata da <xref:System.Windows.Automation.AutomationElement.HelpTextProperty>, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] restituisce una stringa vuota. Analogamente, se il provider non supporta la proprietà identificata da <xref:System.Windows.Automation.AutomationElement.IsDockPatternAvailableProperty>, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] restituisce `false`.  
  
 È possibile modificare questo comportamento usando gli overload dei metodi <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A?displayProperty=fullName> e <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A?displayProperty=fullName>. Quando si specifica `true` come secondo parametro, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] non restituisce un valore predefinito, ma restituisce il valore speciale <xref:System.Windows.Automation.AutomationElement.NotSupported>.  
  
 Nel codice di esempio riportato di seguito si tenta di recuperare una proprietà da un elemento e, se la proprietà non è supportata, viene usato in alternativa un valore definito dall'applicazione.  
  
 [!code-csharp[UIAClient_snip#123](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#123)]
 [!code-vb[UIAClient_snip#123](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#123)]  
  
 Per individuare le proprietà supportate da un elemento, usare il metodo <xref:System.Windows.Automation.AutomationElement.GetSupportedProperties%2A>. Restituisce una matrice di identificatori <xref:System.Windows.Automation.AutomationProperty>.  
  
<a name="Property_changed_Events"></a>   
## Eventi di modifica delle proprietà  
 Quando viene modificato un valore di proprietà su un oggetto <xref:System.Windows.Automation.AutomationElement> o un pattern di controllo, viene generato un evento. Un'applicazione può sottoscrivere tali eventi chiamando il metodo <xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A>, fornendo una matrice di identificatori <xref:System.Windows.Automation.AutomationProperty> come ultimo parametro per specificare le proprietà di interesse.  
  
 Nell'oggetto <xref:System.Windows.Automation.AutomationPropertyChangedEventHandler>, è possibile identificare la proprietà modificata controllando il membro <xref:System.Windows.Automation.AutomationPropertyChangedEventArgs.Property%2A> degli argomenti dell'evento. Gli argomenti contengono anche i valori obsoleti e nuovi della proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] modificata. Questi valori sono di tipo <xref:System.Object> ed è necessario eseguirne il cast al tipo corretto prima di usarli.  
  
<a name="Additional_AutomationElement_Properties"></a>   
## Proprietà AutomationElement aggiuntiva  
 Oltre alle strutture delle proprietà <xref:System.Windows.Automation.AutomationElement.Current%2A> e <xref:System.Windows.Automation.AutomationElement.Cached%2A>, l'oggetto <xref:System.Windows.Automation.AutomationElement> ha le proprietà seguenti, recuperate tramite semplici funzioni di accesso della proprietà.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Windows.Automation.AutomationElement.CachedChildren%2A>|Insieme di oggetti <xref:System.Windows.Automation.AutomationElement> figlio presenti nella cache.|  
|<xref:System.Windows.Automation.AutomationElement.CachedParent%2A>|Oggetto <xref:System.Windows.Automation.AutomationElement> padre presente nella cache.|  
|<xref:System.Windows.Automation.AutomationElement.FocusedElement%2A>|\(Proprietà statica\) Oggetto <xref:System.Windows.Automation.AutomationElement> con lo stato attivo per l'input.|  
|<xref:System.Windows.Automation.AutomationElement.RootElement%2A>|\(Proprietà statica\) Oggetto <xref:System.Windows.Automation.AutomationElement> radice.|  
  
## Vedere anche  
 [Caching in UI Automation Clients](../../../docs/framework/ui-automation/caching-in-ui-automation-clients.md)   
 [Server\-Side UI Automation Provider Implementation](../../../docs/framework/ui-automation/server-side-ui-automation-provider-implementation.md)   
 [Subscribe to UI Automation Events](../../../docs/framework/ui-automation/subscribe-to-ui-automation-events.md)