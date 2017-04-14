---
title: "Procedura: associare dati a elementi Windows Presentation Foundation (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "associazione dati, WCF Data Services"
  - "WCF Data Services, associazione dati"
ms.assetid: d6538ab0-0abe-426a-b9d9-e6f3a5ca2016
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: associare dati a elementi Windows Presentation Foundation (WCF Data Services)
Con [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] è possibile associare elementi Windows Presentation Foundation \(WPF\) quale un oggetto <xref:System.Windows.Controls.ListBox>``o <xref:System.Windows.Controls.ComboBox> a un'istanza di <xref:System.Data.Services.Client.DataServiceCollection%601> che gestisce gli eventi generati dai controlli per mantenere l'oggetto <xref:System.Data.Services.Client.DataServiceContext> sincronizzato con le modifiche apportate ai dati nei controlli.  Per altre informazioni, vedere [Associazione di dati a controlli](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md).  
  
 Nell'esempio riportato in questo argomento vengono usati il servizio dati Northwind di esempio e le classi del servizio dati client generate automaticamente.  Questo servizio e le classi di dati client vengono creati al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
## Esempio  
 L'esempio seguente è tratto dalla pagina code\-behind per una pagina XAML \(Extensible Application Markup Language\) che definisce la finestra `SalesOrders` in WPF.  Quando la finestra viene caricata, viene creato un oggetto <xref:System.Data.Services.Client.DataServiceCollection%601> in base al risultato di una query che restituisce i clienti filtrati per paese.  Tutte le pagine di questo risultato di paging vengono caricate insieme agli ordini correlati e vengono associate alla proprietà <xref:System.Windows.FrameworkElement.DataContext%2A> dell'oggetto <xref:System.Windows.Controls.StackPanel> che rappresenta il controllo di layout radice per la finestra WPF.  Per altre informazioni, vedere [Caricamento di contenuto posticipato](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md).  
  
 [!code-csharp[Astoria Northwind Client#BindPagedData](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderswpf3.xaml.cs#bindpageddata)]
 [!code-vb[Astoria Northwind Client#BindPagedData](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf3.xaml.vb#bindpageddata)]  
  
## Esempio  
 Nel codice XAML seguente viene definita la finestra `SalesOrders` in WPF per l'esempio precedente.  
  
 [!code-xml[Astoria Northwind Client#BindPagedDataXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf3.xaml#bindpageddataxaml)]  
  
## Esempio  
 L'esempio seguente è tratto dalla pagina code\-behind per una pagina XAML \(Extensible Application Markup Language\) che definisce la finestra `SalesOrders` in WPF.  Quando la finestra viene caricata, viene creato un oggetto <xref:System.Data.Services.Client.DataServiceCollection%601> in base al risultato di una query che restituisce i clienti con gli oggetti correlati filtrati per paese.  Questo risultato viene associato alla proprietà <xref:System.Windows.FrameworkElement.DataContext%2A> dell'oggetto <xref:System.Windows.Controls.StackPanel> che rappresenta il controllo di layout radice per la finestra WPF.  
  
 [!code-csharp[Astoria Northwind Client#WpfDataBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderswpf.xaml.cs#wpfdatabinding)]
 [!code-vb[Astoria Northwind Client#WpfDataBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf.xaml.vb#wpfdatabinding)]  
  
## Esempio  
 Nel codice XAML seguente viene definita la finestra `SalesOrders` in WPF per l'esempio precedente.  
  
 [!code-xml[Astoria Northwind Client#WpfDataBindingXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf.xaml#wpfdatabindingxaml)]