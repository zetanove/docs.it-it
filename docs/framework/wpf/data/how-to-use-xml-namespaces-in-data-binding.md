---
title: "Procedura: utilizzare gli spazi dei nomi XML nell&#39;associazione dati | Microsoft Docs"
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
  - "associazione dati, XML (spazi dei nomi)"
  - "spazi dei nomi, XML"
  - "XML, spazi dei nomi"
ms.assetid: a47c832f-dc84-48f2-96d5-cde18fc4284b
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: utilizzare gli spazi dei nomi XML nell&#39;associazione dati
## Esempio  
 In questo esempio viene illustrato come gestire gli spazi dei nomi specificati nell'[origine di associazione](GTMT) [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)].  
  
 Se i dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] presentano la seguente definizione dello spazio dei nomi [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]:  
  
 `<rss version="2.0" xmlns:dc="http://purl.org/dc/elements/1.1/">`  
  
 è possibile utilizzare l'elemento <xref:System.Windows.Data.XmlNamespaceMapping> per eseguire il mapping dello spazio dei nomi a un oggetto <xref:System.Windows.Data.XmlNamespaceMapping.Prefix%2A>, come mostrato nell'esempio seguente.  Successivamente è possibile utilizzare <xref:System.Windows.Data.XmlNamespaceMapping.Prefix%2A> per fare riferimento allo spazio dei nomi [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)].  Nella classe <xref:System.Windows.Controls.ListBox> dell'esempio vengono mostrati *titolo* e *data:doc* di ciascun *elemento*.  
  
 <!-- TODO: review snippet reference [!code-xml[XmlnsBind#XmlNamespaceMapping](../../../../samples/snippets/xaml/VS_Snippets_Wpf/XmlnsBind/XAML/Window1.xaml#xmlnamespacemapping)]  -->
 <!-- TODO: review snippet reference [!code-xml[XmlnsBind#XmlNamespaceMapping](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XmlnsBind/CS/Window1.xaml#xmlnamespacemapping)]  -->  
  
 Notare che l'oggetto <xref:System.Windows.Data.XmlNamespaceMapping.Prefix%2A> specificata non deve necessariamente coincidere con quello utilizzato nell'origine [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]; se il prefisso nell'origine [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] viene modificato, il mapping continua a essere eseguito correttamente.  
  
 In questo specifico esempio, sebbene i dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] provengano da un servizio Web, l'elemento <xref:System.Windows.Data.XmlNamespaceMapping> funzionerà anche con dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] o [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] inline in un file incorporato.  
  
## Vedere anche  
 [Eseguire l'associazione ai dati XML utilizzando un oggetto XMLDataProvider e le query XPath](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)