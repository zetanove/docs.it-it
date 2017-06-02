---
title: "Procedura: allineare ed estendere un controllo in un controllo TableLayoutPanel | Microsoft Docs"
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
  - "net.ComponentModel.StyleCollectionEditor.TLP.AlignStretchCtrl"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli [Windows Form], allineamento"
  - "controlli [Windows Form], allungare"
  - "TableLayoutPanel (controllo) [Windows Form], allungamento dei controlli"
ms.assetid: 7dc1a157-6fee-4995-8ebc-b65bdc0909a8
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: allineare ed estendere un controllo in un controllo TableLayoutPanel
È possibile allineare ed estendere i controlli in un controllo <xref:System.Windows.Forms.TableLayoutPanel> mediante le proprietà <xref:System.Windows.Forms.Control.Anchor%2A> e <xref:System.Windows.Forms.Control.Dock%2A>.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per allineare ed estendere un controllo  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TableLayoutPanel> dalla **Casella degli strumenti** al form.  
  
2.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nella cella superiore sinistra del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  Il controllo <xref:System.Windows.Forms.Button> verrà centrato all'interno della cella.  
  
3.  Impostare il valore della proprietà <xref:System.Windows.Forms.Control.Anchor%2A> del controllo <xref:System.Windows.Forms.Button> su `Left, Right`.  Il controllo <xref:System.Windows.Forms.Button> si estenderà per adattarsi alla larghezza della cella.  
  
4.  Impostare il valore della proprietà <xref:System.Windows.Forms.Control.Anchor%2A> del controllo <xref:System.Windows.Forms.Button> su `Top, Bottom`.  Il controllo <xref:System.Windows.Forms.Button> si estenderà per adattarsi all'altezza della cella.  
  
5.  Impostare il valore della proprietà <xref:System.Windows.Forms.Control.Dock%2A> del controllo <xref:System.Windows.Forms.Button> su <xref:System.Windows.Forms.DockStyle>.  Il controllo <xref:System.Windows.Forms.Button> si estenderà fino ad occupare l'intera cella.  
  
6.  Impostare il valore della proprietà <xref:System.Windows.Forms.Control.Dock%2A> del controllo <xref:System.Windows.Forms.Button> su <xref:System.Windows.Forms.DockStyle>.  Il controllo <xref:System.Windows.Forms.Button> si sposterà nell'angolo superiore sinistro della cella e verranno ripristinate le dimensioni originali  perché la proprietà <xref:System.Windows.Forms.Control.Anchor%2A> della finestra **Progettazione Windows Form** è impostata su `Top, Left`.  
  
7.  Impostare il valore della proprietà <xref:System.Windows.Forms.Control.Anchor%2A> del controllo <xref:System.Windows.Forms.Button> su `Bottom, Right`.  Il controllo <xref:System.Windows.Forms.Button> si sposterà nell'angolo inferiore destro della cella.  
  
8.  Impostare il valore della proprietà <xref:System.Windows.Forms.Control.Anchor%2A> del controllo <xref:System.Windows.Forms.Button> su <xref:System.Windows.Forms.AnchorStyles>.  Il controllo <xref:System.Windows.Forms.Button> si sposterà al centro della cella.  
  
## Vedere anche  
 [Controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-windows-forms.md)