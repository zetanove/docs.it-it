---
title: "Procedura: eseguire l&#39;associazione a dati XML tramite un oggetto XMLDataProvider e query XPath | Microsoft Docs"
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
  - "associazione, a dati XML tramite query XMLDataProvider"
  - "associazione dati, associazione a dati XML tramite query XMLDataProvider"
  - "XmlDataProvider, associazione a dati XML"
ms.assetid: 7dcd018f-16aa-4870-8e47-c1b4ea31e574
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Procedura: eseguire l&#39;associazione a dati XML tramite un oggetto XMLDataProvider e query XPath
In questo esempio viene illustrato come eseguire l'associazione a dati [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] utilizzando <xref:System.Windows.Data.XmlDataProvider>.  
  
 Con <xref:System.Windows.Data.XmlDataProvider>, i dati sottostanti a cui è possibile accedere attraverso l'associazione dati dell'applicazione possono essere una qualsiasi struttura ad albero di nodi [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)].  In altre parole, <xref:System.Windows.Data.XmlDataProvider> offre un modo pratico per utilizzare una qualsiasi struttura ad albero di nodi [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] come [origine di associazione](GTMT).  
  
## Esempio  
 Nell'esempio riportato di seguito, i dati sono incorporati direttamente come *isola di dati* [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] nella sezione <xref:System.Windows.FrameworkElement.Resources%2A>.  Un'isola di dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] deve essere racchiusa tra tag `<x:XData>` e deve avere sempre un singolo nodo radice che, in questo esempio, è *Inventory*.  
  
> [!NOTE]
>  Il nodo radice dei dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] ha un attributo **xmlns** che imposta lo spazio dei nomi [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] su una stringa vuota.  Si tratta di un requisito per l'applicazione di query XPath a un'isola di dati inline nella pagina [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  In questo caso inline, [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], e di conseguenza l'isola di dati, ereditano lo spazio dei nomi di <xref:System.Windows>.  Per questo motivo, è necessario lasciare vuoto lo spazio dei nomi per impedire che le query XPath siano qualificate dallo spazio dei nomi di <xref:System.Windows>, che le indirizzerebbe in modo errato.  
  
 [!code-xml[XMLDataSource#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSource/CS/Window1.xaml#1)]  
  
 Come illustrato in questo esempio, per creare la stessa dichiarazione di associazione nella sintassi dell'attributo è necessario utilizzare correttamente i caratteri di escape per i caratteri speciali.  Per ulteriori informazioni, vedere [Entità carattere XML e XAML](../../../../docs/framework/xaml-services/xml-character-entities-and-xaml.md).  
  
 Quando viene eseguito questo esempio, in <xref:System.Windows.Controls.ListBox> saranno visualizzati gli elementi riportati di seguito.  Si tratta dei *Title* di tutti gli elementi in *Books* con un valore *Stock* di "*out*" o un valore *Number* di 3 o maggiore di o uguale a 8.  Si noti che non vengono restituiti elementi *CD* perché il valore <xref:System.Windows.Data.XmlDataProvider.XPath%2A> impostato su <xref:System.Windows.Data.XmlDataProvider> indica che dovrebbero essere esposti solo gli elementi *Books* \(sostanzialmente impostando un filtro\).  
  
 ![Esempio di XPath](../../../../docs/framework/wpf/data/media/xpathexample.png "XPathExample")  
  
 In questo esempio, i titoli dei libri vengono visualizzati perché <xref:System.Windows.Data.Binding.XPath%2A> dell'associazione <xref:System.Windows.Controls.TextBlock> in <xref:System.Windows.DataTemplate> è impostato su "*Title*".  Se si desidera visualizzare il valore di un attributo, ad esempio *ISBN*, è necessario impostare il valore <xref:System.Windows.Data.Binding.XPath%2A> su "`@ISBN`".  
  
 Le proprietà **XPath** in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono gestite dal metodo XmlNode.SelectNodes.  È possibile modificare le query **XPath** per ottenere risultati diversi.  Di seguito sono riportati alcuni esempi di query <xref:System.Windows.Data.Binding.XPath%2A> eseguite sull'oggetto <xref:System.Windows.Controls.ListBox> associato nell'esempio precedente.  
  
-   `XPath="Book[1]"` restituirà il primo elemento del libro \("XML nell'azione"\).  Si noti che gli indici **XPath** sono basati su 1, non su 0.  
  
-   `XPath="Book[@*]"` restituirà tutti gli elementi del libro con qualsiasi attributo.  
  
-   `XPath="Book[last()-1]"` restituirà dal secondo all'ultimo elemento del libro \("Introduzione a Microsoft .NET"\).  
  
-   `XPath="*[position()>3]"` restituirà tutti gli elementi del libro ad eccezione dei primi 3.  
  
 Quando viene eseguita una query **XPath**, viene restituito un oggetto <xref:System.Xml.XmlNode> o un elenco di XmlNodes.  Poiché <xref:System.Xml.XmlNode> è un oggetto [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)], è possibile utilizzare la proprietà <xref:System.Windows.Data.Binding.Path%2A> per l'associazione alle proprietà [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)].  Si consideri nuovamente l'esempio precedente.  Se viene lasciato invariato il resto dell'esempio e l'associazione <xref:System.Windows.Controls.TextBlock> viene modificata come indicato di seguito, i nomi degli oggetti XmlNode restituiti saranno visualizzati in <xref:System.Windows.Controls.ListBox>.  In questo caso, il nome di tutti i nodi restituiti è "*Book*".  
  
 [!code-xml[XmlDataSourceVariation#XmlNodePath](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSourceVariation/CS/Page1.xaml#xmlnodepath)]  
  
 In alcune applicazioni, incorporare [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] come isola di dati nell'origine della pagina [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] può risultare poco pratico perché il contenuto esatto dei dati deve essere conosciuto in fase di compilazione.  Pertanto, è anche possibile ottenere i dati da un file [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] esterno, come nell'esempio seguente.  
  
 [!code-xml[XMLDataSource2#XmlFileExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSource2/CS/Window1.xaml#xmlfileexample)]  
  
 Se i dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] risiedono in un file [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] remoto, l'accesso ai dati viene definito assegnando un [!INCLUDE[TLA2#tla_url](../../../../includes/tla2sharptla-url-md.md)] adatto all'attributo <xref:System.Windows.Data.XmlDataProvider.Source%2A> come indicato di seguito.  
  
```  
<XmlDataProvider x:Key="BookData" Source="http://MyUrl" XPath="Books"/>  
```  
  
## Vedere anche  
 <xref:System.Windows.Data.ObjectDataProvider>   
 [Esecuzione dell'associazione ai risultati di una query XDocument, XElement o LINQ to XML](../../../../docs/framework/wpf/data/how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md)   
 [Utilizzare il modello Master\-Details con dati XML gerarchici](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)   
 [Cenni preliminari sulle origini di associazione](../../../../docs/framework/wpf/data/binding-sources-overview.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)