---
title: "How to: Read Application Settings in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "reading application settings"
  - "My.Settings object, reading application settings"
  - "application settings, reading"
ms.assetid: eb3428ef-115e-49a8-a878-e0613183fee0
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Read Application Settings in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Per leggere una impostazione utente accedere alla proprietà dell'impostazione nell'oggetto `My.Settings`.  
  
 L'oggetto `My.Settings` visualizza ogni impostazione come proprietà.  Il nome della proprietà corrisponde al nome dell'impostazione e il tipo di proprietà al tipo di impostazione.  L'**Ambito** dell'impostazione indica se la proprietà è in sola lettura. La proprietà dell'impostazione dell'ambito **Application** è in sola lettura, mentre la proprietà dell'impostazione dell'ambito **Utente** è in lettura e scrittura.  Per ulteriori informazioni, vedere [My.Settings Object](../../../../visual-basic/language-reference/objects/my-settings-object.md).  
  
## Esempio  
 Nell'esempio riportato di seguito viene mostrato il valore dell'impostazione `Nickname`.  
  
 [!code-vb[VbVbalrMyResources#14](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/how-to-read-application-settings_1.vb)]  
  
 Perché l'esempio funzioni, l'applicazione deve disporre dell'impostazione `Nickname`, di tipo `String`.  Per ulteriori informazioni, vedere [Gestione delle impostazioni di un'applicazione \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet).  
  
## Vedere anche  
 [My.Settings Object](../../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [How to: Change User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [How to: Persist User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [How to: Create Property Grids for User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)   
 [Gestione delle impostazioni di un'applicazione \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)