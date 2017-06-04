---
title: "Personalizzare il rendering dell&#39;input penna | Microsoft Docs"
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
  - "classi, DynamicRenderer"
  - "classi, InkCanvas"
  - "classi, Tratto"
  - "rendering personalizzato dell'input penna"
  - "DynamicRenderer (classe)"
  - "input penna, rendering personalizzato"
  - "InkCanvas (classe)"
  - "Stroke (classe)"
ms.assetid: 65c978a7-0ee0-454f-ac7f-b1bd2efecac5
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Personalizzare il rendering dell&#39;input penna
La proprietà <xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> di un tratto consente di specificarne l'aspetto, ovvero dimensioni, colore e forma. In alcuni casi potrebbe, tuttavia, essere necessario personalizzare particolari dell'aspetto non coperti dalla proprietà <xref:System.Windows.Ink.Stroke.DrawingAttributes%2A>.  È possibile personalizzare l'aspetto dell'input penna eseguendo il rendering nell'aspetto di un aerografo, di una pittura a olio e di molti altri effetti.  [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] consente di personalizzare il rendering dell'input penna implementando un oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> o <xref:System.Windows.Ink.Stroke> personalizzato.  
  
 In questo argomento sono contenute le seguenti sottosezioni:  
  
-   [Architettura](#Architecture)  
  
-   [Implementazione di un renderer dinamico](#ImplementingADynamicRenderer)  
  
-   [Implementing a Custom Stroke](#ImplementingACustomStroke)  
  
-   [Implementazione di un oggetto InkCanvas personalizzato](#ImplementingACustomInkCanvas)  
  
-   [Conclusione](#Conclusion)  
  
<a name="Architecture"></a>   
## Architettura  
 Il rendering dell'input penna viene eseguito due volte: quando l'utente scrive tramite una penna su un'apposita superficie e dopo l'aggiunta del tratto alla superficie di input penna.  L'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> esegue il rendering dell'input penna quando l'utente sposta la penna del Tablet PC sul digitalizzatore, mentre l'oggetto <xref:System.Windows.Ink.Stroke> esegue il rendering di se stesso dopo essere stato aggiunto a un elemento.  
  
 Per l'esecuzione dinamica del rendering dell'input penna è necessario implementare tre classi.  
  
1.  **DynamicRenderer**: implementare una classe che deriva da <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>.  Questa classe è un oggetto <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> specializzato che esegue il rendering del tratto mentre viene tracciato.  L'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> esegue il rendering su un thread separato, pertanto la superficie di input penna sembra raccogliere l'input penna anche quando il thread dell'interfaccia utente dell'applicazione è bloccato.  Per ulteriori informazioni sul modello di threading, vedere [Modello di threading dell'input penna](../../../../docs/framework/wpf/advanced/the-ink-threading-model.md).  Per personalizzare l'esecuzione dinamica di un tratto, eseguire l'override del metodo <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.OnDraw%2A>.  
  
2.  **Stroke**: implementare una classe che deriva da <xref:System.Windows.Ink.Stroke>.  Questa classe è responsabile del rendering statico dei dati dell'oggetto <xref:System.Windows.Input.StylusPoint> dopo la relativa conversione in un oggetto <xref:System.Windows.Ink.Stroke>.  Eseguire l'override del metodo <xref:System.Windows.Ink.Stroke.DrawCore%2A> per assicurarsi che il rendering statico del tratto sia coerente con il rendering dinamico.  
  
3.  **InkCanvas:** implementare una classe che deriva da <xref:System.Windows.Controls.InkCanvas>.  Assegnare l'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> personalizzato alla proprietà <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A>.  Eseguire l'override del metodo <xref:System.Windows.Controls.InkCanvas.OnStrokeCollected%2A> e aggiungere un tratto personalizzato alla proprietà <xref:System.Windows.Controls.InkCanvas.Strokes%2A>.  In questo modo, è possibile assicurarsi che l'aspetto dell'input penna sia coerente.  
  
<a name="ImplementingADynamicRenderer"></a>   
## Implementazione di un renderer dinamico  
 Sebbene la classe <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> sia una parte standard di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], per eseguire un rendering più specializzato, è necessario creare un renderer dinamico personalizzato che derivi dall'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> ed eseguire l'override del metodo <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.OnDraw%2A>.  
  
 Nell'esempio riportato di seguito viene illustrato un oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> personalizzato che disegna l'input penna con un effetto pennello a sfumatura lineare.  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#1)]
[!code-vb[AdvancedInkTopicsSamples#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#1)]  
  
<a name="ImplementingCustomStrokes"></a>   
## Implementazione di tratti personalizzati  
 Implementare una classe che derivi dall'oggetto <xref:System.Windows.Ink.Stroke>.  Questa classe è responsabile del rendering dei dati dell'oggetto <xref:System.Windows.Input.StylusPoint> dopo la relativa conversione in un oggetto <xref:System.Windows.Ink.Stroke>.  Eseguire l'override della classe <xref:System.Windows.Ink.Stroke.DrawCore%2A> per ottenere il disegno effettivo.  
  
 Nella classe Stroke è inoltre possibile archiviare dati personalizzati utilizzando il metodo <xref:System.Windows.Ink.Stroke.AddPropertyData%2A>.  Questi dati vengono archiviati con i dati del tratto quando sono resi persistenti.  
  
 La classe <xref:System.Windows.Ink.Stroke> può inoltre eseguire l'hit testing.  È inoltre possibile implementare un proprio algoritmo di hit testing eseguendo l'override del metodo <xref:System.Windows.Ink.Stroke.HitTest%2A> nella classe corrente.  
  
 Nel codice C\# riportato di seguito viene illustrata una classe <xref:System.Windows.Ink.Stroke> personalizzata che esegue il rendering dei dati dell'oggetto <xref:System.Windows.Input.StylusPoint> come tratto 3D.  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#2)]
[!code-vb[AdvancedInkTopicsSamples#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#2)]  
  
<a name="ImplementingACustomInkCanvas"></a>   
## Implementazione di un oggetto InkCanvas personalizzato  
 Il modo più semplice per utilizzare il tratto e l'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> personalizzato consiste nell'implementare una classe che deriva da <xref:System.Windows.Controls.InkCanvas> e utilizza queste classi.  L'oggetto <xref:System.Windows.Controls.InkCanvas> presenta una proprietà <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A> che specifica la modalità di rendering del tratto mentre l'utente lo disegna.  
  
 Per eseguire il rendering personalizzato dei tratti su un oggetto <xref:System.Windows.Controls.InkCanvas>, eseguire le seguenti operazioni:  
  
-   Creare una classe che deriva dall'oggetto <xref:System.Windows.Controls.InkCanvas>.  
  
-   Assegnare l'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> personalizzato alla proprietà <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A?displayProperty=fullName>.  
  
-   Eseguire l'override del metodo <xref:System.Windows.Controls.InkCanvas.OnStrokeCollected%2A>.  In questo metodo, rimuovere il tratto originale aggiunto all'oggetto InkCanvas.  Creare, quindi, un tratto personalizzato, aggiungerlo alla proprietà <xref:System.Windows.Controls.InkCanvas.Strokes%2A> e chiamare la classe base con un nuovo oggetto <xref:System.Windows.Controls.InkCanvasStrokeCollectedEventArgs> contenente il tratto personalizzato.  
  
 Nel codice C\# riportato di seguito viene illustrata una classe <xref:System.Windows.Controls.InkCanvas> personalizzata che utilizza un oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> personalizzato e raccoglie tratti personalizzati.  
  
 [!code-csharp[AdvancedInkTopicsSamples#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#9)]  
  
 Un oggetto <xref:System.Windows.Controls.InkCanvas> può avere più di un oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>.  È possibile aggiungere più oggetti <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> all'oggetto <xref:System.Windows.Controls.InkCanvas> aggiungendoli alla proprietà <xref:System.Windows.UIElement.StylusPlugIns%2A>.  
  
<a name="Conclusion"></a>   
## Conclusione  
 È possibile personalizzare l'aspetto dell'input penna derivando classi <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>, <xref:System.Windows.Ink.Stroke> e <xref:System.Windows.Controls.InkCanvas> personalizzate.  Insieme, queste classi assicurano che il tratto abbia un aspetto coerente quando l'utente lo disegna e dopo che viene raccolto.  
  
## Vedere anche  
 [Gestione avanzata dell'input penna](../../../../docs/framework/wpf/advanced/advanced-ink-handling.md)