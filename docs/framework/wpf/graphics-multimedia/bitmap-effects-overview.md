---
title: "Cenni preliminari sugli effetti bitmap | Microsoft Docs"
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
  - "bitmap (effetti)"
ms.assetid: 23cb338e-4b59-4b52-b294-96431f9c9568
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 31
---
# Cenni preliminari sugli effetti bitmap
Gli effetti bitmap consentono a progettisti e sviluppatori di applicare effetti visivi a contenuto [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] dopo averlo sottoposto a rendering.  Gli effetti bitmap consentono ad esempio di applicare con facilità un effetto <xref:System.Windows.Media.Effects.DropShadowBitmapEffect> o un effetto sfocatura a un'immagine o un pulsante.  
  
> [!IMPORTANT]
>  In [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] o versione successiva, la classe <xref:System.Windows.Media.Effects.BitmapEffect> è obsoleta.  Se si tenta di utilizzare la classe <xref:System.Windows.Media.Effects.BitmapEffect>, si otterrà un'eccezione obsoleta.  L'alternativa non obsoleta alla classe <xref:System.Windows.Media.Effects.BitmapEffect> è la classe <xref:System.Windows.Media.Effects.Effect>.  La classe <xref:System.Windows.Media.Effects.Effect> consente di eseguire le operazioni in modo notevolmente più rapido.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="wpf_effects"></a>   
## Effetti bitmap WPF  
 Gli effetti bitmap \(oggetto<xref:System.Windows.Media.Effects.BitmapEffect> \) sono semplici operazioni di elaborazione dei pixel.  Un effetto bitmap accetta un oggetto <xref:System.Windows.Media.Imaging.BitmapSource> come input e produce un nuovo oggetto <xref:System.Windows.Media.Imaging.BitmapSource> dopo avere applicato l'effetto, ad esempio una sfocatura o un'ombreggiatura.  Ogni effetto bitmap espone proprietà che possono controllare le proprietà di filtro, ad esempio <xref:System.Windows.Media.Effects.BlurBitmapEffect.Radius%2A> di <xref:System.Windows.Media.Effects.BlurBitmapEffect>.  
  
 Come caso particolare, in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], gli effetti possono essere impostati come proprietà su oggetti <xref:System.Windows.Media.Visual> attivi, ad esempio <xref:System.Windows.Controls.Button> o <xref:System.Windows.Controls.TextBox>.  L'elaborazione dei pixel viene applicata e sottoposta a rendering in fase di esecuzione.  In questo caso, al momento del rendering, un elemento <xref:System.Windows.Media.Visual> viene convertito automaticamente nel relativo oggetto <xref:System.Windows.Media.Imaging.BitmapSource> equivalente e inserito come input di <xref:System.Windows.Media.Effects.BitmapEffect>.  L'output sostituisce il comportamento di rendering predefinito dell'elemento <xref:System.Windows.Media.Visual>.  Per questo motivo gli oggetti <xref:System.Windows.Media.Effects.BitmapEffect> impongono il rendering degli elementi visivi solo a livello del software,  senza accelerazione hardware sugli elementi visivi quando vengono applicati gli effetti.  
  
-   <xref:System.Windows.Media.Effects.BlurBitmapEffect> simula un oggetto sfuocato.  
  
-   Tramite <xref:System.Windows.Media.Effects.OuterGlowBitmapEffect> viene creato un alone di colore intorno al perimetro di un oggetto.  
  
-   Tramite <xref:System.Windows.Media.Effects.DropShadowBitmapEffect> viene creata un'ombra dietro un oggetto.  
  
-   Tramite <xref:System.Windows.Media.Effects.BevelBitmapEffect> viene creata una smussatura che solleva la superficie di un'immagine secondo una curva specificata.  
  
-   Tramite <xref:System.Windows.Media.Effects.EmbossBitmapEffect> viene creato un bump mapping di un oggetto <xref:System.Windows.Media.Visual> per dare l'impressione di profondità e trama dovute all'esposizione a una sorgente di luce artificiale.  
  
> [!NOTE]
>  Gli effetti bitmap [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] vengono sottoposti a rendering in modalità software.  Qualsiasi oggetto che applica un effetto verrà sottoposto a rendering in modalità software.  Le prestazioni peggiorano in modo più accentuato quando si utilizzano effetti bitmap su elementi visivi di grandi dimensioni o quando si animano le proprietà di un effetto bitmap.  Ciò non significa che gli effetti bitmap non devono mai essere utilizzati in questo modo, ma che è necessario prestare attenzione e fare numerosi test affinché gli utenti acquisiscano l'esperienza necessaria.  
  
> [!NOTE]
>  Gli effetti bitmap [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] non supportano l'esecuzione in situazioni di attendibilità parziale.  Un'applicazione deve disporre di autorizzazioni di attendibilità completa per l'utilizzo degli effetti bitmap.  
  
<a name="applyeffects"></a>   
## Come applicare un effetto  
 <xref:System.Windows.Media.Effects.BitmapEffect> è una proprietà sull'elemento <xref:System.Windows.Media.Visual>.  Pertanto, l'applicazione di effetti a elementi visivi, ad esempio <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.Image>, <xref:System.Windows.Media.DrawingVisual> o <xref:System.Windows.UIElement> è semplice quanto l'impostazione di una proprietà.  È possibile impostare la proprietà <xref:System.Windows.UIElement.BitmapEffect%2A> su un singolo oggetto <xref:System.Windows.Media.Effects.BitmapEffect> oppure concatenare più effetti utilizzando l'oggetto <xref:System.Windows.Media.Effects.BitmapEffectGroup>.  
  
 Nell'esempio riportato di seguito viene illustrato come applicare un <xref:System.Windows.Media.Effects.BitmapEffect> in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  
  
 [!code-xml[EffectsGallery_snip#BlurSimpleExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EffectsGallery_snip/CSharp/blursimpleexample.xaml#blursimpleexampleinline)]  
  
 Nell'esempio riportato di seguito viene illustrato come applicare un <xref:System.Windows.Media.Effects.BitmapEffect> nel codice.  
  
 [!code-csharp[EffectsGallery_snip#CodeBehindBlurCodeBehindExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EffectsGallery_snip/CSharp/blurcodebehindexample.xaml.cs#codebehindblurcodebehindexampleinline)]  
  
> [!NOTE]
>  Quando un <xref:System.Windows.Media.Effects.BitmapEffect> viene applicato a un contenitore di layout, ad esempio <xref:System.Windows.Controls.DockPanel> o <xref:System.Windows.Controls.Canvas>, l'effetto viene applicato alla struttura ad albero visuale dell'elemento o elemento visivo, inclusi tutti gli elementi figlio.  
  
<a name="customeffects"></a>   
## Creazione di effetti personalizzati  
 In [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] sono disponibili interfacce non gestite per creare effetti personalizzati da utilizzare nelle applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] gestite.  Per materiale di riferimento aggiuntivo per la creazione di effetti bitmap personalizzati, vedere la documentazione [Effetto bitmap WPF non gestito](_wibe_lh).  
  
## Vedere anche  
 <xref:System.Windows.Media.Effects.BitmapEffectGroup>   
 <xref:System.Windows.Media.Effects.BitmapEffectInput>   
 <xref:System.Windows.Media.Effects.BitmapEffectCollection>   
 [Unmanaged WPF Bitmap Effect](_wibe_lh)   
 [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)   
 [Sicurezza](../../../../docs/framework/wpf/security-wpf.md)   
 [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)