---
title: "Cenni preliminari sulle origini di associazione | Microsoft Docs"
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
  - "associazione dati, associazione di origini"
  - "associazione di origini"
  - "associazione dati, origine di associazione"
ms.assetid: 2df2cd11-6aac-4bdf-ab7b-ea5f464cd5ca
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Cenni preliminari sulle origini di associazione
Nell'associazione dati, l'oggetto [origine di associazione](GTMT) fa riferimento all'oggetto da cui si ottengono i dati.  In questo argomento vengono descritti i tipi di oggetto che è possibile utilizzare come origine di associazione.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="binding_sources"></a>   
## Tipi di origine di associazione  
 L'associazione dati [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] supporta i seguenti tipi di [origine di associazione](GTMT):  
  
|Origine di associazione|Descrizione|  
|-----------------------------|-----------------|  
|Oggetti [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)].|È possibile stabilire l'associazione a proprietà pubbliche, proprietà secondarie, nonché indicizzatori di qualsiasi oggetto [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)].  La reflection [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] viene utilizzata dal motore di associazione per ottenere i valori delle proprietà.  In alternativa, anche gli oggetti che implementano <xref:System.ComponentModel.ICustomTypeDescriptor> o dispongono di un oggetto <xref:System.ComponentModel.TypeDescriptionProvider> registrato funzionano con il motore di associazione.<br /><br /> Per ulteriori informazioni sull'implementazione di una classe che può essere utilizzata come origine di associazione, vedere [Implementazione di una classe come origine di associazione](#classes) più avanti in questo argomento.|  
|Oggetti dinamici.|È possibile creare un'associazione a proprietà e indicizzatori disponibili di un oggetto che implementa l'interfaccia <xref:System.Dynamic.IDynamicMetaObjectProvider>.  Se è possibile accedere al membro nel codice, è possibile creare un'associazione a tale membro.  Ad esempio, se un oggetto dinamico consente di accedere a un membro nel codice tramite `someObjet.AProperty`, è possibile creare un'associazione al membro impostando il percorso di associazione su `AProperty`.|  
|Oggetti [!INCLUDE[TLA#tla_adonet](../../../../includes/tlasharptla-adonet-md.md)].|È possibile creare un'associazione a oggetti [!INCLUDE[TLA2#tla_adonet](../../../../includes/tla2sharptla-adonet-md.md)] quali <xref:System.Data.DataTable>. [!INCLUDE[TLA2#tla_adonet](../../../../includes/tla2sharptla-adonet-md.md)] <xref:System.Data.DataView> implementa l'interfaccia <xref:System.ComponentModel.IBindingList> che fornisce le notifiche delle modifiche per le quali è in ascolto il motore di associazione.|  
|Oggetti [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)].|È possibile stabilire l'associazione a <xref:System.Xml.XmlNode>, <xref:System.Xml.XmlDocument> o <xref:System.Xml.XmlElement> ed eseguirvi query `XPath`.  Un modo pratico per accedere a dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] che rappresentano l'[origine di associazione](GTMT) nel markup consiste nell'utilizzare un oggetto <xref:System.Windows.Data.XmlDataProvider>.  Per ulteriori informazioni, vedere [Eseguire l'associazione ai dati XML utilizzando un oggetto XMLDataProvider e le query XPath](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md).<br /><br /> È inoltre possibile eseguire l'associazione a un oggetto <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument> oppure eseguire l'associazione ai risultati delle query eseguite su oggetti di questi tipi mediante LINQ to XML.  Un modo pratico di utilizzare LINQ to XML per accedere ai dati XML che rappresentano l'origine di associazione nel markup consiste nell'utilizzare un oggetto <xref:System.Windows.Data.ObjectDataProvider>.  Per ulteriori informazioni, vedere [Esecuzione dell'associazione ai risultati di una query XDocument, XElement o LINQ to XML](../../../../docs/framework/wpf/data/how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md).|  
|Oggetti <xref:System.Windows.DependencyObject>.|È possibile stabilire l'associazione alle [proprietà di dipendenza](GTMT) di qualsiasi oggetto <xref:System.Windows.DependencyObject>.  Per un esempio, vedere [Eseguire l'associazione delle proprietà di due controlli](../../../../docs/framework/wpf/data/how-to-bind-the-properties-of-two-controls.md).|  
  
<a name="classes"></a>   
## Implementazione di una classe come origine di associazione  
 È possibile creare origini di associazione personalizzate.  In questa sezione vengono illustrati i concetti necessari per l'implementazione di una classe da utilizzare come origine di associazione.  
  
### Invio di notifiche delle modifiche  
 Se si utilizza l'associazione <xref:System.Windows.Data.BindingMode> o <xref:System.Windows.Data.BindingMode> per aggiornare l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] quando le proprietà dell'origine di associazione vengono modificate in modo dinamico, è necessario implementare un meccanismo di notifica adeguato per le proprietà modificate.  Il meccanismo consigliato consiste nell'implementare l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged> tramite la classe dinamica o tramite [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  Per ulteriori informazioni, vedere [Implementare la notifica di modifiche alle proprietà](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md).  
  
 Se si crea un oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] che non implementa <xref:System.ComponentModel.INotifyPropertyChanged>, è necessario configurare un sistema di notifica personalizzato in modo da assicurare che i dati utilizzati in un'associazione siano mantenuti aggiornati.  È possibile fornire notifiche delle modifiche tramite il supporto del modello `PropertyChanged` per ogni proprietà per la quale si desidera impostare tali notifiche.  Per supportare questo modello, definire un evento *NomeProprietà*Changed per ogni proprietà, in cui *NomeProprietà* rappresenta il nome della proprietà.  L'evento viene generato a ogni modifica della proprietà.  
  
 Se l'origine di associazione implementa uno di questi meccanismi di notifica, gli aggiornamenti della destinazione vengono eseguiti automaticamente.  Se per un motivo qualsiasi l'origine di associazione non fornisce notifiche corrette delle modifiche delle proprietà, è possibile utilizzare il metodo <xref:System.Windows.Data.BindingExpression.UpdateTarget%2A> per aggiornare in modo esplicito la proprietà di destinazione.  
  
