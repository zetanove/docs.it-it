---
title: "Cenni preliminari sul componente ToolTip (Windows Form) | Microsoft Docs"
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
  - "ToolTip"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ToolTip (componente) [Windows Form], informazioni sul componente ToolTip"
  - "descrizioni comandi [Windows Form], informazioni sulle descrizioni comandi"
ms.assetid: 3fbc6f08-c882-4acd-a960-a08efe3c7e6e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Cenni preliminari sul componente ToolTip (Windows Form)
Il componente <xref:System.Windows.Forms.ToolTip> di Windows Form visualizza testo quando l'utente posiziona il puntatore del mouse su uno dei controlli.  È possibile associare un componente ToolTip a qualsiasi controllo.  Per risparmiare spazio in un form, ad esempio, è possibile visualizzare una piccola icona su un pulsante e utilizzare un componente ToolTip per illustrare la funzione del pulsante.  
  
## Utilizzo del componente ToolTip  
 Un componente <xref:System.Windows.Forms.ToolTip> fornisce una proprietà `ToolTip` a più controlli in un Windows Form o in un altro contenitore.  Ad esempio, se si inserisce un componente <xref:System.Windows.Forms.ToolTip> in un form, è possibile visualizzare il testo "Digitare il nome" per un controllo <xref:System.Windows.Forms.TextBox> e "Fare clic per salvare le modifiche" per un controllo <xref:System.Windows.Forms.Button>.  
  
 I metodi principali del componente <xref:System.Windows.Forms.ToolTip> sono <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> e <xref:System.Windows.Forms.ToolTip.GetToolTip%2A>.  È possibile utilizzare il metodo <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> per impostare i componenti ToolTip visualizzati per i controlli.  Per ulteriori informazioni, vedere [Procedura: impostare le descrizioni comandi per i controlli in un Windows Form in fase di progettazione](../../../../docs/framework/winforms/controls/how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md).  Le proprietà principali sono <xref:System.Windows.Forms.ToolTip.Active%2A>, che deve essere impostata su `true` affinché il componente ToolTip venga visualizzato, e <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>, che stabilisce per quanto tempo la stringa del componente ToolTip rimane visualizzata, per quanto tempo il puntatore deve rimanere sul controllo affinché la descrizione del comando venga visualizzata e quanto tempo deve trascorre prima della visualizzazione delle descrizioni successive.  Per ulteriori informazioni, vedere [Procedura: modificare il ritardo del componente ToolTip di Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-delay-of-the-windows-forms-tooltip-component.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolTip>   
 [Procedura: impostare le descrizioni comandi per i controlli in un Windows Form in fase di progettazione](../../../../docs/framework/winforms/controls/how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)   
 [Procedura: modificare il ritardo del componente ToolTip di Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)