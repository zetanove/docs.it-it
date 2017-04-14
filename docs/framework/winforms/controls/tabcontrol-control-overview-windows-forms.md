---
title: "Cenni preliminari sul controllo TabControl (Windows Form) | Microsoft Docs"
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
  - "TabControl"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "proprietà (pagine), Windows Form"
  - "schede, informazioni sulle pagine con schede"
  - "TabControl (controllo) [Windows Form], informazioni sul controllo TabControl"
  - "Windows Form (finestre di dialogo), schede"
ms.assetid: 2b4ea784-a39d-463c-81d8-af74ce068476
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sul controllo TabControl (Windows Form)
Il controllo <xref:System.Windows.Forms.TabControl> di Windows Form consente di visualizzare più schede, come i divisori di un raccoglitore o le etichette di una serie di cartelle da archivio.  Le schede possono contenere immagini e altri controlli.  È possibile utilizzare questo controllo per generare il tipo di finestra di dialogo a più pagine visualizzato in diversi punti nel sistema operativo Windows, come la finestra Proprietà \- Schermo del Pannello di controllo.  Inoltre, il controllo <xref:System.Windows.Forms.TabControl> può essere utilizzato per creare pagine delle proprietà, utilizzate per impostare un gruppo di proprietà collegate.  
  
## Utilizzo di TabControl  
 La proprietà più importante del controllo <xref:System.Windows.Forms.TabControl> è <xref:System.Windows.Forms.TabControl.TabPages%2A>, che contiene le singole schede.  Ciascuna scheda è un oggetto <xref:System.Windows.Forms.TabPage>.  Quando si fa clic su una scheda, viene generato l'evento <xref:System.Windows.Forms.Control.Click> per l'oggetto <xref:System.Windows.Forms.TabPage> corrispondente.  
  
## Vedere anche  
 <xref:System.Windows.Forms.TabControl>   
 [Controllo TabControl](../../../../docs/framework/winforms/controls/tabcontrol-control-windows-forms.md)   
 [Procedura: modificare l'aspetto del controllo TabControl Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)   
 [Procedura: aggiungere un controllo a un oggetto TabPage](../../../../docs/framework/winforms/controls/how-to-add-a-control-to-a-tab-page.md)   
 [Procedura: aggiungere e rimuovere schede tramite il controllo TabControl Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol.md)   
 [Procedura: disabilitare le schede](../../../../docs/framework/winforms/controls/how-to-disable-tab-pages.md)   
 [Dialog Boxes in Windows Forms](../../../../docs/framework/winforms/dialog-boxes-in-windows-forms.md)