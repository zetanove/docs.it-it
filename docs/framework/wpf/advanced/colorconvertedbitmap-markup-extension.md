---
title: "Estensione del markup ColorConvertedBitmap | Microsoft Docs"
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
  - "estensione di markup ColorConvertedBitmap"
  - "XAML, estensione di markup ColorConvertedBitmap"
ms.assetid: 18321c18-c898-4470-93fa-a702b47770c1
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Estensione del markup ColorConvertedBitmap
Fornisce una modalità per specificare un'origine bitmap priva di profilo incorporato.  Spazi e profili colore sono specificati dall'[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)], così come l'[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] dell'origine dell'immagine.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object property="{ColorConvertedBitmap imageSource sourceIIC destinationIIC}" .../>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`imageSource`|[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] della bitmap senza profilo.|  
|`sourceIIC`|[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] della configurazione del profilo di origine.|  
|`destinationIIC`|[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] della configurazione del profilo di destinazione|  
  
## Note  
 Questa estensione di markup ha lo scopo di riempire un insieme correlato di valori di proprietà dell'origine dell'immagine, ad esempio <xref:System.Windows.Media.Imaging.BitmapImage.UriSource%2A>.  
  
 La sintassi per gli attributi è quella più comunemente utilizzata con questa estensione di markup.  Non è possibile utilizzare `ColorConvertedBitmap` \(o `ColorConvertedBitmapExtension`\) nella sintassi per gli elementi proprietà, poiché i valori possono essere impostati solo come valori sul costruttore iniziale, che è la stringa successiva all'identificatore dell'estensione.  
  
 `ColorConvertedBitmap` è un'estensione di markup.  Le estensioni di markup in genere vengono implementate quando per i valori dell'attributo devono essere utilizzati caratteri escape in modo che non vengano considerati come valori letterali o nomi di gestori e il requisito è più globale del semplice utilizzo di convertitori dei tipi su alcuni tipi o proprietà.  Tutte le estensioni di markup di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] utilizzano i caratteri { e } nella relativa sintassi degli attributi. Grazie a questa convenzione il processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] è in grado di rilevare la necessità che l'attributo venga elaborato da un'estensione di markup.  Per ulteriori informazioni, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.Imaging.BitmapImage.UriSource%2A>   
 [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)