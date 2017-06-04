---
title: "How To: Add Multiple Sets of Settings To Your Application in C# | Microsoft Docs"
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
  - "application settings [Windows Forms], multiple sets"
  - "application settings [Windows Forms], C#"
ms.assetid: 45007ac6-cf07-4be7-bc38-3f0ef962faf9
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# How To: Add Multiple Sets of Settings To Your Application in C# #
In alcuni casi può essere necessario avere più insiemi di impostazioni in un'applicazione.  Ad esempio, se si sta sviluppando un'applicazione in cui si prevede di modificare spesso un determinato gruppo di impostazioni, è consigliabile raggrupparle tutte in un unico file da poter sostituire globalmente, lasciando invariate le altre impostazioni.  Visual Studio consente di aggiungere più insiemi di impostazioni al progetto.  È possibile accedere ad altri insiemi di impostazioni tramite l'oggetto Properties.Settings.  
  
### Per aggiungere un ulteriore insieme di impostazioni all'applicazione  
  
1.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  Viene aperta la finestra di dialogo **Aggiungi nuovo elemento**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **File di impostazioni**, digitare un nome per il file e fare clic su **Aggiungi** per aggiungere un nuovo file di impostazioni alla soluzione.  
  
3.  In **Esplora soluzioni** trascinare il nuovo file di impostazioni nella cartella **Proprietà**.  In tal modo le nuove impostazioni saranno disponibili nel codice.  
  
4.  Aggiungere e utilizzare le impostazioni in questo file come un qualsiasi altro file di impostazioni.  È possibile accedere a questo gruppo di impostazioni tramite l'oggetto Properties.Settings.  
  
## Vedere anche  
 [Using Application Settings and User Settings](../../../../docs/framework/winforms/advanced/using-application-settings-and-user-settings.md)   
 [Cenni preliminari sulle impostazioni delle applicazioni](../../../../docs/framework/winforms/advanced/application-settings-overview.md)