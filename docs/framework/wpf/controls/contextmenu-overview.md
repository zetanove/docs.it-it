---
title: "Cenni preliminari sull&#39;oggetto ContextMenu | Microsoft Docs"
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
  - "ContextMenu (controlli) [WPF], informazioni sui controlli ContextMenu"
  - "controlli, ContextMenu"
ms.assetid: 16909c42-799a-4561-91e0-7d69dcfeea91
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Cenni preliminari sull&#39;oggetto ContextMenu
La classe <xref:System.Windows.Controls.ContextMenu> rappresenta l'elemento che espone le funzionalità utilizzando un oggetto <xref:System.Windows.Controls.Menu> specifico del contesto.  In genere, un utente espone <xref:System.Windows.Controls.ContextMenu> nell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] facendo clic con il pulsante destro del mouse.  In questo argomento viene presentato l'elemento <xref:System.Windows.Controls.ContextMenu> e vengono forniti alcuni esempi di utilizzo in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] e nel codice.  
  
   
  
<a name="contextmenu_control"></a>   
## Controllo ContextMenu  
 <xref:System.Windows.Controls.ContextMenu> viene associato a un controllo specifico.  L'elemento <xref:System.Windows.Controls.ContextMenu> consente di visualizzare un elenco di elementi che specificano opzioni o comandi associati a un particolare controllo, quale ad esempio <xref:System.Windows.Controls.Button>.  Per visualizzare il menu, occorre fare clic con il pulsante destro del mouse sul controllo.  In genere, quando si fa clic su un oggetto <xref:System.Windows.Controls.MenuItem> viene aperto un sottomenu oppure si esegue un comando in un'applicazione.  
  
<a name="creating_contextmenus"></a>   
## Creazione di ContextMenu  
 Nei seguenti esempi viene illustrato come creare un oggetto <xref:System.Windows.Controls.ContextMenu> con vari sottomenu.  I controlli <xref:System.Windows.Controls.ContextMenu> sono associati a pulsanti.  
  
 [!code-xml[ContextMenu#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml#1)]  
  
 [!code-csharp[ContextMenu#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml.cs#2)]
 [!code-vb[ContextMenu#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ContextMenu/VisualBasic/Pane1.xaml.vb#2)]  
  
<a name="applying_styles_to_contextmenu"></a>   
## Applicazione di stili a ContextMenu  
 Utilizzando un oggetto <xref:System.Windows.Style> di un controllo, è possibile modificare in modo significativo l'aspetto e il comportamento di <xref:System.Windows.Controls.ContextMenu> senza alcuna necessità di scrivere un controllo personalizzato.  Oltre a impostare proprietà visive, è anche possibile applicare stili a parti di un controllo.  Ad esempio, è possibile modificare il comportamento di parti del controllo utilizzando le proprietà oppure aggiungere altre parti o modificare il layout di <xref:System.Windows.Controls.ContextMenu>.  Nei seguenti esempi vengono illustrati diversi metodi per aggiungere gli stili ai controlli <xref:System.Windows.Controls.ContextMenu>.  
  
 Nel primo esempio viene definito uno stile denominato `SimpleSysResources`, in cui viene illustrato come utilizzare le impostazioni di sistema correnti nello stile.  Nell'esempio vengono assegnati <xref:System.Windows.SystemColors.MenuHighlightBrushKey%2A> come colore di <xref:System.Windows.Controls.Control.Background%2A> e <xref:System.Windows.SystemColors.MenuTextBrushKey%2A> come colore di <xref:System.Windows.Controls.Control.Foreground%2A> per <xref:System.Windows.Controls.ContextMenu>.  
  
```  
<Style x:Key="SimpleSysResources" TargetType="{x:Type MenuItem}">  
  <Setter Property = "Background" Value=   
    "{DynamicResource {x:Static SystemColors.MenuHighlightBrushKey}}"/>  
  <Setter Property = "Foreground" Value=   
    "{DynamicResource {x:Static SystemColors.MenuTextBrushKey}}"/>  
</Style>  
```  
  
 Nell'esempio successivo viene utilizzato l'elemento <xref:System.Windows.Trigger> per modificare l'aspetto di <xref:System.Windows.Controls.Menu> in risposta a eventi generati in <xref:System.Windows.Controls.ContextMenu>.  Quando un utente sposta il mouse sul menu, l'aspetto degli elementi di <xref:System.Windows.Controls.ContextMenu> viene modificato.  
  
```  
<Style x:Key="Triggers" TargetType="{x:Type MenuItem}">  
  <Style.Triggers>  
    <Trigger Property="MenuItem.IsMouseOver" Value="true">  
      <Setter Property = "FontSize" Value="16"/>  
      <Setter Property = "FontStyle" Value="Italic"/>  
      <Setter Property = "Foreground" Value="Red"/>  
    </Trigger>  
  </Style.Triggers>  
</Style>  
```  
  
## Vedere anche  
 <xref:System.Windows.Controls.ContextMenu>   
 <xref:System.Windows.Style>   
 <xref:System.Windows.Controls.Menu>   
 <xref:System.Windows.Controls.MenuItem>   
 [ContextMenu](../../../../docs/framework/wpf/controls/contextmenu.md)   
 [Stili e modelli di ContextMenu](../../../../docs/framework/wpf/controls/contextmenu-styles-and-templates.md)   
 [Esempio di raccolta di controlli WPF](http://go.microsoft.com/fwlink/?LinkID=160053)