### Altre caratteristiche  
 Nell'elenco seguente vengono illustrati altri punti importanti:  
  
-   Se si desidera creare l'oggetto in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], la classe deve disporre di un costruttore predefinito.  In alcuni linguaggi [!INCLUDE[TLA2#tla_net](../../../../includes/tla2sharptla-net-md.md)], ad esempio [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)], è possibile che il costruttore predefinito venga creato automaticamente.  
  
-   È necessario che le proprietà utilizzate come proprietà di origine di associazione per un'associazione siano proprietà pubbliche della classe.  Non è possibile accedere alle proprietà dell'interfaccia definite in modo esplicito a scopo di associazione, né alle proprietà protette, private, interne o virtuali prive di implementazione di base.  
  
-   Non è possibile stabilire l'associazione a campi pubblici.  
  
-   Il tipo della proprietà dichiarata nella classe è il tipo passato all'associazione.  Tuttavia, il tipo utilizzato in ultima analisi dall'associazione dipende dal tipo della proprietà della [destinazione di associazione](GTMT), non della proprietà di origine di associazione.  Se è presente una differenza nel tipo, è necessario scrivere un convertitore per gestire la modalità di passaggio iniziale della proprietà personalizzata all'associazione.  Per ulteriori informazioni, vedere <xref:System.Windows.Data.IValueConverter>.  
  
<a name="objects"></a>   
## Utilizzo di oggetti interi come origine di associazione  
 È possibile utilizzare un oggetto intero come origine di associazione.  È possibile specificare un'origine di associazione tramite la proprietà <xref:System.Windows.Data.Binding.Source%2A> o <xref:System.Windows.FrameworkElement.DataContext%2A>, quindi fornire una dichiarazione di associazione vuota: `{Binding}`.  Tra gli scenari per i quali questa possibilità si rivela utile vi sono l'associazione a oggetti di tipo stringa, l'associazione a oggetti con più proprietà di interesse o l'associazione a oggetti Collection.  Per un esempio di associazione a un intero oggetto Collection, vedere [Utilizzare il modello Master\-Details con dati gerarchici](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md).  
  
 Alcuni scenari richiedono l'applicazione di una logica personalizzata affinché i dati siano significativi per la proprietà di destinazione associata.  La logica personalizzata può avere il formato di convertitore personalizzato \(se la conversione di tipo predefinita non esiste\) o di <xref:System.Windows.DataTemplate>.  Per ulteriori informazioni sui convertitori, vedere la sezione Conversione di dati in [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  Per ulteriori informazioni sui modelli di dati, vedere [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md).  
  
