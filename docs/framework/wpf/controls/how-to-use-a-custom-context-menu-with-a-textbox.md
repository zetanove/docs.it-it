---
title: "Procedura: utilizzare un menu di scelta rapida personalizzato con un oggetto TextBox | Microsoft Docs"
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
  - "menu di scelta rapida, personalizzati"
  - "menu di scelta rapida personalizzati"
  - "menu, personalizzati"
  - "TextBox (controllo), menu di scelta rapida personalizzati"
ms.assetid: 842d3cd5-6fa0-4be4-8d90-6c7466213b1c
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: utilizzare un menu di scelta rapida personalizzato con un oggetto TextBox
In questo esempio viene mostrato come definire e implementare un semplice menu di scelta rapida personalizzato per <xref:System.Windows.Controls.TextBox>.  
  
## Esempio  
 Nell'esempio [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] seguente viene definito un controllo <xref:System.Windows.Controls.TextBox> che include un menu di scelta rapida personalizzato.  
  
 Il menu di scelta rapida viene definito utilizzando un elemento <xref:System.Windows.Controls.ContextMenu>.  Il menu di scelta rapida stesso è costituito da una serie di elementi <xref:System.Windows.Controls.MenuItem> e di elementi <xref:System.Windows.Controls.Separator>.  Ciascun elemento <xref:System.Windows.Controls.MenuItem> definisce un comando del menu di scelta rapida; l'attributo <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> definisce il testo visualizzato per il comando di menu e l'attributo <xref:System.Windows.Controls.MenuItem.Click> specifica un metodo di gestione per ciascuna voce di menu.  L'elemento <xref:System.Windows.Controls.Separator> causa semplicemente il rendering di una linea di separazione tra le voci di menu precedenti e quelle successive.  
  
 [!code-xml[TextBox_ContextMenu#_TextBox_ContextMenuXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_ContextMenu/CSharp/Window1.xaml#_textbox_contextmenuxaml)]  
  
## Esempio  
 Nell'esempio seguente viene mostrato il codice di implementazione per la definizione del menu di scelta rapida precedente, nonché il codice che abilita e disabilita il menu di scelta rapida.  L'evento <xref:System.Windows.Controls.ContextMenu.Opened> viene utilizzato per abilitare o disabilitare dinamicamente alcuni comandi in base allo stato corrente di <xref:System.Windows.Controls.TextBox>.  
  
 Per ripristinare il menu di scelta rapida predefinito, utilizzare il metodo <xref:System.Windows.DependencyObject.ClearValue%2A> per cancellare il valore della proprietà <xref:System.Windows.FrameworkElement.ContextMenu%2A>.  Per disabilitare tutto il menu di scelta rapida, impostare la proprietà <xref:System.Windows.FrameworkElement.ContextMenu%2A> su un riferimento null \(`Nothing` in Visual Basic\).  
  
 [!code-csharp[TextBox_ContextMenu#_TextBox_ContextMenu](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_ContextMenu/CSharp/Window1.xaml.cs#_textbox_contextmenu)]
 [!code-vb[TextBox_ContextMenu#_TextBox_ContextMenu](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_ContextMenu/VisualBasic/Window1.xaml.vb#_textbox_contextmenu)]  
  
## Vedere anche  
 [Utilizzare il controllo ortografico con un menu di scelta rapida](../../../../docs/framework/wpf/controls/how-to-use-spell-checking-with-a-context-menu.md)   
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)