---
title: "Panoramica sul controllo ToolTip | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "controlli, Descrizione comando"
  - "ToolTip (controllo), informazioni sul controllo ToolTip"
ms.assetid: f06c1603-e9cb-4809-8a62-234607fc52f7
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Panoramica sul controllo ToolTip
Una descrizione comandi è una piccola finestra popup che viene visualizzata quando l'utente posiziona il puntatore del mouse su un elemento, ad esempio <xref:System.Windows.Controls.Button>.  In questo argomento viene definita la descrizione comandi e viene descritto come creare e personalizzare il relativo contenuto.  
  
   
  
<a name="what_is_a_tooltip"></a>   
## Definizione di descrizione comandi  
 Quando un utente sposta il puntatore del mouse su un elemento associato a una descrizione comandi, viene visualizzata una finestra con il relativo contenuto \(ad esempio contenuto di testo in cui viene descritta la funzione di un controllo\) per un intervallo di tempo specificato.  Se l'utente rimuove il puntatore del mouse dal controllo, la finestra scompare perché il contenuto della descrizione comandi non può ricevere lo stato attivo.  
  
 Il contenuto di una descrizione comandi può essere costituito da una o più righe di testo, immagini, forme o altro contenuto visivo.  Per definire una descrizione comandi per un controllo, impostare una delle proprietà seguenti sul contenuto della descrizione comandi.  
  
-   <xref:System.Windows.FrameworkContentElement.ToolTip%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.FrameworkElement.ToolTip%2A?displayProperty=fullName>  
  
 La proprietà da utilizzare varia a seconda che il controllo che definisce la descrizione comandi erediti dalla classe <xref:System.Windows.FrameworkContentElement> o <xref:System.Windows.FrameworkElement>.  
  
<a name="create_tooltip"></a>   
## Creazione di una descrizione comandi  
 Nell'esempio seguente viene illustrato come creare una semplice descrizione comandi impostando la proprietà <xref:System.Windows.FrameworkElement.ToolTip%2A> per un controllo <xref:System.Windows.Controls.Button> su una stringa di testo.  
  
 [!code-xml[GroupBoxSnippet#ToolTipString](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#tooltipstring)]  
  
 È anche possibile definire una descrizione comandi come oggetto <xref:System.Windows.Controls.ToolTip>.  Nell'esempio seguente viene utilizzato [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] per specificare un oggetto <xref:System.Windows.Controls.ToolTip> come descrizione comandi di un elemento <xref:System.Windows.Controls.TextBox>.  Si noti che l'oggetto <xref:System.Windows.Controls.ToolTip> viene specificato impostando la proprietà <xref:System.Windows.FrameworkElement.ToolTip%2A?displayProperty=fullName>.  
  
 [!code-xml[ToolTipSimple#ToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml#tooltip)]  
  
 Nell'esempio seguente viene utilizzato codice per generare un oggetto <xref:System.Windows.Controls.ToolTip>.  Viene creato un oggetto <xref:System.Windows.Controls.ToolTip> \(`tt`\) che viene associato a un oggetto <xref:System.Windows.Controls.Button>.  
  
 [!code-csharp[ToolTipSimple#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml.cs#2)]
 [!code-vb[ToolTipSimple#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipSimple/VisualBasic/Window1.xaml.vb#2)]  
  
 È anche possibile creare contenuto della descrizione comandi non definito come oggetto <xref:System.Windows.Controls.ToolTip> racchiudendo tale contenuto in un elemento di layout, ad esempio <xref:System.Windows.Controls.DockPanel>.  Nell'esempio seguente viene illustrato come impostare la proprietà <xref:System.Windows.FrameworkElement.ToolTip%2A> di un oggetto <xref:System.Windows.Controls.TextBox> sul contenuto racchiuso in un controllo <xref:System.Windows.Controls.DockPanel>.  
  
 [!code-xml[GroupBoxSnippet#ToolTipDockPanel](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#tooltipdockpanel)]  
  
<a name="Using_the_ToolTip_and_ToolTipService_Properties"></a>   
## Utilizzo delle proprietà delle classi ToolTip e ToolTipService  
 È possibile personalizzare il contenuto della descrizione comandi impostando proprietà visive e applicando stili.  Se il contenuto della descrizione comandi viene definito come oggetto <xref:System.Windows.Controls.ToolTip>, è possibile impostare le proprietà visive dell'oggetto <xref:System.Windows.Controls.ToolTip>.  In caso contrario, è necessario impostare [proprietà connesse](GTMT) equivalenti sulla classe <xref:System.Windows.Controls.ToolTipService>.  
  
 Per un esempio di come impostare le proprietà per specificare la posizione del contenuto della descrizione comandi utilizzando le proprietà <xref:System.Windows.Controls.ToolTip> e <xref:System.Windows.Controls.ToolTipService>, vedere [Posizionare un oggetto ToolTip](../../../../docs/framework/wpf/controls/how-to-position-a-tooltip.md).  
  
<a name="StylingToolTip"></a>   
## Applicazione di stili a una descrizione comandi  
 È possibile applicare uno stile a un oggetto <xref:System.Windows.Controls.ToolTip> definendo un oggetto <xref:System.Windows.Style> personalizzato.  Nell'esempio seguente viene definito un oggetto <xref:System.Windows.Style> denominato `Simple` che illustra come eseguire l'offset del posizionamento dell'oggetto <xref:System.Windows.Controls.ToolTip> e come modificarne l'aspetto impostando <xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A>, <xref:System.Windows.Controls.Control.FontSize%2A> e <xref:System.Windows.Controls.Control.FontWeight%2A>.  
  
 [!code-xml[ToolTipSimple#Style](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml#style)]  
  
<a name="UsingtheToolTipServiceTimeIntervalProperties"></a>   
## Utilizzo delle proprietà di ToolTipService relative all'intervallo di tempo  
 La classe <xref:System.Windows.Controls.ToolTipService> fornisce le proprietà seguenti per impostare i tempi di visualizzazione della descrizione comandi: <xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A>, <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> e <xref:System.Windows.Controls.ToolTipService.ShowDuration%2A>.  
  
 Utilizzare le proprietà <xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A> e <xref:System.Windows.Controls.ToolTipService.ShowDuration%2A> per specificare un ritardo, in genere breve, prima che venga visualizzato un oggetto <xref:System.Windows.Controls.ToolTip> e anche per specificare la durata della visualizzazione di <xref:System.Windows.Controls.ToolTip>.  Per ulteriori informazioni, vedere [How to: Delay the Display of a ToolTip](http://msdn.microsoft.com/it-it/618e05ef-f2bf-4a53-a0f4-aacb49918bd7).  
  
 La proprietà <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> determina se le descrizioni comandi di controlli diversi vengono visualizzate senza un ritardo iniziale quando il puntatore del mouse viene spostato rapidamente da uno all'altro.  Per ulteriori informazioni sulla proprietà <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A>, vedere [Utilizzare la proprietà BetweenShowDelay](../../../../docs/framework/wpf/controls/how-to-use-the-betweenshowdelay-property.md).  
  
 Nell'esempio seguente viene illustrato come impostare queste proprietà per una descrizione comandi.  
  
 [!code-xml[ToolTipService#ToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.ToolTipService>   
 <xref:System.Windows.Controls.ToolTip>   
 <xref:System.Windows.Controls.ToolTipEventArgs>   
 <xref:System.Windows.Controls.ToolTipEventHandler>   
 [Procedure relative](../../../../docs/framework/wpf/controls/tooltip-how-to-topics.md)