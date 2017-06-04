---
title: "Cenni preliminari sul componente PageSetupDialog (Windows Form) | Microsoft Docs"
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
  - "PageSetupDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Imposta pagina (finestra di dialogo), visualizzazione"
  - "PageSetupDialog (componente)"
ms.assetid: 791caacb-a5ca-4fca-bad9-1a5721ad697c
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni preliminari sul componente PageSetupDialog (Windows Form)
Il componente <xref:System.Windows.Forms.PageSetupDialog> di Windows Form è una finestra di dialogo preconfigurata utilizzata per impostare i dettagli della pagina per la stampa nelle applicazioni basate su Windows  e costituisce una semplice soluzione, utilizzabile nell'applicazione applicazione basata su Windows creata, per consentire agli utenti di impostare le preferenze relative alla pagina anziché configurare una propria finestra di dialogo.  È possibile consentire agli utenti di impostare i bordi e i margini, intestazioni e piè di pagina e l'orientamento verticale o orizzontale.  Basandosi sulle finestre di dialogo standard di Windows è quindi possibile creare applicazioni le cui funzionalità di base sono immediatamente familiari agli utenti.  
  
## Proprietà e metodi principali  
 Utilizzare il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> per visualizzare la finestra di dialogo in fase di esecuzione.  Questo componente dispone di proprietà che è possibile impostare, relative a una singola pagina \(classe <xref:System.Drawing.Printing.PrintDocument>\) o a qualsiasi documento \(classe <xref:System.Drawing.Printing.PageSettings>\).  È inoltre possibile utilizzare il componente <xref:System.Windows.Forms.PageSetupDialog> per determinare impostazioni della stampante specifiche, archiviate nella classe <xref:System.Drawing.Printing.PrinterSettings>.  
  
 Quando viene aggiunto a un form, il componente <xref:System.Windows.Forms.PageSetupDialog> viene visualizzato nella barra nella parte inferiore di Progettazione Windows Form.  
  
## Vedere anche  
 <xref:System.Windows.Forms.PageSetupDialog>   
 [Componente PageSetupDialog](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md)