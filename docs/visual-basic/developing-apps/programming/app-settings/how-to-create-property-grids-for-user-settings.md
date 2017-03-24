---
title: "How to: Create Property Grids for User Settings in Visual Basic | Microsoft Docs"
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
  - "My.Settings object, creating property grids for user settings"
  - "user settings, creating property grids"
  - "property grids, creating for user settings"
  - "property grids"
ms.assetid: b0bc737e-50d1-43d1-a6df-268db6e6f91c
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# How to: Create Property Grids for User Settings in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile creare una griglia delle proprietà per le impostazioni utente popolando un controllo <xref:System.Windows.Forms.PropertyGrid> con le proprietà delle impostazioni utente dell'oggetto `My.Settings`.  
  
> [!NOTE]
>  Affinché questo esempio funzioni, è necessario aver configurato le impostazioni utente sull'applicazione.  Per ulteriori informazioni, vedere [Gestione delle impostazioni di un'applicazione \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet).  
  
 L'oggetto `My.Settings` visualizza ogni impostazione come proprietà.  Il nome della proprietà corrisponde al nome dell'impostazione e il tipo di proprietà al tipo di impostazione.  L'**Ambito** dell'impostazione determina se la proprietà è in sola lettura. La proprietà per un'impostazione relativa all'**Applicazione** è in sola lettura, mentre la proprietà per un impostazione relativa all'**Utente** è in lettura\-scrittura.  Per ulteriori informazioni, vedere [My.Settings Object](../../../../visual-basic/language-reference/objects/my-settings-object.md).  
  
> [!NOTE]
>  Non è possibile modificare o salvare i valori delle impostazioni relative all'applicazione in fase di esecuzione.  Le impostazioni relative all'applicazione possono essere modificate solo in fase di creazione dell'applicazione mediante **Progettazione progetti** o modificando il file di configurazione dell'applicazione.  Per ulteriori informazioni, vedere [Gestione delle impostazioni di un'applicazione \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet).  
  
 Nell'esempio riportato di seguito viene utilizzato un controllo <xref:System.Windows.Forms.PropertyGrid> per accedere alle proprietà di impostazione utente dell'oggetto `My.Settings`.  Per impostazione predefinita, nella <xref:System.Windows.Forms.PropertyGrid> sono mostrate tutte le proprietà dell'oggetto `My.Settings`.  Tuttavia, alle proprietà delle impostazioni utente è associato l'attributo <xref:System.Configuration.UserScopedSettingAttribute>.  Nell'esempio riportato di seguito viene impostata la proprietà <xref:System.Windows.Forms.PropertyGrid.BrowsableAttributes%2A> della <xref:System.Windows.Forms.PropertyGrid> su <xref:System.Configuration.UserScopedSettingAttribute> per visualizzare solo le proprietà delle impostazioni utente.  
  
### Per aggiungere una griglia delle proprietà delle impostazioni utente  
  
1.  Dalla **Casella degli strumenti**, aggiungere il controllo **PropertyGrid** all'area di progettazione dell'applicazione, considerata nell'esempio come  `Form1`.  
  
     Il nome predefinito del controllo property\-grid è `PropertyGrid1`.  
  
2.  Fare doppio clic sull'area di progettazione per `Form1` per aprire il codice per il gestore eventi di caricamento del form.  
  
3.  Impostare l'oggetto `My.Settings` come l'oggetto selezionato per la griglia delle proprietà.  
  
     [!code-vb[VbVbalrMyResources#11](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/how-to-create-property-grids-for-user-settings_1.vb)]  
  
4.  Configurare la griglia delle proprietà in modo da mostrare solo le impostazioni utente.  
  
     [!code-vb[VbVbalrMyResources#12](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/how-to-create-property-grids-for-user-settings_2.vb)]  
  
    > [!NOTE]
    >  Per mostrare solo le impostazioni con ambito di applicazione, utilizzare l'attributo <xref:System.Configuration.ApplicationScopedSettingAttribute> anziché <xref:System.Configuration.UserScopedSettingAttribute>.  
  
## Programmazione efficiente  
 Le impostazioni utente saranno salvate alla chiusura dell'applicazione.   Per salvare immediatamente le impostazioni, chiamare il metodo `My.Settings.Save`,  Per ulteriori informazioni, vedere [How to: Persist User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md).  
  
## Vedere anche  
 [My.Settings Object](../../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [How to: Read Application Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [How to: Change User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [How to: Persist User Settings in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [Gestione delle impostazioni di un'applicazione \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)