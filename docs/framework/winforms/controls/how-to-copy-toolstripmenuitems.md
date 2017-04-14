---
title: "Procedura: copiare ToolStripMenuItems | Microsoft Docs"
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
  - "voci di menu, operazioni di copia e incolla"
  - "controllo MenuStrip [Windows Form], disposizione degli elementi"
  - "ToolStripMenuItems, operazioni di copia e incolla"
ms.assetid: 17ef4207-e92e-4db2-b648-27246e6517ad
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: copiare ToolStripMenuItems
In fase di progettazione è possibile copiare interi menu di primo livello e le voci dei relativi sottomenu in un'altra posizione in <xref:System.Windows.Forms.MenuStrip>. È anche possibile copiare singole voci di menu tra i menu di primo livello o modificare la posizione delle voci di menu all'interno di un menu.  
  
### Per copiare un menu di primo livello e le voci dei relativi sottomenu in un'altra posizione di primo livello  
  
1.  Fare clic sul menu da copiare, premere CTRL\+C o fare clic con il pulsante destro del mouse sul menu e selezionare **Copia** dal menu di scelta rapida.  
  
2.  Fare clic sul menu di primo livello dopo la nuova posizione individuata e premere CTRL\+V oppure fare clic con il pulsante destro del mouse sulla voce di menu di primo livello che precede la nuova posizione e selezionare **Incolla** dal menu di scelta rapida.  
  
     Il menu copiato viene inserito prima del menu di primo livello selezionato.  
  
### Per copiare un menu di primo livello e le voci dei relativi sottomenu in una posizione a discesa  
  
1.  Fare clic sul menu da spostare, premere CTRL\+C o fare clic con il pulsante destro del mouse sul menu e selezionare **Copia** dal menu di scelta rapida.  
  
2.  Nel menu di primo livello di destinazione, fare clic sulla voce del sottomenu che precede la nuova posizione individuata e premere CTRL\+V oppure fare clic con il pulsante destro del mouse sulla voce di sottomenu che precede la nuova posizione e selezionare **Incolla** dal menu di scelta rapida.  
  
     Il menu copiato viene inserito prima della voce di sottomenu selezionata.  
  
### Per copiare una voce di sottomenu in un altro menu  
  
1.  Fare clic sulla voce di sottomenu da copiare, premere CTRL\+C o fare clic con il pulsante destro del mouse sulla voce di sottomenu e selezionare **Copia** dal menu di scelta rapida.  
  
2.  Fare clic sul menu che conterrà la voce di sottomenu tagliata.  
  
3.  Fare clic sulla voce di sottomenu che precede la nuova posizione individuata e premere CTRL\+V oppure fare clic con il pulsante destro del mouse sulla voce di sottomenu che precede la nuova posizione e selezionare **Incolla** dal menu di scelta rapida.  
  
     La voce di sottomenu copiata viene inserita prima della voce di sottomenu selezionata.  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [Cenni preliminari sul controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)