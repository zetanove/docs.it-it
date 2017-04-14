---
title: "Cenni preliminari sul controllo CheckBox (Windows Form) | Microsoft Docs"
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
  - "CheckBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli con associazione, caselle di controllo"
  - "caselle di controllo, informazioni sulle caselle di controllo"
  - "CheckBox (controllo) [Windows Form], informazioni sul controllo CheckBox"
  - "associazione dati, checkbox (controlli)"
  - "controlli con associazione a dati, caselle di controllo"
ms.assetid: 085a4e0b-9046-473f-b141-d0edddfb2ebb
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Cenni preliminari sul controllo CheckBox (Windows Form)
Il controllo <xref:System.Windows.Forms.CheckBox> Windows Form indica se una determinata condizione è attiva o non attiva.  Viene in genere utilizzato per presentare all'utente la possibilità di scelta tra Sì\/No oppure fra True\/False.  I controlli casella di controllo possono essere utilizzati a gruppi, per visualizzare e consentire all'utente la selezione di una o più opzioni.  
  
 Il controllo casella di controllo è simile al controllo pulsante di opzione, poiché entrambi vengono utilizzati per indicare una selezione effettuata dall'utente.  È tuttavia possibile selezionare un solo pulsante di opzione alla volta per ogni gruppo.  Al contrario, il controllo casella di controllo consente di selezionare più caselle di controllo.  
  
 È possibile associare una casella di controllo a elementi di un database utilizzando l'associazione dati.  È inoltre possibile raggruppare più caselle di controllo utilizzando il controllo <xref:System.Windows.Forms.GroupBox>.  Ciò risulta particolarmente utile ai fini dell'aspetto visivo e della progettazione dell'interfaccia utente, dato che i controlli raggruppati possono essere spostati in blocco all'interno della finestra di progettazione dei form.  Per ulteriori informazioni, vedere [Associazione ai dati di Windows Form](../../../../docs/framework/winforms/windows-forms-data-binding.md) e [Controllo GroupBox](../../../../docs/framework/winforms/controls/groupbox-control-windows-forms.md).  
  
 Il controllo <xref:System.Windows.Forms.CheckBox> dispone di due proprietà importanti: <xref:System.Windows.Forms.CheckBox.Checked%2A> e <xref:System.Windows.Forms.CheckBox.CheckState%2A>.  La proprietà <xref:System.Windows.Forms.CheckBox.Checked%2A> restituisce `true` o `false`.  La proprietà <xref:System.Windows.Forms.CheckBox.CheckState%2A> restituisce <xref:System.Windows.Forms.CheckState> o <xref:System.Windows.Forms.CheckState> oppure, se la proprietà <xref:System.Windows.Forms.CheckBox.ThreeState%2A> è impostata su `true`, <xref:System.Windows.Forms.CheckBox.CheckState%2A> può restituire anche <xref:System.Windows.Forms.CheckState>.  Nello stato indeterminato la casella viene visualizzata come inattiva per indicare che l'opzione non è disponibile.  
  
## Vedere anche  
 <xref:System.Windows.Forms.CheckBox>   
 [Procedura: impostare opzioni con i controlli CheckBox di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-options-with-windows-forms-checkbox-controls.md)   
 [Procedura: rispondere alla selezione di controlli CheckBox Windows Form](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-checkbox-clicks.md)   
 [Controllo CheckBox](../../../../docs/framework/winforms/controls/checkbox-control-windows-forms.md)