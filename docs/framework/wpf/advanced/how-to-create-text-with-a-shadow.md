---
title: "Procedura: creare testo con ombreggiatura | Microsoft Docs"
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
  - "effetto ombreggiatura nel testo"
  - "testo, nascosti"
  - "tipografia, effetti ombreggiatura"
ms.assetid: 6ab9c754-6001-4708-b479-5367f2fd1a35
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: creare testo con ombreggiatura
Negli esempi di questa sezione viene illustrato come creare un effetto di ombreggiatura per il testo visualizzato.  
  
## Esempio  
 L'oggetto <xref:System.Windows.Media.Effects.DropShadowEffect> consente di creare una varietà di effetti di ombreggiatura per gli oggetti [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  Nell'esempio riportato di seguito viene illustrato un effetto di ombreggiatura applicato al testo.  Poiché in questo caso l'ombreggiatura è sfumata, il colore dell'ombreggiatura sarà sfocato.  
  
 ![Ombreggiatura del testo con Softness &#61; 0,25](../../../../docs/framework/wpf/advanced/media/shadowtext01.png "ShadowText01")  
Esempio di testo con un'ombreggiatura sfumata  
  
 È possibile controllare la larghezza dell'ombreggiatura impostando la proprietà <xref:System.Windows.Media.Effects.DropShadowEffect.ShadowDepth%2A>.  Un valore pari a `4.0` indica una larghezza dell'ombreggiatura di 4 pixel.  È possibile controllare la sfumatura, o sfocatura, di un'ombreggiatura modificando la proprietà <xref:System.Windows.Media.Effects.DropShadowEffect.BlurRadius%2A>.  Un valore di `0.0` indica l'assenza di sfocatura.  Nell'esempio di codice riportato di seguito viene illustrato come creare un'ombreggiatura sfumata.  
  
 [!code-xml[TextShadowSnippets#TextShadowSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/SingleShadows.xaml#textshadowsnippet1)]  
  
> [!NOTE]
>  Questi effetti di ombreggiatura non vengono applicati alla pipeline del rendering del testo di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  Di conseguenza, ClearType è disabilitato quando si utilizzano tali effetti.  
  
 Nell'esempio riportato di seguito viene illustrato un effetto di ombreggiatura piena applicato al testo.  In questo caso, l'ombreggiatura non è sfocata.  
  
 ![Ombreggiatura del testo con Softness &#61; 0](../../../../docs/framework/wpf/advanced/media/shadowtext02.png "ShadowText02")  
Esempio di testo con un'ombreggiatura piena  
  
 È possibile creare un'ombreggiatura piena impostando la proprietà <xref:System.Windows.Media.Effects.DropShadowEffect.BlurRadius%2A> su `0.0`, che indica che non viene utilizzata nessuna sfocatura.  È possibile controllare la direzione dell'ombreggiatura modificando la proprietà <xref:System.Windows.Media.Effects.DropShadowEffect.Direction%2A>.  Impostare il valore direzionale di questa proprietà su un grado compreso tra `0` e `360`.  Nell'illustrazione seguente vengono illustrati i valori direzionali dell'impostazione della proprietà <xref:System.Windows.Media.Effects.DropShadowEffect.Direction%2A>.  
  
 ![Impostazione del grado DropShadow dell'ombreggiatura](../../../../docs/framework/wpf/advanced/media/shadowtext08.png "ShadowText08")  
Diagramma di direzione DropShadow  
  
 Nell'esempio di codice riportato di seguito viene illustrato come creare un'ombreggiatura piena.  
  
 [!code-xml[TextShadowSnippets#TextShadowSnippet2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/SingleShadows.xaml#textshadowsnippet2)]  
  
## Utilizzo di un effetto di sfocatura  
 È possibile utilizzare un oggetto <xref:System.Windows.Media.Effects.BlurBitmapEffect> per creare un effetto simile all'ombreggiatura che può essere posizionato dietro un oggetto di testo.  Un effetto bitmap di sfocatura applicato consente di sfocare il testo in tutte le direzioni in modo uniforme.  
  
 Nell'esempio riportato di seguito viene illustrato un effetto di sfocatura applicato al testo.  
  
 ![Ombreggiatura del testo con BlurBitmapEffect](../../../../docs/framework/wpf/advanced/media/shadowtext06.png "ShadowText06")  
Esempio di testo con un effetto di sfocatura  
  
 Nell'esempio di codice riportato di seguito viene illustrato come creare un effetto di sfocatura.  
  
 [!code-xml[TextShadowSnippets#TextShadowSnippet6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/BlurShadows.xaml#textshadowsnippet6)]  
  
## Utilizzo di una trasformazione di traslazione  
 È possibile utilizzare un oggetto <xref:System.Windows.Media.TranslateTransform> per creare un effetto simile all'ombreggiatura che può essere posizionato dietro un oggetto di testo.  
  
 Nell'esempio di codice riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.TranslateTransform> per applicare un offset al testo.  In questo esempio, una copia del testo con un leggero offset sotto il testo primario crea un effetto di ombreggiatura.  
  
 ![Ombreggiatura del testo con TranslateTransform](../../../../docs/framework/wpf/advanced/media/shadowtext07.png "ShadowText07")  
Esempio di testo che utilizza una trasformazione per un effetto di ombreggiatura  
  
 Nell'esempio di codice riportato di seguito viene illustrato come creare una trasformazione per un effetto di ombreggiatura.  
  
 [!code-xml[TextShadowSnippets#TextShadowSnippet7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/TransformShadows.xaml#textshadowsnippet7)]