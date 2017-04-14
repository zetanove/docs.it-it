---
title: "Procedura: spostare i ToolStripMenuItems | Microsoft Docs"
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
  - "voci di menu, taglia e incolla"
  - "voci di menu, trascinamento della selezione"
  - "voci di menu, spostamento"
  - "menu, disposizione di elementi"
  - "MenuStrip (controllo) [Windows Form], disposizione di elementi"
  - "ToolStripMenuItems, taglia e incolla"
  - "ToolStripMenuItems, trascinamento della selezione"
  - "ToolStripMenuItems, spostamento"
ms.assetid: cab9e03e-4edd-4c25-b3e3-bd1edc602bd9
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: spostare i ToolStripMenuItems
In fase di progettazione, è possibile spostare interi menu di primo livello e i relativi elementi in un punto diverso dell'oggetto <xref:System.Windows.Forms.MenuStrip>.  È possibile anche spostare i singoli elementi fra menu di primo livello o cambiare la posizione degli elementi all'interno di un menu.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per spostare un menu di primo livello e i relativi elementi in un'altra posizione di primo livello  
  
1.  Fare clic e mantenere premuto il tasto sinistro del mouse sull'elemento da spostare.  
  
2.  Trascinare il punto di inserimento sul menu di primo livello che precede la nuova posizione stabilita e rilasciare il tasto sinistro del mouse.  
  
     Il menu selezionato si sposta a destra del punto di inserimento.  
  
### Per spostare un menu di primo livello e i relativi elementi in una posizione a discesa  
  
1.  Fare clic sul menu da spostare con il pulsante sinistro del mouse e premere CTRL \+ X oppure fare clic con il pulsante destro del mouse e selezionare **Taglia** dal menu di scelta rapida.  
  
2.  Nel menu di primo livello di destinazione, fare clic con il pulsante sinistro del mouse al di sopra della nuova posizione stabilita e premere CTRL \+ V oppure fare clic con il pulsante destro del mouse al di sopra della nuova posizione stabilita e selezionare **Incolla** dal menu di scelta rapida.  
  
     Il menu tagliato viene inserito dopo l'elemento di menu selezionato.  
  
### Per spostare un elemento di menu all'interno di un menu usando l'editor della raccolta Items  
  
1.  Fare clic con il pulsante destro del mouse sul menu che contiene l'elemento da spostare.  
  
2.  Scegliere **Modifica DropDownItems** dal menu di scelta rapida.  
  
3.  Nell'**editor della raccolta Items**, fare clic con il pulsante sinistro del mouse sull'elemento di menu da spostare.  
  
4.  Utilizzare i tasti freccia SU e GIÙ per spostare l'elemento all'interno del menu.  
  
5.  Scegliere **OK**.  
  
### Per spostare un elemento all'interno di un menu utilizzando la tastiera  
  
1.  Tenere premuto ALT.  
  
2.  Fare clic e mantenere premuto il tasto sinistro del mouse sull'elemento da spostare.  
  
3.  Trascinare l'elemento nella nuova posizione, quindi rilasciare il pulsante sinistro del mouse.  
  
### Per spostare un elemento in un'altro menu  
  
1.  Fare clic sull'elemento di menu da spostare con il pulsante sinistro del mouse e premere CTRL \+ X oppure fare clic con il pulsante destro del mouse sull'elemento di menu e scegliere **Taglia** dal menu di scelta rapida.  
  
2.  Fare clic con il pulsante sinistro del mouse sul menu che conterrà l'elemento tagliato.  
  
3.  Fare clic con il pulsante sinistro sull'elemento che precede la nuova posizione stabilita e premere CTRL \+ V oppure fare clic con il pulsante destro del mouse sull'elemento che precede la nuova posizione stabilita e selezionare **Incolla** dal menu di scelta rapida.  
  
     L'elemento tagliato viene inserito dopo l'elemento di menu selezionato.  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [Cenni preliminari sul controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)