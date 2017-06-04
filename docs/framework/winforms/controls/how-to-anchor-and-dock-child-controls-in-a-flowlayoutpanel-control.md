---
title: "Procedura: ancorare e agganciare controlli figlio in un controllo FlowLayoutPanel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli figlio, ancoraggio"
  - "controlli [Windows Form], figlio"
  - "FlowLayoutPanel (controllo) [Windows Form], controlli figlio"
  - "layout [Windows Form], controlli figlio"
ms.assetid: a2bcdfca-9b63-45e6-9c0e-3411015cba98
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: ancorare e agganciare controlli figlio in un controllo FlowLayoutPanel
Il controllo <xref:System.Windows.Forms.FlowLayoutPanel> supporta le proprietà <xref:System.Windows.Forms.Control.Anchor%2A> e <xref:System.Windows.Forms.Control.Dock%2A> nei controlli figlio.  
  
### Per ancorare e agganciare controlli figlio in un controllo FlowLayoutPanel  
  
1.  Creare un controllo <xref:System.Windows.Forms.FlowLayoutPanel> nel form.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.Control.Width%2A> del controllo <xref:System.Windows.Forms.FlowLayoutPanel> su 300 e la relativa proprietà <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> su <xref:System.Windows.Forms.FlowDirection>.  
  
3.  Creare due controlli <xref:System.Windows.Forms.Button> e inserirli nel controllo <xref:System.Windows.Forms.FlowLayoutPanel>.  
  
4.  Impostare la proprietà <xref:System.Windows.Forms.Control.Width%2A> del primo pulsante su 200.  
  
5.  Impostare la proprietà <xref:System.Windows.Forms.Control.Dock%2A> del secondo pulsante su <xref:System.Windows.Forms.DockStyle>.  
  
    > [!NOTE]
    >  Il secondo pulsante assume la stessa larghezza del primo.  Non si adatta alla larghezza del controllo <xref:System.Windows.Forms.FlowLayoutPanel>.  
  
6.  Impostare la proprietà <xref:System.Windows.Forms.Control.Dock%2A> del secondo pulsante su `None`.  Verrà ripristinata la larghezza originale del pulsante.  
  
7.  Impostare la proprietà <xref:System.Windows.Forms.Control.Anchor%2A> del secondo pulsante su `Left, Right`.  
  
    > [!IMPORTANT]
    >  Il secondo pulsante assume la stessa larghezza del primo.  Non si adatta alla larghezza del controllo <xref:System.Windows.Forms.FlowLayoutPanel>.  Di seguito è riportata la regola generale per l'ancoraggio e l'aggancio nel controllo <xref:System.Windows.Forms.FlowLayoutPanel>: per le direzioni del flusso verticale il controllo <xref:System.Windows.Forms.FlowLayoutPanel> calcola la larghezza di una colonna implicita dal controllo figlio più largo presente nella colonna.  Tutti gli altri controlli in questa colonna con la proprietà <xref:System.Windows.Forms.Control.Anchor%2A> o <xref:System.Windows.Forms.Control.Dock%2A> vengono allineati o estesi in base alla colonna implicita.  Le direzioni del flusso orizzontale si comportano in modo simile.  Il controllo <xref:System.Windows.Forms.FlowLayoutPanel> calcola l'altezza di una riga implicita dal controllo figlio più alto presente nella riga e tutti i controlli figlio agganciati o ancorati in questa riga vengono allineati o ridimensionati di conseguenza.  
  
## Esempio  
 La figura seguente illustra quattro pulsanti ancorati e agganciati rispetto al pulsante blu in un controllo <xref:System.Windows.Forms.FlowLayoutPanel>.  L'elemento <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> è <xref:System.Windows.Forms.FlowDirection>.  
  
 ![Ancoraggio FlowLayoutPanel](../../../../docs/framework/winforms/controls/media/net-flpanchorexp.png "NET\_FLPanchorExp")  
  
 La figura seguente illustra quattro pulsanti ancorati e agganciati rispetto al pulsante blu in un controllo <xref:System.Windows.Forms.FlowLayoutPanel>.  La proprietà <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> è <xref:System.Windows.Forms.FlowDirection>.  
  
 ![Ancoraggio FlowLayoutPanel](../../../../docs/framework/winforms/controls/media/vs-flpanchor2.png "VS\_FLPanchor2")  
  
 L'esempio di codice seguente illustra diversi valori della proprietà <xref:System.Windows.Forms.Control.Anchor%2A> per un controllo <xref:System.Windows.Forms.Button> in un controllo <xref:System.Windows.Forms.FlowLayoutPanel>.  
  
 [!code-csharp[System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm/CS/FlpAnchorExampleForm.cs#1)]
 [!code-vb[System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm/VB/FlpAnchorExampleForm.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Data, System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.Windows.Forms.FlowLayoutPanel>   
 [Cenni preliminari sul controllo FlowLayoutPanel](../../../../docs/framework/winforms/controls/flowlayoutpanel-control-overview.md)