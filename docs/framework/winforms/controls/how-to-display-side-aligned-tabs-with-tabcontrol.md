---
title: "Procedura: visualizzare schede allineate lateralmente con TabControl | Microsoft Docs"
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
  - "schede, visualizzazione di schede allineate lateralmente"
  - "TabControl (controllo) [Windows Form], visualizzazione di schede allineate lateralmente"
  - "schede, visualizzazione di schede allineate lateralmente"
ms.assetid: 110d5abd-3ae3-4ded-95bf-778aaac798a0
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: visualizzare schede allineate lateralmente con TabControl
La proprietà <xref:System.Windows.Forms.TabControl.Alignment%2A> di <xref:System.Windows.Forms.TabControl> supporta la visualizzazione di schede in verticale \(lungo il bordo sinistro o destro del controllo\) anziché in orizzontale \(lungo la parte superiore o inferiore del controllo\).  Per impostazione predefinita, questa visualizzazione verticale comporta un'esperienza utente non soddisfacente, perché la proprietà <xref:System.Windows.Forms.TabPage.Text%2A> dell'oggetto <xref:System.Windows.Forms.TabPage> non viene visualizzata nella scheda quando sono abilitati gli stili visivi.  Inoltre, non esiste un modo diretto per controllare la direzione del testo all'interno della scheda.  È possibile usare Owner Draw in <xref:System.Windows.Forms.TabControl> per migliorare questa esperienza.  
  
 La procedura seguente mostra come eseguire il rendering di schede allineate a destra, con il testo della scheda visualizzato da sinistra a destra, usando la funzionalità "Owner Draw".  
  
### Per visualizzare le schede allineate a destra  
  
1.  Aggiungere un oggetto <xref:System.Windows.Forms.TabControl> al form.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.TabControl.Alignment%2A> su <xref:System.Windows.Forms.TabAlignment>.  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.TabControl.SizeMode%2A> su <xref:System.Windows.Forms.TabSizeMode> in modo che tutte le schede siano della stessa larghezza.  
  
4.  Impostare la proprietà <xref:System.Windows.Forms.TabControl.ItemSize%2A> sulle dimensioni fisse preferite per le schede.  Tenere presente che la proprietà <xref:System.Windows.Forms.TabControl.ItemSize%2A> si comporta come se le schede si trovassero nella parte superiore, sebbene siano allineate a destra.  Di conseguenza, per aumentare la larghezza delle schede, è necessario modificare la proprietà <xref:System.Drawing.Size.Height%2A> mentre, per aumentarne l'altezza, è necessario modificare la proprietà <xref:System.Drawing.Size.Width%2A>.  
  
     Per ottenere risultati migliori con l'esempio di codice riportato di seguito, impostare <xref:System.Drawing.Size.Width%2A> delle schede su 25 e <xref:System.Drawing.Size.Height%2A> su 100.  
  
5.  Impostare la proprietà <xref:System.Windows.Forms.TabControl.DrawMode%2A> su <xref:System.Windows.Forms.TabDrawMode>.  
  
6.  Definire un gestore per l'evento <xref:System.Windows.Forms.TabControl.DrawItem> di <xref:System.Windows.Forms.TabControl> che esegue il rendering del testo da sinistra a destra.  
  
     [!code-csharp[TabControl.RightAlignedTabs#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/TabControl.RightAlignedTabs/CS/Form1.cs#1)]
     [!code-vb[TabControl.RightAlignedTabs#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/TabControl.RightAlignedTabs/VB/Form1.vb#1)]  
  
## Vedere anche  
 [Controllo TabControl](../../../../docs/framework/winforms/controls/tabcontrol-control-windows-forms.md)