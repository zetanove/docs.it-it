---
title: "Cenni preliminari sul componente PrintDialog (Windows Form) | Microsoft Docs"
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
  - "PrintDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Stampa (finestra di dialogo), visualizzazione"
  - "PrintDialog (componente) [Windows Form], informazioni sul componente PrintDialog"
ms.assetid: 8327b8ac-1017-4b5e-a88b-fea9dd56999c
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sul componente PrintDialog (Windows Form)
Il componente [PrintDialog](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md) di Windows Form è una finestra preconfigurata utilizzata per selezionare una stampante, scegliere le pagine da stampare e indicare altre impostazioni relative alla stampa nelle applicazioni basate su Windows.  Utilizzare questo componente come semplice soluzione per la selezione della stampante e delle impostazioni relative alla stampa anziché configurare una propria finestra di dialogo.  Consente agli utenti di stampare diverse parti dei documenti \(l'intero documento, un intervallo di pagine selezionato o una selezione\).  Basandosi sulle finestre di dialogo standard di Windows è quindi possibile creare applicazioni le cui funzionalità di base sono immediatamente familiari agli utenti.  Il componente <xref:System.Windows.Forms.PrintDialog> eredita dalla classe <xref:System.Windows.Forms.CommonDialog>.  
  
## Utilizzo del componente  
 Utilizzare il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> per visualizzare la finestra di dialogo in fase di esecuzione.  Questo componente dispone di proprietà relative a un singolo processo di stampa \(classe <xref:System.Drawing.Printing.PrintDocument>\) o alle impostazioni di una singola stampante \(classe <xref:System.Drawing.Printing.PrinterSettings>\),  ciascuna delle quali può essere condivisa da più stampanti.  
  
 Quando viene aggiunto a un form, il componente <xref:System.Windows.Forms.PrintDialog> viene visualizzato nella barra delle applicazioni nella parte inferiore di Progettazione Windows Form.  
  
## Vedere anche  
 <xref:System.Windows.Forms.PrintDialog>   
 [Componente PrintDialog](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md)