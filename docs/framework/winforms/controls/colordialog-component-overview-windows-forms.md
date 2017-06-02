---
title: "Cenni preliminari sul componente ColorDialog (Windows Form) | Microsoft Docs"
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
  - "ColorDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "finestra di dialogo dei colori, informazioni sulla finestra di dialogo dei colori"
  - "ColorDialog (componente), informazioni"
ms.assetid: 6dbdd8f0-f697-4728-bb09-7ea156f6d800
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sul componente ColorDialog (Windows Form)
Il componente <xref:System.Windows.Forms.ColorDialog> Windows Form è una finestra di dialogo preconfigurata che consente all'utente di selezionare un colore da una tavolozza e aggiungervi colori personalizzati.  Si tratta della stessa finestra di dialogo visualizzata in altre applicazioni Windows per la selezione di colori  e costituisce una semplice soluzione, utilizzabile nell'applicazione basata su Windows creata, per evitare di configurare una propria finestra di dialogo.  
  
 Il colore selezionato nella finestra di dialogo viene restituito nella proprietà <xref:System.Windows.Forms.ColorDialog.Color%2A>.  Se la proprietà <xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A> è impostata su `false`, il pulsante "Definisci colori personalizzati" è disabilitato e l'utente può utilizzare solo i colori predefiniti della tavolozza.  Se la proprietà <xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A> è impostata su `true`, l'utente non può selezionare colori retinati.  Per visualizzare la finestra di dialogo, è necessario chiamare il relativo metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ColorDialog>   
 [Componente ColorDialog](../../../../docs/framework/winforms/controls/colordialog-component-windows-forms.md)   
 [Controlli e componenti della finestra di dialogo](../../../../docs/framework/winforms/controls/dialog-box-controls-and-components-windows-forms.md)   
 [Procedura: modificare l'aspetto del componente ColorDialog di Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-colordialog-component.md)