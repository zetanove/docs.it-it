---
title: "Procedura: utilizzare la classe SystemFonts | Microsoft Docs"
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
  - "classi, SystemFonts"
  - "tipi di carattere, caratteri del sistema"
  - "caratteri del sistema"
  - "SystemFonts (classe)"
ms.assetid: 3f46a4ec-2225-408a-8123-8838a8f7057a
caps.latest.revision: 27
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Procedura: utilizzare la classe SystemFonts
In questo esempio viene illustrato come utilizzare le risorse statiche della classe <xref:System.Windows.SystemFonts> per disegnare o personalizzare un pulsante.  
  
## Esempio  
 Le risorse di sistema espongono molti valori determinati dal sistema come risorse e proprietà per consentire la creazione di elementi visivi coerenti con le impostazioni del sistema.  <xref:System.Windows.SystemFonts> è una classe che contiene valori del tipo di carattere del sistema come proprietà statiche e proprietà che fanno riferimento a chiavi di risorse che è possibile utilizzare per accedere dinamicamente a tali valori in fase di esecuzione.  Ad esempio, <xref:System.Windows.SystemFonts.CaptionFontFamily%2A> è un valore di <xref:System.Windows.SystemFonts> e <xref:System.Windows.SystemFonts.CaptionFontFamilyKey%2A> è una chiave di risorsa corrispondente.  
  
 In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è possibile utilizzare i membri di <xref:System.Windows.SystemFonts> come proprietà statiche o riferimenti di risorsa dinamica, con il valore della proprietà statica come chiave.  Utilizzare un riferimento di risorsa dinamica per aggiornare automaticamente la metrica del tipo di carattere durante l'esecuzione dell'applicazione; in caso contrario utilizzare un riferimento di valore statico.  
  
> [!NOTE]
>  Nelle chiavi di risorsa il suffisso "Key" viene aggiunto al nome della proprietà.  
  
 Nell'esempio riportato di seguito viene mostrato come accedere e utilizzare le proprietà di <xref:System.Windows.SystemFonts> come valori statici per disegnare o personalizzare un pulsante.  In questo esempio di markup vengono assegnati valori <xref:System.Windows.SystemFonts> a un pulsante.  
  
 [!code-xml[SystemRes_snip#FontStaticResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml#fontstaticresources)]  
  
 Per utilizzare i valori di <xref:System.Windows.SystemFonts> nel codice non è necessario utilizzare un riferimento di valore statico o di risorsa dinamica.  Utilizzare invece le proprietà non chiave della classe <xref:System.Windows.SystemFonts>.  Anche se le proprietà non chiave sono apparentemente definite come proprietà statiche, il comportamento in fase di esecuzione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitato dal sistema rivaluterà le proprietà in tempo reale e risponderà correttamente alle modifiche apportate dall'utente ai valori di sistema.  Nell'esempio riportato di seguito viene illustrato come specificare le impostazioni del tipo di carattere di un pulsante.  
  
 [!code-csharp[SystemRes_snip#FontResourcesCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml.cs#fontresourcescode)]
 [!code-vb[SystemRes_snip#FontResourcesCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SystemRes_snip/VisualBasic/Pane1.xaml.vb#fontresourcescode)]  
  
## Vedere anche  
 <xref:System.Windows.SystemFonts>   
 [Disegnare un'area con un pennello di sistema](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)   
 [Utilizzare SystemParameters](../../../../docs/framework/wpf/advanced/how-to-use-systemparameters.md)   
 [Utilizzare chiavi di caratteri del sistema](../../../../docs/framework/wpf/advanced/how-to-use-system-fonts-keys.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/resources-how-to-topics.md)   
 [Estensione del markup x:Static](../../../../docs/framework/xaml-services/x-static-markup-extension.md)   
 [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [Estensione del markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)