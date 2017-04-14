---
title: "Procedura: rendere i dati disponibili per l&#39;associazione in XAML | Microsoft Docs"
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
  - "associazione dati, rendere i dati disponibili"
  - "associazione dati, rendere i dati disponibili per l'associazione"
ms.assetid: 7103c2e8-0e31-4a13-bf12-ca382221a8d5
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: rendere i dati disponibili per l&#39;associazione in XAML
In questo argomento vengono analizzate le diverse modalità in cui è possibile rendere i dati disponibili per l'associazione in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], in base alle esigenze dell'applicazione.  
  
## Esempio  
 Se si dispone di un oggetto [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] a cui si desidera eseguire l'associazione da [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è possibile renderlo disponibile per l'associazione definendolo come risorsa e assegnando a esso una `x:Key`.  Nell'esempio riportato di seguito, è presente un oggetto `Person` con una proprietà stringa denominata `PersonName`.  L'oggetto `Person` è definito nello spazio dei nomi denominato `SDKSample`.  
  
 [!code-xml[SimpleBinding#Instantiation](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#instantiation)]  
[!code-xml[SimpleBinding#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#2)]  
  
 Successivamente sarà possibile eseguire l'associazione all'oggetto in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], come illustrato nell'esempio riportato di seguito.  
  
 [!code-xml[SimpleBinding#BDO1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#bdo1)]  
  
 In alternativa, è possibile utilizzare la classe <xref:System.Windows.Data.ObjectDataProvider>, come nell'esempio riportato di seguito:  
  
 [!code-xml[SimpleBinding#ODPCP](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Page1.xaml#odpcp)]  
  
 Definire l'associazione nello stesso modo:  
  
 [!code-xml[SimpleBinding#BDO1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#bdo1)]  
  
 In questo esempio, il risultato è lo stesso: si ottiene un oggetto <xref:System.Windows.Controls.TextBlock> con il contenuto di testo `Joe`.  Tuttavia, la classe <xref:System.Windows.Data.ObjectDataProvider> fornisce funzionalità come la possibilità di eseguire l'associazione al risultato di un metodo.  È possibile scegliere di utilizzare la classe <xref:System.Windows.Data.ObjectDataProvider> nel caso siano necessarie le funzionalità da essa fornite.  
  
 Tuttavia, se si esegue l'associazione a un oggetto che è già stato creato, è necessario impostare `DataContext` nel codice, come nell'esempio riportato di seguito.  
  
 [!code-csharp[ADODataSet#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml.cs#1)]
 [!code-vb[ADODataSet#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ADODataSet/VisualBasic/Window1.xaml.vb#1)]  
  
 Per accedere ai dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] per l'associazione mediante la classe <xref:System.Windows.Data.XmlDataProvider>, vedere [Eseguire l'associazione ai dati XML utilizzando un oggetto XMLDataProvider e le query XPath](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md).  Per accedere ai dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] per l'associazione mediante la classe <xref:System.Windows.Data.ObjectDataProvider>, vedere [Esecuzione dell'associazione ai risultati di una query XDocument, XElement o LINQ to XML](../../../../docs/framework/wpf/data/how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md).  
  
 Per informazioni sulle diverse modalità con cui è possibile specificare i dati a cui si esegue l'associazione, vedere [Specificare l'origine di associazione](../../../../docs/framework/wpf/data/how-to-specify-the-binding-source.md).  Per informazioni sui tipi di dati a cui è possibile eseguire l'associazione o sulle modalità per implementare gli oggetti [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] per l'associazione, vedere [Cenni preliminari sulle origini di associazione](../../../../docs/framework/wpf/data/binding-sources-overview.md).  
  
## Vedere anche  
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)