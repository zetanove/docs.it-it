---
title: "Procedura: raggruppare i controlli tramite il controllo GroupBox di Windows Form | Microsoft Docs"
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
  - "controlli [Windows Form], raggruppamento"
  - "GroupBox (controllo) [Windows Form], raggruppamento di controlli"
  - "controlli Windows Form, raggruppamento"
ms.assetid: 0bda316d-bd2a-43aa-ac73-342453303169
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: raggruppare i controlli tramite il controllo GroupBox di Windows Form
I controlli <xref:System.Windows.Forms.GroupBox> di Windows Form vengono utilizzati per raggruppare altri controlli.  Il raggruppamento dei controlli risulta utile per tre motivi:  
  
-   Per creare un raggruppamento visivo di elementi di form per la realizzazione di un'interfaccia utente chiara e intuitiva.  
  
-   Per creare un raggruppamento a livello di codice, ad esempio di pulsanti di opzione.  
  
-   Per spostare i controlli in blocco in fase di progettazione.  
  
### Per creare un gruppo di controlli  
  
1.  Creare un controllo <xref:System.Windows.Forms.GroupBox> in un form.  
  
2.  Aggiungere alla casella di gruppo altri controlli, creando ciascun controllo all'interno della casella di gruppo.  
  
     Se si desidera inserire in una casella di gruppo controlli esistenti, è possibile selezionarli e tagliarli, selezionare il controllo <xref:System.Windows.Forms.GroupBox>, quindi incollare i controlli nella casella di gruppo.  È anche possibile trascinare i controlli nella casella di gruppo.  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.GroupBox.Text%2A> della casella di gruppo sulla didascalia appropriata.  
  
## Vedere anche  
 <xref:System.Windows.Forms.GroupBox>   
 [Controllo GroupBox](../../../../docs/framework/winforms/controls/groupbox-control-windows-forms.md)