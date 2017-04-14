---
title: "Cenni preliminari sul controllo Panel (Windows Form) | Microsoft Docs"
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
  - "Panel"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "raggruppamento di controlli, Panel (controllo)"
  - "Panel (controllo) [Windows Form], informazioni"
ms.assetid: b6b83636-2c39-4dad-89d6-f0fa41049a74
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Cenni preliminari sul controllo Panel (Windows Form)
I controlli <xref:System.Windows.Forms.Panel> Windows Form vengono utilizzati per organizzare altri controlli in gruppi identificabili.  I pannelli vengono in genere utilizzati per suddividere un form in base alla funzione.  Si supponga ad esempio di disporre di un form per gli ordini in cui sono specificate le opzioni di spedizione, quale il corriere notturno da utilizzare.  Il raggruppamento in una pannello di tutte le opzioni fornisce all'utente una visione d'insieme logica.  I controlli possono essere inoltre spostati agevolmente in fase di progettazione, poiché spostando il controllo <xref:System.Windows.Forms.Panel> si spostano anche tutti i controlli che si trovano al suo interno.  È possibile accedere ai controlli raggruppati in un pannello tramite la relativa proprietà <xref:System.Windows.Forms.Control.Controls%2A>,  la quale restituisce una raccolta di istanze <xref:System.Windows.Forms.Control>. Ciò richiede generalmente il cast di un controllo recuperato in questo modo al relativo tipo specifico.  
  
## Panel e GroupBox  
 Il controllo <xref:System.Windows.Forms.Panel> è simile al controllo <xref:System.Windows.Forms.GroupBox>, con la differenza che il controllo <xref:System.Windows.Forms.Panel> contiene barre di scorrimento mentre il controllo <xref:System.Windows.Forms.GroupBox> visualizza una didascalia.  
  
## Proprietà principali  
 Per visualizzare le barre di scorrimento, impostare la proprietà <xref:System.Windows.Forms.ScrollableControl.AutoScroll%2A> su `true`.  È inoltre possibile personalizzare l'aspetto del pannello impostando le proprietà <xref:System.Windows.Forms.Control.BackColor%2A>, <xref:System.Windows.Forms.Control.BackgroundImage%2A> e <xref:System.Windows.Forms.Panel.BorderStyle%2A>.  Per ulteriori informazioni sulle proprietà <xref:System.Windows.Forms.Control.BackColor%2A> e <xref:System.Windows.Forms.Control.BackgroundImage%2A>, vedere [Procedura: impostare lo sfondo di un controllo Panel](../../../../docs/framework/winforms/controls/how-to-set-the-background-of-a-windows-forms-panel.md).  La proprietà <xref:System.Windows.Forms.Panel.BorderStyle%2A> determina il tipo di bordo del pannello, che può essere non visibile \(<xref:System.Windows.Forms.BorderStyle>\), costituito da una linea semplice \(<xref:System.Windows.Forms.BorderStyle>\) o da una linea ombreggiata \(<xref:System.Windows.Forms.BorderStyle>\).  
  
## Vedere anche  
 <xref:System.Windows.Forms.Panel>   
 [Controllo GroupBox](../../../../docs/framework/winforms/controls/groupbox-control-windows-forms.md)   
 [Procedura: raggruppare i controlli con il controllo Panel di Windows Form nella finestra di progettazione](../../../../docs/framework/winforms/controls/group-controls-with-wf-panel-control-using-the-designer.md)   
 [Procedura: impostare lo sfondo di un controllo Panel Windows Form mediante la finestra di progettazione](../../../../docs/framework/winforms/controls/how-to-set-the-background-of-a-windows-forms-panel-using-the-designer.md)