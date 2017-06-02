---
title: "Procedura: utilizzare le risorse delle applicazioni | Microsoft Docs"
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
  - "risorse delle applicazioni"
  - "risorse, risorse delle applicazioni"
ms.assetid: 507ea937-5191-406b-8797-0a3d9f94156d
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: utilizzare le risorse delle applicazioni
In questo esempio viene illustrato come utilizzare le risorse delle applicazioni.  
  
## Esempio  
 Nell'esempio seguente viene illustrato un file di definizione dell'applicazione \(ADF\).  Questo file definisce una sezione delle risorse \(un valore per la proprietà <xref:System.Windows.Application.Resources%2A>\).  Le risorse definite a livello di applicazione sono accessibili da tutte le altre pagine che fanno parte dell'applicazione.  In questo caso, la risorsa è uno stile dichiarato.  Poiché uno stile completo che include un modello di controllo può richiedere molto tempo, in questo esempio viene omesso il modello di controllo definito all'interno del metodo di impostazione della proprietà <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> dello stile.  
  
 [!code-xml[ResourcesApplication#PreTemplateResource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ResourcesApplication/CS/app.xaml#pretemplateresource)]  
[!code-xml[ResourcesApplication#PostTemplateResource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ResourcesApplication/CS/app.xaml#posttemplateresource)]  
  
 Nell'esempio seguente viene illustrata una pagina [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] che fa riferimento alla risorsa a livello di applicazione definita nell'esempio precedente.  Il riferimento alla risorsa viene creato utilizzando un'[Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) che specifica la chiave di risorsa univoca per la risorsa richiesta.  Nella pagina corrente non è stata rilevata alcuna risorsa con chiave "GelButton", pertanto l'ambito di ricerca per la risorsa richiesta continua oltre la pagina corrente e nelle risorse definite a livello di applicazione.  
  
 [!code-xml[ResourcesApplication#ConsumingPage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ResourcesApplication/CS/page1.xaml#consumingpage)]  
  
## Vedere anche  
 [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [Cenni preliminari sulla gestione di applicazioni](../../../../docs/framework/wpf/app-development/application-management-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/resources-how-to-topics.md)