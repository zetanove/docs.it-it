---
title: "How To: Change the Value of a Setting Between Application Sessions | Microsoft Docs"
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
  - "application settings [Windows Forms], changing"
  - "application settings [Windows Forms], between application sessions"
ms.assetid: 1a85911f-97b2-476c-930b-83379edd890c
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# How To: Change the Value of a Setting Between Application Sessions
In alcuni casi può essere necessario modificare il valore di un'impostazione tra le sessioni dell'applicazione dopo la compilazione e la distribuzione dell'applicazione.  Ad esempio, può essere necessario modificare una stringa di connessione affinché punti al percorso del database corretto.  Poiché gli strumenti in fase di progettazione non sono disponibili dopo la compilazione e la distribuzione dell'applicazione, è necessario modificare manualmente il valore dell'impostazione nel file.  
  
### Per modificare il valore di un'impostazione tra le sessioni dell'applicazione  
  
1.  Aprire il file con estensione CONFIG associato all'applicazione utilizzando il Blocco note di Microsoft o un altro editor di testo o editor XML.  
  
2.  Individuare la voce per l'impostazione da modificare.  Deve essere simile all'esempio illustrato di seguito.  
  
    ```  
    <setting name="Setting1" serializeAs="String" >  
       <value>My Setting Value</value>  
    </setting>  
    ```  
  
3.  Digitare un valore nuovo per l'impostazione e salvare il file.  
  
## Vedere anche  
 [Using Application Settings and User Settings](../../../../docs/framework/winforms/advanced/using-application-settings-and-user-settings.md)   
 [Cenni preliminari sulle impostazioni delle applicazioni](../../../../docs/framework/winforms/advanced/application-settings-overview.md)