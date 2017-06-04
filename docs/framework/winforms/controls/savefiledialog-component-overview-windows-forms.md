---
title: "Cenni preliminari sul componente SaveFileDialog (Windows Form) | Microsoft Docs"
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
  - "SaveFileDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Salva file (finestra di dialogo), visualizzazione"
  - "SaveFileDialog (componente), informazioni"
ms.assetid: be7a625f-46fd-4d06-9985-b613dcbf9bd2
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Cenni preliminari sul componente SaveFileDialog (Windows Form)
Il componente <xref:System.Windows.Forms.SaveFileDialog> di Windows Form è una finestra di dialogo preconfigurata.  È simile alla finestra di dialogo standard **Salva file** utilizzata da Windows  ed eredita dalla classe <xref:System.Windows.Forms.CommonDialog>.  
  
## Utilizzo del componente SaveFileDialog  
 Utilizzarlo come semplice soluzione per consentire agli utenti di salvare i file anziché configurare una propria finestra di dialogo.  Basandosi sulle finestre di dialogo standard di Windows, è possibile creare applicazioni le cui funzionalità di base sono immediatamente familiari agli utenti.  Quando si utilizza il componente <xref:System.Windows.Forms.SaveFileDialog>, è tuttavia necessario scrivere una propria logica per il salvataggio del file.  
  
 È possibile utilizzare il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> per visualizzare la finestra di dialogo in fase di esecuzione.  È possibile aprire un file in modalità lettura\/scrittura mediante il metodo <xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A>.  
  
 Quando viene aggiunto a un form, il componente <xref:System.Windows.Forms.SaveFileDialog> è visualizzato nella barra delle applicazioni nella parte inferiore di Progettazione Windows Form.  
  
## Vedere anche  
 <xref:System.Windows.Forms.SaveFileDialog>   
 [Componente SaveFileDialog](../../../../docs/framework/winforms/controls/savefiledialog-component-windows-forms.md)