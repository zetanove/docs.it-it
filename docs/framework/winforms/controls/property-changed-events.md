---
title: "Eventi per propriet&#224; modificate | Microsoft Docs"
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
  - "controlli personalizzati [Windows Form], modifica delle proprietà (mediante il codice)"
  - "proprietà [Windows Form], modifiche"
ms.assetid: 268039ec-5aaa-4d76-b902-acccb036c850
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Eventi per propriet&#224; modificate
Se si desidera che un controllo invii notifiche quando viene modificata la proprietà denominata *NomeProprietà*, definire un evento denominato *NomeProprietà*`Changed` e un metodo denominato `On`*NomeProprietà*`Changed` che generi l'evento.  In base alla convenzione di denominazione adottata in Windows Forms, viene aggiunta la parola *Changed* al nome della proprietà.  Il tipo delegato associato a eventi di proprietà modificata è <xref:System.EventHandler> mentre il tipo di dati dell'evento è <xref:System.EventArgs>.  La classe base <xref:System.Windows.Forms.Control> definisce numerosi eventi di proprietà modificata, quali <xref:System.Windows.Forms.Control.BackColorChanged>, <xref:System.Windows.Forms.Control.BackgroundImageChanged>, <xref:System.Windows.Forms.Control.FontChanged>, <xref:System.Windows.Forms.Control.LocationChanged> e altri.  Per informazioni generali sugli eventi, vedere [Eventi](../../../../docs/standard/events/index.md) e [Eventi nei controlli di Windows Form](../../../../docs/framework/winforms/controls/events-in-windows-forms-controls.md).  
  
 L'utilità degli eventi per proprietà modificate risiede nel fatto che consentono ai consumer di un controllo di associare gestori eventi che rispondano alla modifica rilevata.  Se è necessario che il controllo risponda a un evento di proprietà modificata da esso generato, eseguire l'override del metodo `On`*NomeProprietà*`Changed` corrispondente anziché collegare un delegato all'evento.  In genere i controlli rispondono agli eventi per proprietà modificate aggiornando altre proprietà o ridisegnando interamente o in parte la propria superficie di disegno.  
  
 Nell'esempio riportato di seguito viene illustrato come il controllo personalizzato `FlashTrackBar` risponda ad alcuni degli eventi di proprietà modificata ereditati da <xref:System.Windows.Forms.Control>.  Per l'esempio completo, vedere [Procedura: creare un controllo di Windows Form che visualizzi lo stato di avanzamento](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md).  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#2)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#2)]  
  
## Vedere anche  
 [Eventi](../../../../docs/standard/events/index.md)   
 [Eventi nei controlli di Windows Form](../../../../docs/framework/winforms/controls/events-in-windows-forms-controls.md)   
 [Proprietà dei controlli Windows Form](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)