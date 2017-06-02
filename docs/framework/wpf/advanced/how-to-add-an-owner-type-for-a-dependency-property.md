---
title: "Procedura: aggiungere un tipo di proprietario per una propriet&#224; di dipendenza | Microsoft Docs"
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
  - "classi, aggiunta come proprietarie di proprietà Dependency"
  - "proprietà di dipendenza, aggiunta di classi come proprietarie"
ms.assetid: edcce050-0576-4edb-a31a-3f909637b452
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: aggiungere un tipo di proprietario per una propriet&#224; di dipendenza
In questo esempio viene mostrato come aggiungere una classe come proprietario di una proprietà di dipendenza registrata per un tipo diverso.  In questo modo, il lettore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e il sistema di proprietà sono entrambi in grado di riconoscere la classe come proprietario aggiuntivo della proprietà.  L'aggiunta come proprietario consente alla classe aggiunta di fornire metadati specifici per il tipo.  
  
 Nell'esempio seguente, `StateProperty` è una proprietà registrata dalla classe `MyStateControl`.  La classe `UnrelatedStateControl` viene aggiunta come proprietario di `StateProperty` utilizzando il metodo <xref:System.Windows.DependencyProperty.AddOwner%2A> che utilizza in modo specifico la firma che consente nuovi metadati per la proprietà di dipendenza presente sul tipo aggiunto.  Notare che è necessario fornire funzioni di accesso [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] per la proprietà in modo simile a quanto avviene nell'esempio mostrato nell'esempio [Implementare una proprietà di dipendenza](../../../../docs/framework/wpf/advanced/how-to-implement-a-dependency-property.md), nonché esporre nuovamente l'identificatore della proprietà di dipendenza nella classe aggiunta come proprietario.  
  
 Senza wrapper, la proprietà di dipendenza funzionerebbe ancora dal punto di vista dell'accesso a livello di codice utilizzando l'oggetto <xref:System.Windows.DependencyObject.GetValue%2A> o <xref:System.Windows.DependencyObject.SetValue%2A>.  Tuttavia, è preferibile affiancare questo comportamento del sistema di proprietà con i wrapper della proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] .  I wrapper semplificano l'impostazione a livello di codice della proprietà di dipendenza e rendono possibile l'impostazione delle proprietà come attributi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 Per ulteriori informazioni su come eseguire l'override dei metadati predefiniti, vedere [Eseguire l'override dei metadati per una proprietà di dipendenza](../../../../docs/framework/wpf/advanced/how-to-override-metadata-for-a-dependency-property.md).  
  
## Esempio  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
[!code-csharp[PropertySystemEsoterics#UnrelatedStateControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#unrelatedstatecontrol)]
[!code-vb[PropertySystemEsoterics#UnrelatedStateControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#unrelatedstatecontrol)]  
  
## Vedere anche  
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)