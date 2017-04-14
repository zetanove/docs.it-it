---
title: "Procedura: ancorare i controlli in Windows Form | Microsoft Docs"
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
  - "controlli [Windows Form], ancoraggio"
  - "Dock (proprietà)"
  - "applicazioni di tipo Esplora risorse, creazione"
  - "controlli Windows Form, riempimento area client"
ms.assetid: bc11f2e4-e90a-4830-b0e2-f43b6e2b8bec
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: ancorare i controlli in Windows Form
È possibile ancorare i controlli ai bordi del form o fare in modo che occupino lo spazio del contenitore dei controlli, che può essere sia un form che un controllo contenitore.  Esplora risorse, ad esempio, consente l'ancoraggio del controllo <xref:System.Windows.Forms.TreeView> sul lato sinistro della finestra e del controllo <xref:System.Windows.Forms.ListView> sul lato destro della finestra.  Utilizzare la proprietà <xref:System.Windows.Forms.Control.Dock%2A> per tutti i controlli Windows Form visibili per definire la modalità di ancoraggio.  
  
> [!NOTE]
>  I controlli vengono ancorati in ordine Z inverso.  
  
 La proprietà <xref:System.Windows.Forms.Control.Dock%2A> interagisce con la proprietà <xref:System.Windows.Forms.Control.AutoSize%2A>.  Per ulteriori informazioni, vedere [Cenni preliminari sulla proprietà AutoSize](../../../../docs/framework/winforms/controls/autosize-property-overview.md).  
  
### Per ancorare un controllo  
  
1.  Selezionare il controllo che si desidera ancorare.  
  
2.  Nella finestra Proprietà fare clic sulla freccia a destra della proprietà <xref:System.Windows.Forms.Control.Dock%2A>.  
  
     Verrà visualizzato un editor con una serie di caselle, che rappresentano bordi e centro del form.  
  
3.  Fare clic sul pulsante che rappresenta il bordo del form in cui si desidera ancorare il controllo.  Per inserire il contenuto del form del controllo o del controllo contenitore, fare clic sulla casella centrale.  Fare clic su **\(nessuno\)** per disabilitare l'ancoraggio.  
  
     Il controllo verrà ridimensionato automaticamente per adattarsi ai limiti del bordo ancorato.  
  
    > [!NOTE]
    >  I controlli ereditati, per poter essere agganciati, devono essere `Protected`.  Per modificare il livello di accesso di un controllo, impostare la proprietà **Modifier** del controllo nella finestra Proprietà.  
  
## Vedere anche  
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)   
 [Disposizione di controlli in Windows Form](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [Impostazione delle etichette di singoli controlli Windows Form e creazione dei relativi tasti di scelta rapida](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [Controlli Windows Form per funzione](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)   
 [Procedura: ancorare e agganciare controlli figlio in un controllo FlowLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-flowlayoutpanel-control.md)   
 [Procedura: agganciare e ancorare controlli figlio in un controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)   
 [Cenni preliminari sulla proprietà AutoSize](../../../../docs/framework/winforms/controls/autosize-property-overview.md)   
 [Procedura: agganciare i controlli in Windows Form](../../../../docs/framework/winforms/controls/how-to-anchor-controls-on-windows-forms.md)