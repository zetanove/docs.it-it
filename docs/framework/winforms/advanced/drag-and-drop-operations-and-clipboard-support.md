---
title: "Drag-and-Drop Operations and Clipboard Support | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "drag and drop"
  - "drag and drop, Windows Forms"
  - "Clipboard, Windows Forms"
ms.assetid: 7cce79b6-5835-46fd-b690-73f12ad368b2
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Drag-and-Drop Operations and Clipboard Support
È possibile abilitare le operazioni di trascinamento all'interno di applicazioni per Windows mediante la gestione di una serie di eventi, in particolare gli eventi <xref:System.Windows.Forms.Control.DragEnter>, <xref:System.Windows.Forms.Control.DragLeave> e <xref:System.Windows.Forms.Control.DragDrop>.  
  
 È anche possibile implementare il supporto per operazioni di taglia\/copia\/incolla e il trasferimento di dati dell'utente negli Appunti all'interno delle applicazioni basate su Windows usando semplici chiamate al metodo.  
  
## In questa sezione  
 [Walkthrough: Performing a Drag\-and\-Drop Operation in Windows Forms](../../../../docs/framework/winforms/advanced/walkthrough-performing-a-drag-and-drop-operation-in-windows-forms.md)  
 Illustra come avviare un'operazione di trascinamento e rilascio.  
  
 [How to: Perform Drag\-and\-Drop Operations Between Applications](../../../../docs/framework/winforms/advanced/how-to-perform-drag-and-drop-operations-between-applications.md)  
 Illustra come eseguire le operazioni di trascinamento e rilascio tra le applicazioni.  
  
 [How to: Add Data to the Clipboard](../../../../docs/framework/winforms/advanced/how-to-add-data-to-the-clipboard.md)  
 Descrive un modo per inserire informazioni negli Appunti a livello di codice.  
  
 [How to: Retrieve Data from the Clipboard](../../../../docs/framework/winforms/advanced/how-to-retrieve-data-from-the-clipboard.md)  
 Descrive come accedere ai dati archiviati negli Appunti.  
  
## Sezioni correlate  
 [Drag\-and\-Drop Functionality in Windows Forms](../../../../docs/framework/winforms/drag-and-drop-functionality-in-windows-forms.md)  
 Descrive i metodi, gli eventi e le classi usate per implementare il comportamento di trascinamento e rilascio.  
  
 <xref:System.Windows.Forms.Control.QueryContinueDrag>  
 Descrive gli aspetti complessi relativi all'evento che richiede l'autorizzazione per proseguire con l'operazione di trascinamento.  
  
 <xref:System.Windows.Forms.Control.DoDragDrop%2A>  
 Descrive gli aspetti complessi relativi al metodo fondamentale per l'inizio dell'operazione di trascinamento.  
  
 <xref:System.Windows.Forms.Clipboard>  
 Vedere anche [Procedura: Inviare dati al figlio MDI attivo](http://msdn.microsoft.com/library/y0hkh2c8\(v=vs.110\)).