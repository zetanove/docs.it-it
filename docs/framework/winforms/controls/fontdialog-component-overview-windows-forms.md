---
title: "Cenni preliminari sul componente FontDialog (Windows Form) | Microsoft Docs"
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
  - "FontDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Tipo di carattere (finestra di dialogo)"
  - "Tipo di carattere (finestra di dialogo), Windows Form"
  - "FontDialog (componente) [Windows Form], informazioni sul componente FontDialog"
ms.assetid: daf46e57-1b4b-4b7a-bad0-b50ca7ba75dc
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni preliminari sul componente FontDialog (Windows Form)
Il componente <xref:System.Windows.Forms.FontDialog> di Windows Form è una finestra di dialogo preconfigurata, che corrisponde alla finestra di dialogo **Tipo di carattere** Windows standard utilizzata per esporre i tipi di carattere attualmente installati sul sistema,  e costituisce una semplice soluzione, utilizzabile nell'applicazione Windows creata, per evitare di configurare una propria finestra di dialogo.  
  
 Per impostazione predefinita la finestra di dialogo contiene le caselle di riepilogo Tipo di carattere, Stile e Dimensione; le caselle di controllo per gli effetti quali Barrato e Sottolineato; un elenco a discesa per Script; e un'anteprima del tipo di carattere.  Script fa riferimento ai diversi script di carattere disponibili per un dato tipo di carattere, ad esempio, ebraico o giapponese. Per visualizzare la finestra di dialogo Tipo di carattere, richiamare il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>.  
  
## Proprietà principali  
 Il componente comprende numerose proprietà per la configurazione dell'aspetto.  Le proprietà che consentono di impostare le selezioni della finestra di dialogo sono <xref:System.Windows.Forms.FontDialog.Font%2A> e <xref:System.Windows.Forms.FontDialog.Color%2A>.  La proprietà <xref:System.Windows.Forms.FontDialog.Font%2A> consente di impostare il tipo di carattere, lo stile, la dimensione, lo script e gli effetti, ad esempio  `Arial, 10pt, style=Italic, Strikeout`.  
  
## Vedere anche  
 <xref:System.Windows.Forms.FontDialog>   
 [Componente FontDialog](../../../../docs/framework/winforms/controls/fontdialog-component-windows-forms.md)