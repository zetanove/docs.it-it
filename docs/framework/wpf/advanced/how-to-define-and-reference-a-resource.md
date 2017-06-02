---
title: "Procedura: definire e fare riferimento a una risorsa | Microsoft Docs"
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
  - "definizione di risorse"
  - "riferimento a risorse"
  - "risorse, definizione"
  - "risorse, riferimento"
ms.assetid: b86b876b-0a10-489b-9a5d-581ea9b32406
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: definire e fare riferimento a una risorsa
In questo esempio viene mostrato come definire e fare riferimento a una risorsa utilizzando un attributo in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  
  
## Esempio  
 Nell'esempio riportato di seguito vengono definiti due tipi di risorse: una risorsa <xref:System.Windows.Media.SolidColorBrush> e più risorse <xref:System.Windows.Style>.  La risorsa `MyBrush` di tipo <xref:System.Windows.Media.SolidColorBrush> viene utilizzata per ottenere il valore di diverse proprietà, ognuna delle quali accetta un valore di tipo <xref:System.Windows.Media.Brush>.  Le risorse <xref:System.Windows.Style> `PageBackground`, `TitleText` e `Label` sono destinate ciascuna a un particolare tipo di controllo.  Gli stili consentono di impostare diverse proprietà sui controlli di destinazione se, per fare riferimento a tale risorsa di stile che viene utilizzata per impostare la proprietà <xref:System.Windows.FrameworkElement.Style%2A> di diversi elementi di controllo specifici definiti in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], si utilizza la chiave di risorsa.  
  
 Notare che una delle proprietà all'interno dei metodi di impostazione dello stile `Label` fa riferimento anche alla risorsa `MyBrush` definita in precedenza.  Si tratta di una tecnica comune; tuttavia è importante ricordare che le risorse vengono analizzate e inserite in un dizionario nell'ordine in cui vengono specificate.  Le risorse vengono inoltre richieste nell'ordine rilevato all'interno del dizionario, se si utilizza [Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) per fare riferimento a queste risorse dall'interno di un'altra risorsa.  Verificare che qualsiasi risorsa a cui si fa riferimento venga definita, all'interno della raccolta delle risorse, in una posizione precedente rispetto a quella in cui tale risorsa è richiesta.  Se necessario, è possibile ovviare al rigido ordine di creazione dei riferimenti alle risorse utilizzando un oggetto [Estensione del markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md) per fare riferimento alla risorsa in fase di esecuzione, ma occorre tenere presente che questa tecnica DynamicResource incide sulle prestazioni.  Per informazioni dettagliate, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
 [!code-xml[FEResource#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResource/CS/default.xaml#xaml)]  
  
## Vedere anche  
 [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)