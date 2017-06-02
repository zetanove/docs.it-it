---
title: "Procedura: eseguire l&#39;associazione a un servizio Web | Microsoft Docs"
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
  - "associazione dati, servizio Web"
  - "associazione dati, servizio Web"
  - "servizio Web (associazione)"
ms.assetid: 77e2d373-69ba-4cbd-b6f5-2c83c38fc98b
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: eseguire l&#39;associazione a un servizio Web
Nell'esempio riportato di seguito viene illustrato come eseguire l'associazione a oggetti restituiti dalle chiamate al metodo di servizio Web.  
  
## Esempio  
 In questo esempio viene utilizzato [MSDN\/TechNet Publishing System \(MTPS\) Content Service](http://go.microsoft.com/fwlink/?LinkId=95677) per recuperare l'elenco di lingue supportate da uno specifico documento.  
  
 Prima di chiamare un servizio Web, è necessario creare un relativo riferimento.  Per creare un riferimento Web al servizio MTPS utilizzando [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)], attenersi alla seguente procedura.  
  
1.  Aprire il progetto in [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)].  
  
2.  Scegliere **Aggiungi riferimento Web** dal menu **Progetto**.  
  
3.  Nella finestra di dialogo, impostare l'**URL** su [http:\/\/services.msdn.microsoft.com\/contentservices\/contentservice.asmx?wsdl](http://services.msdn.microsoft.com/contentservices/contentservice.asmx?wsdl).  
  
4.  Premere **Vai** e quindi **Aggiungi riferimento**.  
  
 Successivamente, chiamare il metodo di servizio Web e impostare <xref:System.Windows.FrameworkElement.DataContext%2A> del controllo o finestra appropriati sull'oggetto restituito.  Il metodo **GetContent** del servizio MTPS accetta un riferimento all'oggetto **getContentRequest**.  Pertanto, nell'esempio riportato di seguito viene impostato prima un oggetto della richiesta:  
  
 [!code-csharp[BindToWebService#Namespace](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToWebService/CSharp/Window1.xaml.cs#namespace)]
 [!code-vb[BindToWebService#Namespace](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BindToWebService/VisualBasic/Window1.xaml.vb#namespace)]  
[!code-csharp[BindToWebService#WebServiceCall](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToWebService/CSharp/Window1.xaml.cs#webservicecall)]
[!code-vb[BindToWebService#WebServiceCall](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BindToWebService/VisualBasic/Window1.xaml.vb#webservicecall)]  
  
 Dopo aver impostato <xref:System.Windows.FrameworkElement.DataContext%2A>, è possibile creare associazioni alle proprietà dell'oggetto su cui è stato impostato <xref:System.Windows.FrameworkElement.DataContext%2A>.  In questo esempio, <xref:System.Windows.FrameworkElement.DataContext%2A> è impostato sull'oggetto **getContentResponse** restituito dal metodo **GetContent**.  Nell'esempio riportato di seguito, <xref:System.Windows.Controls.ItemsControl> viene associato e visualizza i valori **locale** di **availableVersionsAndLocales** di **getContentResponse**.  
  
 [!code-xml[BindToWebService#Binding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToWebService/CSharp/Window1.xaml#binding)]  
  
 Per informazioni sulla struttura di **getContentResponse**, vedere [Content Service documentation](http://services.msdn.microsoft.com/ContentServices/ContentService.asmx) \(informazioni in lingua inglese\).  
  
## Vedere anche  
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sulle origini di associazione](../../../../docs/framework/wpf/data/binding-sources-overview.md)   
 [Rendere i dati disponibili per l'associazione in XAML](../../../../docs/framework/wpf/data/how-to-make-data-available-for-binding-in-xaml.md)