<a name="collections"></a>   
## Utilizzo di oggetti Collection come origine di associazione  
 Spesso l'oggetto che si desidera utilizzare come origine di associazione corrisponde a una raccolta di oggetti personalizzati.  Ogni oggetto funge da origine per un'istanza di un'associazione ripetuta.  Ad esempio se si dispone di una raccolta `CustomerOrders` che include oggetti `CustomerOrder`, l'applicazione scorrerà la raccolta per determinare il numero di ordini inclusi e i dati contenuti in ciascuno di essi.  
  
 È possibile eseguire enumerazioni in qualsiasi raccolta che implementa l'interfaccia <xref:System.Collections.IEnumerable>.  Tuttavia, per impostare associazioni dinamiche in modo tale che l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] venga automaticamente aggiornata in seguito a operazioni di inserimento o eliminazione nella raccolta, è necessario che questo implementi l'interfaccia <xref:System.Collections.Specialized.INotifyCollectionChanged>.  Questa interfaccia espone un evento che deve essere generato a ogni modifica della raccolta sottostante.  
  
 La classe <xref:System.Collections.ObjectModel.ObservableCollection%601> rappresenta un'implementazione incorporata di una raccolta di dati che espone l'interfaccia <xref:System.Collections.Specialized.INotifyCollectionChanged>.  I singoli oggetti dati nella raccolta devono soddisfare i requisiti descritti nelle sezioni precedenti.  Per un esempio, vedere [Creare ed eseguire l'associazione a un oggetto ObservableCollection](../../../../docs/framework/wpf/data/how-to-create-and-bind-to-an-observablecollection.md).  Prima di implementare una raccolta personalizzata, considerare la possibilità di utilizzare <xref:System.Collections.ObjectModel.ObservableCollection%601> o una delle classi di raccolte esistenti, ad esempio <xref:System.Collections.Generic.List%601>, <xref:System.Collections.ObjectModel.Collection%601> e <xref:System.ComponentModel.BindingList%601>.  
  
 WPF non esegue mai direttamente l'associazione a una raccolta.  Se si specifica una raccolta come origine di associazione, WPF crea effettivamente l'associazione alla visualizzazione predefinita della raccolta.  Per informazioni sulle visualizzazioni predefinite, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
 Se in un scenario avanzato si desidera implementare una raccolta personalizzata, è possibile utilizzare l'interfaccia <xref:System.Collections.IList>.  <xref:System.Collections.IList> fornisce una raccolta non generica di oggetti cui è possibile accedere singolarmente in base all'indice, con un possibile miglioramento delle prestazioni.  
  
<a name="permissions"></a>   
## Requisiti di autorizzazione in un'associazione dati  
 Quando si crea un'associazione dati, è necessario considerare il livello di attendibilità dell'applicazione.  Nella tabella seguente vengono riepilogati i tipi di proprietà ai quali è possibile stabilire l'associazione in un'applicazione eseguita con attendibilità totale o attendibilità parziale:  
  
|Tipo proprietà<br /><br /> \(tutti i modificatori di accesso\)|Proprietà dell'oggetto dinamico|Proprietà dell'oggetto dinamico|Proprietà CLR|Proprietà CLR|Proprietà di dipendenza|Proprietà di dipendenza|  
|------------------------------------------------------------|-------------------------------------|-------------------------------------|-------------------|-------------------|-----------------------------|-----------------------------|  
|**Livello di attendibilità**|**Attendibilità totale**|**Attendibilità parziale**|**Attendibilità totale**|**Attendibilità parziale**|**Attendibilità totale**|**Attendibilità parziale**|  
|Classe pubblica|Sì|Sì|Sì|Sì|Sì|Sì|  
|Classe non pubblica|Sì|No|Sì|No|Sì|Sì|  
  
 In questa tabella vengono illustrati punti importanti relativi ai requisiti di autorizzazione per l'associazione dati:  
  
-   Per le proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], l'associazione dati funziona purché il motore di associazione sia in grado di accedere alla proprietà di origine di associazione utilizzando la reflection.  In caso contrario, viene generato un avviso relativo all'impossibilità di trovare la proprietà e viene utilizzato il valore di fallback o quello predefinito, se disponibile.  
  
-   È possibile creare associazioni alle proprietà degli oggetti dinamici definiti in fase di compilazione o di esecuzione.  
  
-   È sempre possibile stabilire l'associazione alle [proprietà di dipendenza](GTMT).  
  
 Il requisito di autorizzazione per l'associazione [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] è simile. In un sandbox con attendibilità parziale, si verifica una condizione di errore se <xref:System.Windows.Data.XmlDataProvider> non dispone delle autorizzazioni per accedere ai dati specificati.  
  
 Gli oggetti con un tipo anonimo sono interni.  È possibile creare associazioni a proprietà di tipi anonimi solo durante l'esecuzione con attendibilità totale.  Per ulteriori informazioni sui tipi anonimi, vedere [Tipi anonimi \(Guida per programmatori C\#\)](../Topic/Anonymous%20Types%20\(C%23%20Programming%20Guide\).md) o [Tipi anonimi \(Visual Basic\)](../Topic/Anonymous%20Types%20\(Visual%20Basic\).md) \(Visual Basic\).  
  
 Per ulteriori informazioni sulla sicurezza dell'attendibilità parziale, vedere [Sicurezza con attendibilità parziale in WPF](../../../../docs/framework/wpf/wpf-partial-trust-security.md).  
  
## Vedere anche  
 <xref:System.Windows.Data.ObjectDataProvider>   
 <xref:System.Windows.Data.XmlDataProvider>   
 [Specificare l'origine di associazione](../../../../docs/framework/wpf/data/how-to-specify-the-binding-source.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)   
 [Cenni preliminari sull'associazione dati WPF con LINQ to XML](../Topic/WPF%20Data%20Binding%20with%20LINQ%20to%20XML%20Overview.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)