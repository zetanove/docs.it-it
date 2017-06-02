---
title: "Gestione dell&#39;input dell&#39;utente | Microsoft Docs"
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
  - "controlli personalizzati [Windows Form], eventi tastiera (mediante il codice)"
  - "controlli personalizzati [Windows Form], eventi mouse (mediante il codice)"
  - "controlli personalizzati [Windows Form], input utente (mediante il codice)"
ms.assetid: d9b12787-86f6-4022-8e0f-e12d312c4af2
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Gestione dell&#39;input dell&#39;utente
In questo argomento vengono descritti gli eventi principali relativi a tastiera e mouse forniti da <xref:System.Windows.Forms.Control?displayProperty=fullName>.  Durante la gestione di un evento, gli autori dei controlli dovrebbero eseguire l'override del metodo `On`*NomeEvento* protetto anziché associare un delegato all'evento.  Per informazioni generali sugli eventi, vedere [Raising Events from a Component](../Topic/Raising%20Events%20from%20a%20Component.md).  
  
> [!NOTE]
>  Se a un evento non sono associati dati, un'istanza della classe di base <xref:System.EventArgs> verrà passata come argomento al metodo `On`*NomeEvento*.  
  
## Eventi della tastiera  
 Gli eventi della tastiera che il controllo è in grado di gestire sono <xref:System.Windows.Forms.Control.KeyDown>, <xref:System.Windows.Forms.Control.KeyPress> e <xref:System.Windows.Forms.Control.KeyUp>.  
  
|Nome evento|Metodo di cui eseguire l'override|Descrizione dell'evento|  
|-----------------|---------------------------------------|-----------------------------|  
|`KeyDown`|`void OnKeyDown(KeyEventArgs)`|Generato solo quando inizialmente è premuto un tasto.|  
|`KeyPress`|`void OnKeyPress`<br /><br /> `(KeyPressEventArgs)`|Generato ogni volta che è premuto un tasto.  Se un tasto viene tenuto premuto, viene generata una serie di eventi <xref:System.Windows.Forms.Control.KeyPress> con una frequenza definita dal sistema operativo.|  
|`KeyUp`|`void OnKeyUp(KeyEventArgs)`|Generato quando è rilasciato un tasto.|  
  
> [!NOTE]
>  La gestione dell'input da tastiera è notevolmente più complessa dell'override degli eventi esposti nella tabella precedente e non rientra nell'ambito di questo argomento.  Per ulteriori informazioni, vedere [User Input in Windows Forms](../../../../docs/framework/winforms/user-input-in-windows-forms.md).  
  
## Eventi del mouse  
 Gli eventi del mouse che il controllo è in grado di gestire sono <xref:System.Windows.Forms.Control.MouseDown>, <xref:System.Windows.Forms.Control.MouseEnter>, <xref:System.Windows.Forms.Control.MouseHover>, <xref:System.Windows.Forms.Control.MouseLeave>, <xref:System.Windows.Forms.Control.MouseMove> e <xref:System.Windows.Forms.Control.MouseUp>.  
  
|Nome evento|Metodo di cui eseguire l'override|Descrizione dell'evento|  
|-----------------|---------------------------------------|-----------------------------|  
|`MouseDown`|`void OnMouseDown(MouseEventArgs)`|Generato quando viene premuto il pulsante del mouse mentre il puntatore si trova sopra il controllo.|  
|`MouseEnter`|`void OnMouseEnter(EventArgs)`|Generato quando il puntatore viene portato all'interno della regione del controllo.|  
|`MouseHover`|`void OnMouseHover(EventArgs)`|Generato quando il puntatore passa sopra il controllo.|  
|`MouseLeave`|`void OnMouseLeave(EventArgs)`|Generato quando il puntatore viene portato all'esterno della regione del controllo.|  
|`MouseMove`|`void OnMouseMove(MouseEventArgs)`|Generato quando il puntatore viene spostato sopra la regione del controllo.|  
|`MouseUp`|`void OnMouseUp(MouseEventArgs)`|Generato quando il pulsante del mouse viene rilasciato mentre il puntatore si trova sul controllo o quando il puntatore viene portato all'esterno della regione del controllo.|  
  
 Nel codice riportato di seguito viene illustrato un esempio di override dell'evento <xref:System.Windows.Forms.Control.MouseDown>.  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#7)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#7)]  
  
 Nel codice riportato di seguito viene illustrato un esempio di override dell'evento <xref:System.Windows.Forms.Control.MouseMove>.  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#8](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#8)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#8](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#8)]  
  
 Nel codice riportato di seguito viene illustrato un esempio di override dell'evento <xref:System.Windows.Forms.Control.MouseUp>.  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#9](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#9)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#9](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#9)]  
  
 Per il codice sorgente completo dell'esempio `FlashTrackBar`, vedere [Procedura: creare un controllo di Windows Form che visualizzi lo stato di avanzamento](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md).  
  
## Vedere anche  
 [Eventi nei controlli di Windows Form](../../../../docs/framework/winforms/controls/events-in-windows-forms-controls.md)   
 [Definizione di un evento](../../../../docs/framework/winforms/controls/defining-an-event-in-windows-forms-controls.md)   
 [Eventi](../../../../docs/standard/events/index.md)   
 [User Input in Windows Forms](../../../../docs/framework/winforms/user-input-in-windows-forms.md)