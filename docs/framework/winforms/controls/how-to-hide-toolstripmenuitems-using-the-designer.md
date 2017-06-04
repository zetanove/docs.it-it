---
title: "Procedura: nascondere ToolStripMenuItems utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "voci di menu, nascondere"
  - "MenuStrip (controllo) [Windows Form], nascondere le voci di menu nella finestra di progettazione"
  - "ToolStripMenuItems, nascondere le voci di menu nella finestra di progettazione"
ms.assetid: 8f1b057e-3d8a-4f11-88df-935f7b29a836
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: nascondere ToolStripMenuItems utilizzando la finestra di progettazione
Nascondere voci di menu è un modo per controllare l'interfaccia utente \(UI\) dell'applicazione e limitare il numero dei comandi accessibili.  Spesso risulta necessario nascondere un intero menu se tutte le voci che ne fanno parte non sono disponibili,  per evitare distrazioni all'utente.  Oltre a nascondere il menu o la voce di menu, potrebbe essere necessario disabilitarlo, in quanto nasconderlo solamente non ne impedisce l'accesso tramite un tasto di scelta rapida.  Per ulteriori informazioni sulla disabilitazione delle voci di menu, vedere [Procedura: disabilitare i ToolStripMenuItems con la finestra di progettazione](../../../../docs/framework/winforms/controls/how-to-disable-toolstripmenuitems-using-the-designer.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per nascondere un menu di primo livello e le relative voci di sottomenu  
  
1.  Selezionare la voce del menu di primo livello e impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Visible%2A> o <xref:System.Windows.Forms.ToolStripItem.Available%2A> su `false`.  
  
     Insieme alla voce del menu di primo livello vengono nascoste anche tutte le voci all'interno di tale menu.  Se non si seleziona <xref:System.Windows.Forms.MenuStrip> dopo aver impostato <xref:System.Windows.Forms.ToolStripItem.Visible%2A> su `false`, l'intera voce del menu di primo livello e le relative voci di sottomenu vengono rimosse dal form, mostrando in tal modo l'effetto dell'operazione in fase di esecuzione.  Per visualizzare la voce di menu di primo livello in fase di progettazione, fare clic su <xref:System.Windows.Forms.MenuStrip> nella **barra dei componenti**, in **Struttura documento** o nella parte superiore della griglia delle proprietà.  
  
> [!NOTE]
>  Raramente sarà necessario nascondere un intero menu, tranne che nel caso dei menu figlio con interfaccia a documenti multipli \(MDI\) in un scenario di unione.  
  
### Per nascondere una voce di sottomenu  
  
1.  Selezionare la voce di sottomenu e impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Visible%2A> su `false`.  
  
     Quando si nasconde una voce di sottomenu, tale voce rimane visibile nel form in fase di progettazione in modo da consentirne la selezione per altre operazioni,  ma risulterà nascosta in fase di esecuzione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStripItem.Visible%2A>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A>   
 <xref:System.Windows.Forms.ToolStripItem.Available%2A>   
 <xref:System.Windows.Forms.ToolStripMenuItem.Overflow%2A>   
 [Cenni preliminari sul controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)   
 [Procedura: disabilitare i ToolStripMenuItems con la finestra di progettazione](../../../../docs/framework/winforms/controls/how-to-disable-toolstripmenuitems-using-the-designer.md)