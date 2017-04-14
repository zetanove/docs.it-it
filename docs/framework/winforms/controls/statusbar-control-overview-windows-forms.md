---
title: "Cenni preliminari sul controllo StatusBar (Windows Form) | Microsoft Docs"
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
  - "StatusBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "barre di stato"
  - "StatusBar (controllo) [Windows Form], informazioni sul controllo StatusBar"
ms.assetid: b7b9852c-633d-4416-bb2e-94852b989c6c
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sul controllo StatusBar (Windows Form)
> [!IMPORTANT]
>  Benché i controlli <xref:System.Windows.Forms.StatusStrip> e <xref:System.Windows.Forms.ToolStripStatusLabel> sostituiscano i controlli <xref:System.Windows.Forms.StatusBar> e <xref:System.Windows.Forms.StatusBarPanel> delle versioni precedenti aggiungendo funzionalità, i controlli <xref:System.Windows.Forms.StatusBar> e <xref:System.Windows.Forms.StatusBarPanel> vengono mantenuti per compatibilità con le versioni precedenti e per utilizzo futuro se lo si desidera.  
  
 Il controllo [Controllo StatusBar](../../../../docs/framework/winforms/controls/statusbar-control-windows-forms.md) di Windows Form viene utilizzato sui form come un'area, in genere visualizzata nella parte inferiore di una finestra, nella quale un'applicazione può visualizzare i vari tipi di informazioni sullo stato.  I controlli <xref:System.Windows.Forms.StatusBar> possono includere pannelli in cui sono visualizzati testo o icone per indicare lo stato oppure una serie di icone animate per indicare l'esecuzione di un processo, ad esempio [!INCLUDE[ofprword](../../../../includes/ofprword-md.md)] per indicare il salvataggio di un documento.  
  
## Utilizzo del controllo StatusBar  
 In Internet Explorer la barra di stato viene utilizzata per indicare l'URL di una pagina quando il mouse si sposta sul collegamento ipertestuale. In [!INCLUDE[ofprword](../../../../includes/ofprword-md.md)] sono visualizzate informazioni sulla posizione della pagina e della sezione, nonché le modalità di modifica, come la sovrascrittura e l'utilizzo dei segni di revisione. In [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] la barra di stato viene utilizzata per fornire informazioni sensibili al contesto, quali informazioni su come utilizzare le finestre ancorabili quando sono ancorate o mobili.  
  
 È possibile visualizzare un singolo messaggio sulla barra di stato impostando la proprietà <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> su `false` \(impostazione predefinita\) e la proprietà <xref:System.Windows.Forms.StatusBar.Text%2A> della barra di stato sul testo che si desidera visualizzare nella barra di stato.  È possibile dividere la barra di stato in pannelli per visualizzare più tipi di informazioni, impostando la proprietà <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> su `true` e utilizzando il metodo <xref:System.Windows.Forms.StatusBar.StatusBarPanelCollection.Add%2A> della classe <xref:System.Windows.Forms.StatusBar.StatusBarPanelCollection>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.StatusBar>   
 <xref:System.Windows.Forms.ToolStripStatusLabel>   
 [Procedura: individuare il pannello selezionato nel controllo StatusBar Windows Form](../../../../docs/framework/winforms/controls/determine-which-panel-wf-statusbar-control-was-clicked.md)