---
title: "Procedura: utilizzare SystemParameters | Microsoft Docs"
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
  - "classi, SystemParameters"
  - "SystemParameters (classe)"
ms.assetid: 02e7a5de-94eb-4953-b91c-52e6c872ad5b
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Procedura: utilizzare SystemParameters
In questo esempio viene illustrato come accedere e utilizzare le proprietà di <xref:System.Windows.SystemParameters> per disegnare o personalizzare un pulsante.  
  
## Esempio  
 Le risorse di sistema espongono molti valori basati sul sistema come risorse per consentire la creazione di elementi visivi coerenti con le impostazioni del sistema.  <xref:System.Windows.SystemParameters> è una classe che contiene sia le proprietà del valore del parametro di sistema sia le chiavi di risorsa associate ai valori.  Ad esempio, <xref:System.Windows.SystemParameters.FullPrimaryScreenHeight%2A> è un valore della proprietà <xref:System.Windows.SystemParameters> e <xref:System.Windows.SystemParameters.FullPrimaryScreenHeightKey%2A> è la chiave di risorsa corrispondente.  
  
 In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è possibile utilizzare i membri di <xref:System.Windows.SystemParameters> come utilizzo di proprietà statica o riferimenti di risorsa dinamici, con il valore della proprietà statica come chiave.  Utilizzare un riferimento di risorsa dinamica per aggiornare automaticamente il valore basato su sistema durante l'esecuzione dell'applicazione; in caso contrario utilizzare un riferimento statico.  Nelle chiavi di risorsa il suffisso `Key` viene aggiunto al nome della proprietà.  
  
 Nell'esempio riportato di seguito viene illustrato come accedere e utilizzare i valori statici di <xref:System.Windows.SystemParameters> per disegnare o personalizzare un pulsante.  In questo esempio di markup viene ridimensionato un pulsante mediante l'applicazione dei valori <xref:System.Windows.SystemParameters>.  
  
 [!code-xml[SystemRes_snip#ParameterStaticResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml#parameterstaticresources)]  
  
 Per utilizzare i valori di <xref:System.Windows.SystemParameters> nel codice non è necessario utilizzare riferimenti statici o riferimenti di risorsa dinamica.  Utilizzare invece i valori della classe <xref:System.Windows.SystemParameters>.  Anche se le proprietà non chiave sono apparentemente definite come proprietà statiche, il comportamento in fase di esecuzione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitato dal sistema rivaluterà le proprietà in tempo reale e risponderà correttamente alle modifiche apportate dall'utente ai valori di sistema. Nell'esempio riportato di seguito viene illustrato come impostare la larghezza e l'altezza di un pulsante utilizzando valori <xref:System.Windows.SystemParameters>.  
  
 [!code-csharp[SystemRes_snip#ParameterResourcesCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml.cs#parameterresourcescode)]
 [!code-vb[SystemRes_snip#ParameterResourcesCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SystemRes_snip/VisualBasic/Pane1.xaml.vb#parameterresourcescode)]  
  
## Vedere anche  
 <xref:System.Windows.SystemParameters>   
 [Disegnare un'area con un pennello di sistema](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)   
 [Utilizzare la classe SystemFonts](../../../../docs/framework/wpf/advanced/how-to-use-systemfonts.md)   
 [Utilizzare le chiavi dei parametri di sistema](../../../../docs/framework/wpf/advanced/how-to-use-system-parameters-keys.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/resources-how-to-topics.md)