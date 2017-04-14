---
title: "Procedura: riassegnare i controlli esistenti a un padre diverso | Microsoft Docs"
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
  - "controlli contenitore, Windows Form"
  - "layout [Windows Form], ridimensionamento"
  - "layout [Windows Form], controlli figlio"
ms.assetid: 5a5723ff-34e0-4b6f-a57b-be4ebe35cb34
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: riassegnare i controlli esistenti a un padre diverso
È possibile assegnare i controlli presenti nel form a un nuovo controllo contenitore.  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma. Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**. Per altre informazioni, vedere [Personalizzazione delle impostazioni di sviluppo in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per riassegnare i controlli esistenti a un padre diverso  
  
1.  Trascinare i tre controlli <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** al form.  
  
     Posizionarli uno accanto a altro, ma lasciarli non allineati.  
  
2.  Nella **Casella degli strumenti** fare clic sull'icona del controllo <xref:System.Windows.Forms.FlowLayoutPanel>.  
  
     Non trascinare l'icona nel form.  
  
3.  Spostare il puntatore del mouse accanto ai tre controlli <xref:System.Windows.Forms.Button>.  
  
     Il puntatore assume la forma di un mirino con l'icona del controllo <xref:System.Windows.Forms.FlowLayoutPanel> associata.  
  
4.  Fare clic e tenere premuto il pulsante del mouse.  
  
5.  Trascinare il puntatore del mouse per disegnare la struttura del controllo <xref:System.Windows.Forms.FlowLayoutPanel>.  
  
6.  Disegnare la struttura intorno ai tre controlli <xref:System.Windows.Forms.Button>.  
  
7.  Rilasciare il pulsante del mouse.  
  
     I tre controlli <xref:System.Windows.Forms.Button> sono stati inseriti nel controllo <xref:System.Windows.Forms.FlowLayoutPanel>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.FlowLayoutPanel>   
 <xref:System.Windows.Forms.TableLayoutPanel>   
 [Disposizione di controlli in Windows Form](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando guide di allineamento](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)