---
title: "Obtaining UI Automation Elements | Microsoft Docs"
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
  - "UI Automation, obtaining elements"
  - "elements, UI Automation, obtaining"
ms.assetid: c2caaf45-e59c-42a1-bc9b-77a6de520171
caps.latest.revision: 23
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 23
---
# Obtaining UI Automation Elements
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Questo argomento descrive i diversi modi in cui è possibile ottenere oggetti <xref:System.Windows.Automation.AutomationElement> per gli elementi dell'[!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)].  
  
> [!CAUTION]
>  Se c'è la possibilità che l'applicazione client cerchi di trovare elementi nell'interfaccia utente, è necessario effettuare tutte le chiamate a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] in un thread separato. Per altre informazioni, vedere [UI Automation Threading Issues](../../../docs/framework/ui-automation/ui-automation-threading-issues.md).  
  
<a name="The_Root_Element"></a>   
## Elemento radice  
 Tutte le ricerche di oggetti <xref:System.Windows.Automation.AutomationElement> devono avere un punto di partenza, che può essere un elemento qualsiasi, incluso il desktop, una finestra dell'applicazione o un controllo.  
  
 L'elemento radice per il desktop, da cui discendono tutti gli elementi, si ottiene dalla proprietà <xref:System.Windows.Automation.AutomationElement.RootElement%2A?displayProperty=fullName> statica.  
  
> [!CAUTION]
>  In generale, è consigliabile cercare di ottenere solo elementi figlio diretti di <xref:System.Windows.Automation.AutomationElement.RootElement%2A>. Una ricerca dei discendenti può scorrere centinaia o anche migliaia di elementi, con la possibilità che venga generato un overflow dello stack. Per ottenere un elemento specifico a un livello inferiore, è consigliabile avviare la ricerca dalla finestra dell'applicazione o da un contenitore a un livello inferiore.  
  
<a name="Using_Conditions"></a>   
## Condizioni  
 Per la maggior parte delle tecniche che è possibile usare per recuperare elementi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], è necessario specificare un oggetto <xref:System.Windows.Automation.Condition>, ovvero un set di criteri che definiscono gli elementi da recuperare.  
  
 La condizione più semplice è <xref:System.Windows.Automation.Condition.TrueCondition>, un oggetto predefinito che specifica che devono essere restituiti tutti gli elementi nell'ambito della ricerca.<xref:System.Windows.Automation.Condition.FalseCondition>, il contrario di <xref:System.Windows.Automation.Condition.TrueCondition>, è meno utile, perché impedisce di trovare qualsiasi elemento.  
  
 Si possono usare altre tre condizioni predefinite, da sole o in combinazione con altre condizioni: <xref:System.Windows.Automation.Automation.ContentViewCondition>, <xref:System.Windows.Automation.Automation.ControlViewCondition> e <xref:System.Windows.Automation.Automation.RawViewCondition>.<xref:System.Windows.Automation.Automation.RawViewCondition>, usata da sola, equivale a <xref:System.Windows.Automation.Condition.TrueCondition>, perché non filtra gli elementi in base alle proprietà <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsControlElement%2A> o <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsContentElement%2A>.  
  
 Le altre condizioni si basano su uno o più oggetti <xref:System.Windows.Automation.PropertyCondition>, che specificano tutti un valore di una proprietà. Ad esempio, un oggetto <xref:System.Windows.Automation.PropertyCondition> può specificare che l'elemento è abilitato o che supporta un determinato pattern di controllo.  
  
 Le condizioni possono essere combinate con la logica booleana costruendo oggetti di tipo <xref:System.Windows.Automation.AndCondition>, <xref:System.Windows.Automation.OrCondition> e <xref:System.Windows.Automation.NotCondition>.  
  
<a name="Search_Scope"></a>   
## Ambito di ricerca  
 Le ricerche eseguite usando <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> o <xref:System.Windows.Automation.AutomationElement.FindAll%2A> devono avere un ambito, oltre che un punto di partenza.  
  
 L'ambito definisce lo spazio attorno al punto di partenza, in cui eseguire la ricerca, e può includere l'elemento stesso, gli elementi sibling, gli elementi padre, i predecessori, gli elementi figlio diretti e i discendenti.  
  
 L'ambito di una ricerca viene definito da una combinazione bit per bit di valori dall'enumerazione <xref:System.Windows.Automation.TreeScope>.  
  
<a name="Finding_a_Known_Element"></a>   
## Ricerca di un elemento noto  
 Per trovare un elemento noto, identificato da <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name%2A>, <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.AutomationId%2A> o da altre proprietà o combinazioni di proprietà, il modo più semplice è usare il metodo <xref:System.Windows.Automation.AutomationElement.FindFirst%2A>. Se l'elemento cercato è una finestra dell'applicazione, il punto di partenza della ricerca può essere l'oggetto <xref:System.Windows.Automation.AutomationElement.RootElement%2A>.  
  
 Questo tipo di ricerca degli elementi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] è molto utile negli scenari di test automatizzato.  
  
