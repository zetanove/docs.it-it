---
title: "How to: Persist User Settings in Visual Basic | Microsoft Docs"
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
  - "My.Settings object, persisting user settings"
  - "persistence, persisting user settings [Visual Basic]"
  - "user settings, persisting"
ms.assetid: 0e5e6415-b6e2-4602-9be0-a65fa167d007
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Persist User Settings in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile utilizzare il metodo `My.Settings.Save` per mantenere le modifiche apportate alle impostazioni dell'utente.  
  
 Di solito, le applicazioni vengono progettate in modo da conservare le modifiche alle impostazioni dell'utente quando l'applicazione viene chiusa.  Salvare le impostazioni richiede di norma, in base a una serie di fattori, diversi secondi.  
  
 Per ulteriori informazioni, vedere [My.Settings Object](../../../../visual-basic/language-reference/objects/my-settings-object.md).  
  
> [!NOTE]
>  Sebbene sia possibile modificare e salvare i valori delle impostazioni relative all'ambito utente in fase di esecuzione, le impostazioni relative all'applicazione sono in sola lettura e non è possibile modificarle a livello di codice.  Le impostazioni relative all'applicazione possono essere modificate solo in fase di creazione dell'applicazione mediante **Progettazione progetti** o modificando il file di configurazione dell'applicazione.  Per ulteriori informazioni, vedere [Gestione delle impostazioni di un'applicazione \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet).  
  
## Esempio  
 In questo esempio viene modificato il valore dell'impostazione utente `LastChanged` e la modifica viene salvata richiamando il metodo `My.Settings.Save`.  
  
 [!code-vb[VbVbalrMyResources#5](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/how-to-persist-user-settings_1.vb)]  
  
 Per poter utilizzare questo esempio, è necessario che nell'applicazione sia presente un'impostazione dell'utente `LastChanged` del tipo `Date`.  Per ulteriori informazioni, vedere [Gestione delle impostazioni di un'applicazione \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet).  
  
## Vedere anche  
 [My.Settings Object](../../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [How to: Read Application Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [How to: Change User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [How to: Create Property Grids for User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)   
 [Gestione delle impostazioni di un'applicazione \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)