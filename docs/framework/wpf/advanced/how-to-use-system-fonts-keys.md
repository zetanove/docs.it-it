---
title: "Procedura: utilizzare chiavi di caratteri del sistema | Microsoft Docs"
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
  - "chiavi di risorsa, SystemFonts (classe)"
  - "SystemFonts (classe)"
ms.assetid: 036ebea7-5677-4f60-8ba4-56c9f9d9b8bd
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: utilizzare chiavi di caratteri del sistema
Le risorse di sistema espongono diversi parametri di sistema come risorse per consentire agli sviluppatori la creazione di elementi visivi coerenti con le impostazioni del sistema.  La classe <xref:System.Windows.SystemFonts> contiene sia i valori sia le risorse dei tipi di carattere del sistema associati ai valori, ad esempio <xref:System.Windows.SystemFonts.CaptionFontFamily%2A> e <xref:System.Windows.SystemFonts.CaptionFontFamilyKey%2A>.  
  
 Le metriche dei tipi di carattere del sistema possono essere utilizzate come risorse statiche o come risorse dinamiche.  Utilizzare una risorsa dinamica se si desidera che le metriche dei tipi di carattere vengano automaticamente aggiornate durante l'esecuzione dell'applicazione. In caso contrario, utilizzare una risorsa statica.  
  
> [!NOTE]
>  Al nome della proprietà delle risorse dinamiche viene aggiunta la parola chiave *Key*.  
  
 Nell'esempio riportato di seguito viene illustrato come accedere alle risorse dinamiche dei tipi di carattere del sistema e utilizzarle per personalizzare un pulsante o assegnarvi uno stile.  In questo esempio di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] viene creato uno stile pulsante che assegna valori <xref:System.Windows.SystemFonts> a un pulsante.  
  
## Esempio  
 [!code-xml[SystemRes_snip#FontDynamicResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/MyApp.xaml#fontdynamicresources)]  
  
## Vedere anche  
 [Disegnare un'area con un pennello di sistema](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)   
 [Utilizzare SystemParameters](../../../../docs/framework/wpf/advanced/how-to-use-systemparameters.md)   
 [Utilizzare la classe SystemFonts](../../../../docs/framework/wpf/advanced/how-to-use-systemfonts.md)