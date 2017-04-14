---
title: "Procedura: implementare una propriet&#224; di dipendenza | Microsoft Docs"
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
  - "proprietà di dipendenza, supporto di proprietà"
  - "proprietà, supporto con proprietà Dependency"
ms.assetid: 855fd6d7-19ac-493c-bf5e-2f40b57cdc92
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: implementare una propriet&#224; di dipendenza
In questo esempio viene mostrato come supportare una proprietà [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] con un campo <xref:System.Windows.DependencyProperty>, definendo una [proprietà di dipendenza](GTMT).  Quando si definiscono proprietà personalizzate e si desidera che queste supportino numerosi aspetti della funzionalità [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], inclusi stili, associazione dati, ereditarietà, animazione e valori predefiniti, è necessario implementarle come [proprietà di dipendenza](GTMT).  
  
## Esempio  
 Nell'esempio seguente viene innanzitutto registrata una [proprietà di dipendenza](GTMT) chiamando il metodo <xref:System.Windows.DependencyProperty.Register%2A>.  Il nome del campo dell'identificatore utilizzato per memorizzare il nome e le caratteristiche della [proprietà di dipendenza](GTMT) deve essere l'oggetto <xref:System.Windows.DependencyProperty.Name%2A> scelto per la proprietà di dipendenza come parte della chiamata <xref:System.Windows.DependencyProperty.Register%2A>, aggiunta dalla stringa letterale `Property`.  Ad esempio, se si registra una proprietà di dipendenza con una proprietà <xref:System.Windows.DependencyProperty.Name%2A> di `Location`, il campo dell'identificatore definito per la proprietà di dipendenza deve essere denominato `LocationProperty`.  
  
 In questo esempio, il nome della [proprietà di dipendenza](GTMT) e la relativa funzione di accesso [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] è `State`; il campo dell'identificatore è `StateProperty`; il tipo della proprietà è <xref:System.Boolean> e il tipo che registra la [proprietà di dipendenza](GTMT) è `MyStateControl`.  
  
 Se non si riesce a seguire questo modello di denominazione, la proprietà potrebbe non essere segnalata correttamente nelle finestre di progettazione e alcuni aspetti dell'applicazione di stili del sistema di proprietà potrebbero non funzionare nel modo previsto.  
  
 Inoltre, è possibile specificare i metadati predefiniti per una [proprietà di dipendenza](GTMT).  In questo esempio viene registrato il valore predefinito della  `State` [proprietà di dipendenza](GTMT) affinché sia `false`.  
  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
  
 Per ulteriori informazioni sulla modalità e sui motivi dell'implementazione di una [proprietà di dipendenza](GTMT), in contrapposizione al semplice supporto di una proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] con un campo privato, vedere [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  
  
## Vedere anche  
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/properties-how-to-topics.md)