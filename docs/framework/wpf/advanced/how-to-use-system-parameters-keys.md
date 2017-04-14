---
title: "Procedura: utilizzare chiavi dei parametri di sistema | Microsoft Docs"
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
  - "chiavi di risorsa, SystemParameters (classe)"
  - "SystemParameters (classe)"
ms.assetid: 77571283-d16c-45bb-9f69-cafbbf72b21e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: utilizzare chiavi dei parametri di sistema
Le risorse di sistema espongono diversi parametri di sistema come risorse per consentire agli sviluppatori la creazione di elementi visivi coerenti con le impostazioni del sistema.  <xref:System.Windows.SystemParameters> è una classe che contiene sia i valori dei parametri di sistema sia le chiavi di risorsa associate ai valori, ad esempio <xref:System.Windows.SystemParameters.FullPrimaryScreenHeight%2A> e <xref:System.Windows.SystemParameters.FullPrimaryScreenHeightKey%2A>.  Le metriche dei parametri di sistema possono essere utilizzate come risorse statiche o come risorse dinamiche.  Utilizzare una risorsa dinamica se si desidera che le metriche dei parametri vengano automaticamente aggiornate durante l'esecuzione dell'applicazione. In caso contrario, utilizzare una risorsa statica.  
  
> [!NOTE]
>  Al nome della proprietà delle risorse dinamiche viene aggiunta la parola chiave *Key*.  
  
 Nell'esempio riportato di seguito viene illustrato come accedere e utilizzare le risorse dinamiche dei parametri di sistema per applicare uno stile o personalizzare un pulsante.  In questo esempio di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] viene ridimensionato un pulsante mediante l'assegnazione dei valori <xref:System.Windows.SystemParameters> alla larghezza e all'altezza del pulsante.  
  
## Esempio  
 [!code-xml[SystemRes_snip#ParameterDynamicResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/MyApp.xaml#parameterdynamicresources)]  
  
## Vedere anche  
 [Disegnare un'area con un pennello di sistema](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)   
 [Utilizzare la classe SystemFonts](../../../../docs/framework/wpf/advanced/how-to-use-systemfonts.md)   
 [Utilizzare SystemParameters](../../../../docs/framework/wpf/advanced/how-to-use-systemparameters.md)