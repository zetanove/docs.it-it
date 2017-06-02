---
title: "Procedura: trovare un oggetto TreeViewItem in un oggetto TreeView | Microsoft Docs"
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
  - "TreeView (controllo) [WPF], ricerca di un controllo TreeViewItem"
  - "TreeViewItem [WPF], ricerca"
ms.assetid: 72ecd40c-3939-4e01-b617-5e9daa6074d9
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: trovare un oggetto TreeViewItem in un oggetto TreeView
Il controllo <xref:System.Windows.Controls.TreeView> fornisce un modo pratico per visualizzare i dati gerarchici.  Se <xref:System.Windows.Controls.TreeView> è associato a un'origine dati, la proprietà <xref:System.Windows.Controls.TreeView.SelectedItem%2A> fornisce un modo pratico per recuperare rapidamente l'oggetto dati selezionato.  In genere è preferibile utilizzare l'oggetto dati sottostante, ma talvolta può essere necessario modificare a livello di codice i dati contenenti <xref:System.Windows.Controls.TreeViewItem>.  Ad esempio, è possibile che sia necessario espandere a livello di codice <xref:System.Windows.Controls.TreeViewItem> o selezionare un elemento diverso in <xref:System.Windows.Controls.TreeView>.  
  
 Per trovare un oggetto <xref:System.Windows.Controls.TreeViewItem> che contenga un oggetto dati specifico, è necessario scorrere ogni livello di <xref:System.Windows.Controls.TreeView>.  Gli elementi in <xref:System.Windows.Controls.TreeView> possono anche essere virtualizzati per migliorare le prestazioni.  Nel caso in cui gli elementi possano essere virtualizzati, è inoltre necessario eseguire <xref:System.Windows.Controls.TreeViewItem> per verificare se contiene l'oggetto dati.  
  
## Esempio  
  
## Descrizione  
 Nell'esempio seguente viene cercato un oggetto specifico in <xref:System.Windows.Controls.TreeView> e viene restituito l'oggetto contenente <xref:System.Windows.Controls.TreeViewItem>.  Nell'esempio si assicura che venga creata un'istanza di ogni oggetto <xref:System.Windows.Controls.TreeViewItem> in modo da consentire la ricerca dei relativi elementi figlio.  Questo esempio funziona anche se <xref:System.Windows.Controls.TreeView> non contiene elementi virtualizzati.  
  
> [!NOTE]
>  L'esempio seguente è applicabile a qualsiasi oggetto <xref:System.Windows.Controls.TreeView>, indipendentemente dal modello di dati sottostante e consente di cercare in tutti gli oggetti <xref:System.Windows.Controls.TreeViewItem> finché l'oggetto non viene trovato.  Un'altra tecnica che offre prestazioni migliori consiste nel cercare l'oggetto specificato nel modello dati, tenere traccia della relativa posizione all'interno della gerarchia dei dati e quindi trovare l'oggetto <xref:System.Windows.Controls.TreeViewItem> corrispondente in <xref:System.Windows.Controls.TreeView>.  Tuttavia, la tecnica che offre prestazioni migliori richiede la conoscenza del modello di dati e non può essere generalizzata per qualsiasi oggetto <xref:System.Windows.Controls.TreeView>.  
  
## Codice  
 [!code-csharp[TreeViewFindTVI#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml.cs#1)]
 [!code-vb[TreeViewFindTVI#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TreeViewFindTVI/VisualBasic/MainWindow.xaml.vb#1)]  
  
 Il codice precedente si basa su un oggetto <xref:System.Windows.Controls.VirtualizingStackPanel> personalizzato che espone un metodo denominato `BringIntoView`.  Il codice seguente definisce l'oggetto <xref:System.Windows.Controls.VirtualizingStackPanel> personalizzato.  
  
 [!code-csharp[TreeViewFindTVI#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml.cs#2)]
 [!code-vb[TreeViewFindTVI#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TreeViewFindTVI/VisualBasic/MainWindow.xaml.vb#2)]  
  
 Nel codice XAML riportato di seguito viene illustrato come creare un oggetto<xref:System.Windows.Controls.TreeView> che utilizza l'oggetto <xref:System.Windows.Controls.VirtualizingStackPanel> personalizzato.  
  
 [!code-xml[TreeViewFindTVI#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml#3)]  
  
## Vedere anche  
 [Miglioramento delle prestazioni di un controllo TreeView](../../../../docs/framework/wpf/controls/how-to-improve-the-performance-of-a-treeview.md)