---
title: "Procedura: eseguire l&#39;associazione ai risultati di una query XDocument, XElement o LINQ to XML | Microsoft Docs"
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
  - "associazione dati (WPF), associazione a XDocument"
  - "associazione dati (WPF), associazione a XElement"
ms.assetid: 6a629a49-fe1c-465d-b76a-3dcbf4307b64
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Procedura: eseguire l&#39;associazione ai risultati di una query XDocument, XElement o LINQ to XML
In questo esempio viene illustrato come eseguire l'associazione dei dati XML a un oggetto <xref:System.Windows.Controls.ItemsControl> mediante <xref:System.Xml.Linq.XDocument>.  
  
## Esempio  
 Il codice XAML seguente definisce un oggetto <xref:System.Windows.Controls.ItemsControl> e include un modello di dati di tipo `Planet` nello spazio dei nomi XML `http://planetsNS`.  Un tipo di dati XML che occupa uno spazio dei nomi deve includere lo spazio dei nomi tra parentesi graffe e se risiede dove può essere presente un'estensione di markup XAML, è necessario anteporre allo spazio dei nomi una sequenza di escape tra parentesi graffe.  Questo codice esegue l'associazione a proprietà dinamiche che corrispondono ai metodi <xref:System.Xml.Linq.XContainer.Element%2A> e <xref:System.Xml.Linq.XElement.Attribute%2A> della classe <xref:System.Xml.Linq.XElement>.  Le proprietà dinamiche consentono al codice XAML di eseguire l'associazione a proprietà dinamiche che condividono i nomi dei metodi.  Per ulteriori informazioni, vedere [Proprietà dinamiche di LINQ to XML](../Topic/LINQ%20to%20XML%20Dynamic%20Properties.md).  La dichiarazione dello spazio dei nomi predefinita per XML non viene applicata ai nomi degli attributi.  
  
 [!code-xml[XLinqExample#StackPanelResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#stackpanelresources)]  
[!code-xml[XLinqExample#ItemsControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#itemscontrol)]  
  
 Il codice C\# seguente chiama il metodo <xref:System.Xml.Linq.XDocument.Load%2A> e imposta il contesto dati del pannello stack su tutti i sottoelementi dell'elemento denominato `SolarSystemPlanets` nello spazio dei nomi XML `http://planetsNS`.  
  
 [!code-csharp[XLinqExample#LoadDCFromFile](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#loaddcfromfile)]
 [!code-vb[XLinqExample#LoadDCFromFile](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#loaddcfromfile)]  
  
 I dati XML possono essere archiviati come risorsa XAML mediante <xref:System.Windows.Data.ObjectDataProvider>.  Per un esempio completo, vedere [Codice sorgente di L2DBForm.xaml](../Topic/L2DBForm.xaml%20Source%20Code.md).  Nell'esempio seguente viene illustrato come il codice può impostare il contesto dati su una risorsa dell'oggetto.  
  
 [!code-csharp[XLinqExample#LoadDCFromXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#loaddcfromxaml)]
 [!code-vb[XLinqExample#LoadDCFromXAML](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#loaddcfromxaml)]  
  
 Le proprietà dinamiche che eseguono il mapping a <xref:System.Xml.Linq.XContainer.Element%2A> e <xref:System.Xml.Linq.XElement.Attribute%2A> forniscono la flessibilità all'interno di XAML.  Il codice può inoltre eseguire l'associazione ai risultati di una query LINQ to XML.  In questo esempio viene eseguita l'associazione ai risultati della query ordinati in base al valore di un elemento.  
  
 [!code-csharp[XLinqExample#BindToResults](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#bindtoresults)]
 [!code-vb[XLinqExample#BindToResults](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#bindtoresults)]  
  
## Vedere anche  
 [Cenni preliminari sulle origini di associazione](../../../../docs/framework/wpf/data/binding-sources-overview.md)   
 [Cenni preliminari sull'associazione dati WPF con LINQ to XML](../Topic/WPF%20Data%20Binding%20with%20LINQ%20to%20XML%20Overview.md)   
 [Esempio di associazione dati di WPF con LINQ to XML](../Topic/WPF%20Data%20Binding%20Using%20LINQ%20to%20XML%20Example.md)   
 [Proprietà dinamiche di LINQ to XML](../Topic/LINQ%20to%20XML%20Dynamic%20Properties.md)