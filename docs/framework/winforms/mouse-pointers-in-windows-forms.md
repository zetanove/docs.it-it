---
title: "Mouse Pointers in Windows Forms | Microsoft Docs"
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
  - "pointers, setting [Windows Forms]"
  - "mouse pointers"
  - "mouse cursors"
  - "mouse pointers, setting [Windows Forms]"
  - "cursors, setting [Windows Forms]"
  - "mouse, cursors"
ms.assetid: c3400d85-de5b-42e8-abc3-d6088d69ee53
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Mouse Pointers in Windows Forms
Il *puntatore* del mouse, spesso denominato cursore, è una bitmap che specifica un punto in primo piano sullo schermo in cui l'utente può eseguire un'operazione con il mouse.  In questo argomento viene fornita una panoramica del puntatore del mouse in Windows Form e ne vengono descritte alcune modalità di modifica e controllo.  
  
## Accesso al puntatore del mouse  
 Il puntatore del mouse è rappresentato dalla classe <xref:System.Windows.Forms.Cursor> e ogni classe <xref:System.Windows.Forms.Control> dispone di una proprietà <xref:System.Windows.Forms.Control.Cursor%2A?displayProperty=fullName> che specifica il puntatore per il controllo.  La classe <xref:System.Windows.Forms.Cursor> contiene proprietà che descrivono il puntatore, quali <xref:System.Windows.Forms.Cursor.Position%2A> e <xref:System.Windows.Forms.Cursor.HotSpot%2A>, e metodi in grado di modificare l'aspetto del puntatore, quali <xref:System.Windows.Forms.Cursor.Show%2A>, <xref:System.Windows.Forms.Cursor.Hide%2A> e <xref:System.Windows.Forms.Cursor.DrawStretched%2A>.  
  
## Controllo del puntatore del mouse  
 È a volte necessario limitare l'area nella quale utilizzare il puntatore del mouse o modificare la posizione del mouse.  Per ottenere o impostare la posizione corrente del mouse, utilizzare la proprietà <xref:System.Windows.Forms.Cursor.Position%2A> della classe <xref:System.Windows.Forms.Cursor>.  È inoltre possibile limitare l'area di utilizzo del puntatore del mouse impostando la proprietà <xref:System.Windows.Forms.Cursor.Clip%2A>.  Per impostazione predefinita l'area di visualizzazione è l'intero schermo.  
  
## Modifica del puntatore del mouse  
 La modifica del puntatore del mouse è un modo importante per fornire un riscontro all'utente.  È ad esempio possibile modificare il puntatore nei gestori degli eventi <xref:System.Windows.Forms.Control.MouseEnter> e <xref:System.Windows.Forms.Control.MouseLeave> per informare l'utente che sono in corso calcoli e per limitare il suo intervento nel controllo.  Il puntatore assume un aspetto diverso, a volte, a causa di eventi di sistema, ad esempio quando nell'applicazione viene eseguita un'operazione di trascinamento della selezione.  
  
 Il modo principale per modificare il puntatore del mouse consiste nell'impostare la proprietà <xref:System.Windows.Forms.Control.Cursor%2A?displayProperty=fullName> o <xref:System.Windows.Forms.Control.DefaultCursor%2A> di un controllo su una nuova classe <xref:System.Windows.Forms.Cursor>.  Per esempi di modifica del puntatore del mouse, vedere il codice campione nella classe <xref:System.Windows.Forms.Cursor>.  La classe <xref:System.Windows.Forms.Cursors>, inoltre, espone una serie di oggetti della classe <xref:System.Windows.Forms.Cursor> per molti tipi diversi di puntatore, ad esempio quello che rappresenta una mano.  Per visualizzare il puntatore di attesa, rappresentato da una clessidra, ogni volta che il puntatore è su un controllo, utilizzare la proprietà <xref:System.Windows.Forms.Control.UseWaitCursor%2A> della classe <xref:System.Windows.Forms.Control>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Cursor>   
 [Mouse Input in a Windows Forms Application](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)   
 [Drag\-and\-Drop Functionality in Windows Forms](../../../docs/framework/winforms/drag-and-drop-functionality-in-windows-forms.md)