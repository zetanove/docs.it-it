---
title: "How to: Change User Settings in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "user settings, changing in Visual Basic"
  - "user settings"
  - "My.Settings object, changing user settings"
  - "examples [Visual Basic], changing user settings"
ms.assetid: 41250181-c594-4854-9988-8183b9eb03cf
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# How to: Change User Settings in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile modificare le impostazioni dell'utente assegnando un nuovo valore alla relativa proprietà nell'oggetto`My.Settings`.  
  
 L'oggetto `My.Settings` visualizza ogni impostazione come proprietà.  Il nome della proprietà corrisponde al nome dell'impostazione e il tipo di proprietà al tipo di impostazione.  Il valore di **Ambito** dell'impostazione determina se la proprietà è di sola lettura: la proprietà per un'impostazione di ambito **Applicazione** è di sola lettura, mentre la proprietà per un'impostazione di ambito **Utente** è di lettura e scrittura.  Per ulteriori informazioni, vedere [My.Settings Object](../../../../visual-basic/language-reference/objects/my-settings-object.md).  
  
> [!NOTE]
>  Sebbene sia possibile modificare e salvare i valori delle impostazioni relative all'ambito utente in fase di esecuzione, le impostazioni relative all'applicazione sono in sola lettura e non è possibile modificarle a livello di codice.  Le impostazioni relative all'ambito dell'applicazione possono essere modificate in fase di creazione dell'applicazione mediante **Progettazione progetti** o modificando il file di configurazione dell'applicazione.  Per ulteriori informazioni, vedere [Gestione delle impostazioni di un'applicazione \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet).  
  
## Esempio  
 In questo esempio, viene modificato il valore dell'impostazione utente `Nickname`.  
  
 [!code-vb[VbVbalrMyResources#7](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#7)]  
  
 Per poter utilizzare questo esempio, è necessario che nell'applicazione sia presente un'impostazione dell'utente `Nickname` del tipo `String`.  
  
 Le impostazioni utente saranno salvate alla chiusura dell'applicazione.   Per salvare immediatamente le impostazioni, chiamare il metodo `My.Settings.Save`,  Per ulteriori informazioni, vedere [How to: Persist User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md).  
  
## Vedere anche  
 [My.Settings Object](../../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [How to: Read Application Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [How to: Persist User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [How to: Create Property Grids for User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)   
 [Gestione delle impostazioni di un'applicazione \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)