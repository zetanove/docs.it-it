---
title: "Procedura: agganciare e ancorare controlli figlio in un controllo TableLayoutPanel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "net.ComponentModel.StyleCollectionEditor.TLP.AnchorDock"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli figlio, ancoraggio"
  - "controlli [Windows Form], figlio"
  - "layout [Windows Form], controlli figlio"
  - "TableLayoutPanel (controllo) [Windows Form], controlli figlio"
ms.assetid: 0d267c35-25f1-49b8-8976-c64e8f0ddc0b
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: agganciare e ancorare controlli figlio in un controllo TableLayoutPanel
Il controllo <xref:System.Windows.Forms.TableLayoutPanel> supporta le proprietà <xref:System.Windows.Forms.Control.Anchor%2A> e <xref:System.Windows.Forms.Control.Dock%2A> nei controlli figlio.  
  
### Per allineare un controllo figlio in una cella TableLayoutPanel  
  
1.  Creare un controllo <xref:System.Windows.Forms.TableLayoutPanel> nel form.  
  
2.  Impostare il valore delle proprietà del controllo <xref:System.Windows.Forms.TableLayoutPanel>, <xref:System.Windows.Forms.TableLayoutPanel.ColumnCount%2A> e <xref:System.Windows.Forms.TableLayoutPanel.RowCount%2A>, su 1.  
  
3.  Creare un controllo <xref:System.Windows.Forms.Button> nel controllo <xref:System.Windows.Forms.TableLayoutPanel>.  <xref:System.Windows.Forms.Button> occupa l'angolo superiore sinistro della cella.  
  
4.  Modificare il valore della proprietà del controllo <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.Control.Anchor%2A>, su `A sinistra`.  Il controllo <xref:System.Windows.Forms.Button> viene spostato per allinearlo al bordo sinistro della cella.  
  
    > [!NOTE]
    >  Questo comportamento è diverso dal comportamento di altri controlli contenitore.  In altri controlli contenitore, il controllo figlio non viene spostato quando viene impostata la proprietà <xref:System.Windows.Forms.Control.Anchor%2A> e la distanza tra il controllo ancorato e i limiti del contenitore padre viene stabilita al momento dell’impostazione della proprietà <xref:System.Windows.Forms.Control.Anchor%2A>.  
  
5.  Modificare il valore della proprietà del controllo <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.Control.Anchor%2A>, su `In alto, A sinistra`.  Il controllo <xref:System.Windows.Forms.Button> viene spostato in modo che occupi l'angolo superiore sinistro della cella.  
  
6.  Ripetere il passaggio 5 con un valore `In alto, A destra` per spostare il controllo <xref:System.Windows.Forms.Button> nell'angolo superiore destro della cella.  Ripetere l’operazione con i valori `In basso, A sinistra` e `In basso, A destra`.  
  
### Per estendere un controllo figlio in una cella TableLayoutPanel  
  
1.  Modificare il valore della proprietà del controllo <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.Control.Anchor%2A>, su `A sinistra, A destra`.  Il controllo <xref:System.Windows.Forms.Button> viene ridimensionato in modo da estendersi per tutta la cella.  
  
    > [!NOTE]
    >  Questo comportamento è diverso dal comportamento di altri controlli contenitore.  In altri controlli contenitore, il controllo figlio non viene ridimensionato quando la proprietà <xref:System.Windows.Forms.Control.Anchor%2A> è impostata su `A sinistra, A destra` o `In alto, In basso`.  
  
2.  Modificare il valore della proprietà del controllo <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.Control.Anchor%2A>, su `In alto, In basso`.  Il controllo <xref:System.Windows.Forms.Button> viene ridimensionato in modo da estendersi dalla parte superiore a quella inferiore della cella.  
  
3.  Modificare il valore del <xref:System.Windows.Forms.Button> del controllo <xref:System.Windows.Forms.Control.Anchor%2A> proprietà `In alto, In basso, A sinistra, A destra`.  Il controllo <xref:System.Windows.Forms.Button> viene ridimensionato per riempire la cella.  
  
4.  Modificare il valore della proprietà del controllo <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.Control.Anchor%2A>, su `Nessuno`.  Il controllo <xref:System.Windows.Forms.Button> viene ridimensionato e centrato nella cella.  
  
5.  Modificare il valore della proprietà del controllo <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.Control.Dock%2A>, su <xref:System.Windows.Forms.DockStyle>.  Il controllo <xref:System.Windows.Forms.Button> viene spostato per allinearlo al bordo sinistro della cella.  Il controllo <xref:System.Windows.Forms.Button> conserva la larghezza, ma l'altezza viene ridimensionata per riempire la cella in verticale.  
  
    > [!NOTE]
    >  È lo stesso comportamento che si verifica in altri controlli contenitore.  
  
6.  Modificare il valore della proprietà del controllo <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.Control.Dock%2A>, su <xref:System.Windows.Forms.DockStyle>.  Il controllo <xref:System.Windows.Forms.Button> viene ridimensionato per riempire la cella.  
  
## Esempio  
 La figura seguente mostra cinque pulsanti ancorati in cinque celle <xref:System.Windows.Forms.TableLayoutPanel> separate.  
  
 ![Ancoraggio TableLayoutPanel](../../../../docs/framework/winforms/controls/media/vs-tlpanchor.png "VS\_TLPanchor")  
  
 La figura seguente mostra quattro pulsanti ancorati agli angoli di quattro celle <xref:System.Windows.Forms.TableLayoutPanel> separate.  
  
 ![Ancoraggio TableLayoutPanel](../../../../docs/framework/winforms/controls/media/vs-tlpanchor2.png "VS\_TLPanchor2")  
  
 La figura seguente mostra tre pulsanti estesi mediante ancoraggio in tre celle <xref:System.Windows.Forms.TableLayoutPanel> separate.  
  
 ![Ancoraggio TableLayoutPanel](../../../../docs/framework/winforms/controls/media/vs-tlpanchor3.gif "VS\_TLPAnchor3")  
  
 L'esempio di codice seguente mostra tutte le combinazioni dei valori della proprietà <xref:System.Windows.Forms.Control.Anchor%2A> per un controllo <xref:System.Windows.Forms.Button> in un controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
 [!code-csharp[System.Windows.Forms.TableLayoutPanel.AnchorExampleForm#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.TableLayoutPanel.AnchorExampleForm/CS/TlpAnchorExampleForm.cs#1)]
 [!code-vb[System.Windows.Forms.TableLayoutPanel.AnchorExampleForm#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.TableLayoutPanel.AnchorExampleForm/VB/TlpAnchorExampleForm.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Data, System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.Windows.Forms.TableLayoutPanel>   
 [Controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-windows-forms.md)