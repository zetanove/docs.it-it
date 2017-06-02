---
title: "Procedura: eseguire l&#39;override dei metadati per una propriet&#224; di dipendenza | Microsoft Docs"
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
  - "proprietà di dipendenza, override di metadati"
  - "metadati, override per proprietà Dependency"
  - "override di metadati per proprietà Dependency"
ms.assetid: f90f026e-60d8-428a-933d-edf0dba4441f
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: eseguire l&#39;override dei metadati per una propriet&#224; di dipendenza
In questo esempio viene mostrato come eseguire l'override dei metadati delle proprietà di dipendenza predefiniti che provengono da una classe ereditata, chiamando il metodo <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> e fornendo metadati specifici del tipo.  
  
## Esempio  
 Tramite la definizione del relativo oggetto <xref:System.Windows.PropertyMetadata>, una classe può specificare i comportamenti della [proprietà di dipendenza](GTMT), ad esempio il valore predefinito e i callback del sistema di proprietà.  Molte classi della proprietà di dipendenza dispongono già di metadati predefiniti stabiliti come parte del processo di registrazione.  Sono incluse le proprietà di dipendenza che fanno parte delle [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Una classe che eredita la proprietà di dipendenza tramite l'ereditarietà di classe può eseguire l'override dei metadati originali in modo che le caratteristiche della proprietà che è possibile modificare tramite i metadati soddisfino qualsiasi requisito specifico della sottoclasse.  
  
 L'override dei metadati di una proprietà di dipendenza deve essere eseguito prima che la proprietà venga resa utilizzabile dal sistema di proprietà, ovvero nel momento in cui vengono create istanze specifiche degli oggetti che registrano la proprietà.  Le chiamate a <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> devono essere eseguite all'interno dei costruttori statici del tipo che fornisce se stesso come parametro `forType` di <xref:System.Windows.DependencyProperty.OverrideMetadata%2A>.  Il tentativo di modificare i metadati dopo la creazione delle istanze del tipo di proprietario non genererà eccezioni, ma darà come risultato comportamenti incoerenti nel sistema della proprietà.  Inoltre, l'override di metadati può essere eseguito solo una volta per tipo.  I successivi tentativi di eseguire l'override dei metadati sullo stesso tipo genereranno un'eccezione.  
  
 Nell'esempio seguente, la classe personalizzata `MyAdvancedStateControl` esegue l'override dei metadati forniti per `StateProperty` da `MyAdvancedStateControl` con i nuovi metadati delle proprietà.  Ad esempio, il valore predefinito di `StateProperty` sarà `true` quando viene eseguita una query sulla proprietà in un'istanza `MyAdvancedStateControl` appena creata.  
  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
[!code-csharp[PropertySystemEsoterics#MyAdvancedStateControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#myadvancedstatecontrol)]
[!code-vb[PropertySystemEsoterics#MyAdvancedStateControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#myadvancedstatecontrol)]  
  
## Vedere anche  
 <xref:System.Windows.DependencyProperty>   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/properties-how-to-topics.md)