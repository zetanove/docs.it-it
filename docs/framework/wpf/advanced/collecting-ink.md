---
title: "Raccolta di input penna | Microsoft Docs"
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
  - "raccolta input penna digitale"
  - "DefaultDrawingAttributes (proprietà)"
  - "input penna digitale, raccolta"
  - "DrawingAttributes (proprietà)"
  - "input penna, raccolta"
  - "InkCanvas (elemento)"
  - "proprietà, DefaultDrawingAttributes"
  - "proprietà, DrawingAttributes"
ms.assetid: 66a3129d-9577-43eb-acbd-56c147282016
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Raccolta di input penna
La raccolta di input penna è una delle funzionalità principali della piattaforma [Windows Presentation Foundation](../../../../docs/framework/wpf/index.md).  In questo argomento vengono illustrati i metodi per la raccolta di input penna in [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)].  
  
## Prerequisiti  
 Per utilizzare gli esempi seguenti è necessario innanzitutto installare [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)] e [!INCLUDE[TLA2#tla_winfxsdk](../../../../includes/tla2sharptla-winfxsdk-md.md)].  È inoltre necessario disporre di conoscenze su come scrivere applicazioni per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Per ulteriori informazioni sull'utilizzo di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md).  
  
## Utilizzo dell'elemento InkCanvas  
 L'elemento <xref:System.Windows.Controls.InkCanvas> rappresenta il modo più semplice per raccogliere input penna in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  L'elemento <xref:System.Windows.Controls.InkCanvas> è simile all'oggetto <xref:Microsoft.Ink.InkOverlay> disponibile in [!INCLUDE[TLA2#tla_tpclssdk](../../../../includes/tla2sharptla-tpclssdk-md.md)]e nelle versioni precedenti.  
  
 Utilizzare un elemento <xref:System.Windows.Controls.InkCanvas> per ricevere e visualizzare input penna.  In genere, l'input penna viene effettuato tramite uno stilo che interagisce con un digitalizzatore per produrre i tratti.  È inoltre possibile utilizzare un mouse invece di uno stilo.  I tratti creati sono rappresentati come oggetti <xref:System.Windows.Ink.Stroke> e possono essere modificati sia a livello di codice sia tramite input dell'utente.  L'elemento <xref:System.Windows.Controls.InkCanvas> consente agli utenti di selezionare, modificare o eliminare un oggetto <xref:System.Windows.Ink.Stroke> esistente.  
  
 Con XAML, è possibile configurare raccolte di input penna con la stessa facilità con cui si aggiunge un elemento `InkCanvas` alla struttura ad albero.  Nell'esempio riportato di seguito viene aggiunto un oggetto <xref:System.Windows.Controls.InkCanvas> a un progetto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] predefinito creato in [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)].  
  
 [!code-xml[DigitalInkTopics#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#6)]  
  
 L'elemento `InkCanvas` può anche contenere elementi figlio, rendendo possibile l'aggiunta di funzionalità di annotazione a penna a quasi tutti i tipi di elementi XAML.  Ad esempio, per aggiungere funzionalità di input penna a un elemento di testo, è sufficiente trasformarlo in un elemento figlio di un oggetto <xref:System.Windows.Controls.InkCanvas>.  
  
 [!code-xml[DigitalInkTopics#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#5)]  
  
 L'aggiunta del supporto per contrassegnare un'immagine con input penna è altrettanto semplice.  
  
 [!code-xml[DigitalInkTopics#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#7)]  
  
### Modalità InkCollection  
 L'oggetto <xref:System.Windows.Controls.InkCanvas> fornisce supporto per varie modalità di input tramite la proprietà <xref:System.Windows.Controls.InkCanvas.EditingMode%2A>.  
  
### Modifica di input penna  
 L'oggetto <xref:System.Windows.Controls.InkCanvas> fornisce supporto per numerose operazioni di modifica di input penna.  Ad esempio, <xref:System.Windows.Controls.InkCanvas> supporta la cancellazione con la gomma della penna senza la necessità di codice supplementare per aggiungere tale funzionalità all'elemento.  
  
#### Selection  
 Per impostare la modalità di selezione è sufficiente impostare la proprietà <xref:System.Windows.Controls.InkCanvasEditingMode> su **Select**.  Nel codice seguente viene impostata la modalità di modifica in base al valore di <xref:System.Windows.Forms.CheckBox>:  
  
 [!code-csharp[DigitalInkTopics#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#8)]
 [!code-vb[DigitalInkTopics#8](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#8)]  
  
#### DrawingAttributes  
 Utilizzare la proprietà <xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> per modificare l'aspetto dei tratti di input penna.  Ad esempio, il membro <xref:System.Windows.Ink.DrawingAttributes.Color%2A> di <xref:System.Windows.Ink.DrawingAttributes> consente di impostare il colore dell'oggetto <xref:System.Windows.Ink.Stroke> sottoposto a rendering.  Nell'esempio riportato di seguito viene impostato il colore dei tratti selezionati su rosso.  
  
 [!code-csharp[DigitalInkTopics#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#9)]
 [!code-vb[DigitalInkTopics#9](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#9)]  
  
### DefaultDrawingAttributes  
 La proprietà <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> consente di accedere a proprietà quali l'altezza, l'ampiezza e il colore dei tratti da creare in un oggetto <xref:System.Windows.Controls.InkCanvas>.  Una volta modificata la proprietà <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>, tutti i futuri tratti immessi nell'oggetto <xref:System.Windows.Controls.InkCanvas> verranno sottoposti a rendering con i nuovi valori della proprietà.  
  
 Oltre che per modificare la proprietà <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> nel file code\-behind, è possibile utilizzare la sintassi XAML per specificare le proprietà <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>.  Nel codice XAML riportato di seguito viene illustrato come impostare la proprietà <xref:System.Windows.Ink.DrawingAttributes.Color%2A>.  Per utilizzare questo codice, creare un nuovo progetto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] denominato "HelloInkCanvas" in Visual Studio 2005.  Sostituire il codice nel file Window1.xaml con il codice seguente.  
  
 [!code-xml[HelloInkCanvas#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HelloInkCanvas/CSharp/Window1.xaml#1)]  
  
 Successivamente, aggiungere i seguenti gestori eventi di pulsanti al file code\-behind, nella classe Window1.  
  
 [!code-csharp[HelloInkCanvas#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HelloInkCanvas/CSharp/Window1.xaml.cs#2)]  
  
 Dopo avere copiato il codice, premere **F5** in Microsoft Visual Studio 2005 per eseguire il programma nel debugger.  
  
 Si noti il modo in cui l'oggetto <xref:System.Windows.Controls.StackPanel> colloca i pulsanti nella parte superiore dell'oggetto <xref:System.Windows.Controls.InkCanvas>.  Se si tenta di inserire input penna sopra i pulsanti, l'oggetto <xref:System.Windows.Controls.InkCanvas> raccoglie l'input penna e ne esegue il rendering sotto i pulsanti.  Questa situazione si verifica poiché i pulsanti sono elementi di pari livello dell'oggetto <xref:System.Windows.Controls.InkCanvas> al contrario dell'elemento figlio.  Inoltre, poiché i pulsanti sono più in alto nell'ordine z, il rendering dell'input penna viene eseguito sotto di loro.  
  
## Vedere anche  
 <xref:System.Windows.Ink.DrawingAttributes>   
 <xref:System.Windows.InkCanvas.DefaultDrawingAttributes%2A>   
 <xref:System.Windows.Ink>