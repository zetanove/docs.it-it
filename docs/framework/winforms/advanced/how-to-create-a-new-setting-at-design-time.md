---
title: "How To: Create a New Setting at Design Time | Microsoft Docs"
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
  - "application settings [Windows Forms], design time"
  - "application settings [Windows Forms], creating"
ms.assetid: c5d60a66-6507-462f-a81f-e3bc0a804e16
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# How To: Create a New Setting at Design Time
È possibile creare una nuova impostazione in fase di progettazione utilizzando la finestra di progettazione Impostazioni.  La finestra di progettazione Impostazioni è un'interfaccia a griglia che consente di creare nuove impostazioni e di specificarne le proprietà.  Per le nuove impostazioni è necessario specificare Nome, Valore, Tipo e Ambito.  Una volta creata, l'impostazione diventa accessibile nel codice.  
  
### Per creare una nuova impostazione in fase di progettazione in C\#  
  
1.  In **Esplora soluzioni** espandere il nodo **Proprietà** del progetto.  
  
2.  Fare doppio clic sul file con estensione SETTINGS in cui si desidera aggiungere una nuova impostazione.  Il nome predefinito per questo file è Settings.settings.  
  
3.  Nella finestra di progettazione Impostazioni impostare Nome, Valore, Tipo e Ambito per l'impostazione.  Ogni riga rappresenta una sola impostazione.  
  
### Per creare una nuova impostazione in fase di progettazione in Visual Basic  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Proprietà**.  
  
2.  Nella pagina **Proprietà** selezionare la scheda **Impostazioni**.  
  
3.  Nella finestra di progettazione Impostazioni impostare Nome, Valore, Tipo e Ambito per l'impostazione.  Ogni riga rappresenta una sola impostazione.  
  
## Vedere anche  
 [Using Application Settings and User Settings](../../../../docs/framework/winforms/advanced/using-application-settings-and-user-settings.md)   
 [Cenni preliminari sulle impostazioni delle applicazioni](../../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [How To: Change the Value of an Existing Setting at Design Time](../../../../docs/framework/winforms/advanced/how-to-change-the-value-of-an-existing-setting-at-design-time.md)