<a name="Finding_Elements_in_a_Subtree"></a>   
## Ricerca di elementi in un sottoalbero  
 Per trovare tutti gli elementi che soddisfano criteri specifici correlati a un elemento noto, è possibile usare <xref:System.Windows.Automation.AutomationElement.FindAll%2A>. È possibile, ad esempio, usare questo metodo per recuperare elementi elenco o voci di menu da un elenco o da un menu o per identificare tutti i controlli in una finestra di dialogo.  
  
<a name="Walking_a_Subtree"></a>   
## Esplorazione di un sottoalbero  
 Se non si conoscono le applicazioni con cui il client potrebbe essere usato, è possibile costruire un sottoalbero di tutti gli elementi a cui si è interessati usando la classe <xref:System.Windows.Automation.TreeWalker>. L'applicazione potrebbe eseguire questa operazione in risposta a un evento di modifica dello stato attivo, ovvero, quando un'applicazione o un controllo riceve lo stato attivo per l'input, il client di automazione interfaccia utente esamina gli elementi figlio ed eventualmente i discendenti dell'elemento con lo stato attivo.  
  
 Un altro modo per usare <xref:System.Windows.Automation.TreeWalker> è identificare i predecessori di un elemento. Ad esempio, spostandosi verso l'alto nell'albero, è possibile identificare la finestra padre di un controllo.  
  
 È possibile usare <xref:System.Windows.Automation.TreeWalker> creando un oggetto della classe \(per definire gli elementi a cui si è interessati passando un oggetto <xref:System.Windows.Automation.Condition>\) o usando uno degli oggetti predefiniti seguenti che vengono definiti come campi di <xref:System.Windows.Automation.TreeWalker>.  
  
|||  
|-|-|  
|<xref:System.Windows.Automation.TreeWalker.ContentViewWalker>|Trova solo gli elementi la cui proprietà <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsContentElement%2A> è `true`.|  
|<xref:System.Windows.Automation.TreeWalker.ControlViewWalker>|Trova solo gli elementi la cui proprietà <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsControlElement%2A> è `true`.|  
|<xref:System.Windows.Automation.TreeWalker.RawViewWalker>|Trova tutti gli elementi.|  
  
 Dopo avere ottenuto un <xref:System.Windows.Automation.TreeWalker>, usarlo è davvero semplice. È sufficiente chiamare i metodi `Get` per spostarsi tra gli elementi del sottoalbero.  
  
 Il metodo <xref:System.Windows.Automation.TreeWalker.Normalize%2A> può essere usato per passare a un elemento nel sottoalbero da un altro elemento che non fa parte della visualizzazione. Si supponga, ad esempio, di avere creato una visualizzazione di un sottoalbero usando <xref:System.Windows.Automation.TreeWalker.ContentViewWalker>. L'applicazione riceve quindi la notifica che una barra di scorrimento ha ricevuto lo stato attivo per l'input. Poiché una barra di scorrimento non è un elemento con contenuto, non è presente nella visualizzazione del sottoalbero. È possibile, tuttavia, passare l'oggetto <xref:System.Windows.Automation.AutomationElement> che rappresenta la barra di scorrimento a <xref:System.Windows.Automation.TreeWalker.Normalize%2A> e recuperare il predecessore più vicino nella visualizzazione contenuto.  
  
<a name="Other_Ways_to_Retrieve_an_Element"></a>   
## Altri modi per recuperare un elemento  
 Oltre alle ricerche e alla navigazione, è possibile recuperare un oggetto <xref:System.Windows.Automation.AutomationElement> nei seguenti modi.  
  
### Da un evento  
 Quando l'applicazione riceve un evento di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], l'oggetto di origine passato al gestore eventi è <xref:System.Windows.Automation.AutomationElement>. Se, ad esempio, sono stati sottoscritti gli eventi di modifica dello stato attivo, l'origine passata all'oggetto <xref:System.Windows.Automation.AutomationFocusChangedEventHandler> è l'elemento che ha ricevuto lo stato attivo.  
  
 Per altre informazioni, vedere [Subscribe to UI Automation Events](../../../docs/framework/ui-automation/subscribe-to-ui-automation-events.md).  
  
### Da un punto  
 Se si conoscono le coordinate nella schermata \(ad esempio, la posizione di un cursore\), è possibile recuperare un oggetto <xref:System.Windows.Automation.AutomationElement> usando il metodo <xref:System.Windows.Automation.AutomationElement.FromPoint%2A> statico.  
  
### Da un handle di finestra  
 Per recuperare un oggetto <xref:System.Windows.Automation.AutomationElement> da HWND, usare il metodo <xref:System.Windows.Automation.AutomationElement.FromHandle%2A> statico.  
  
### Dal controllo con lo stato attivo  
 È possibile ricevere un oggetto <xref:System.Windows.Automation.AutomationElement> che rappresenta il controllo con lo stato attivo dalla proprietà <xref:System.Windows.Automation.AutomationElement.FocusedElement%2A> statica.  
  
## Vedere anche  
 [Find a UI Automation Element Based on a Property Condition](../../../docs/framework/ui-automation/find-a-ui-automation-element-based-on-a-property-condition.md)   
 [Navigate Among UI Automation Elements with TreeWalker](../../../docs/framework/ui-automation/navigate-among-ui-automation-elements-with-treewalker.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)