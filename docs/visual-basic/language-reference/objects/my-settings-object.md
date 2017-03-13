---
title: "Oggetto My.Settings | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "My.MySettingsProperty.Settings"
  - "My.Settings"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Settings (oggetto)"
ms.assetid: 41f30dc1-202a-4273-b9b7-5728941f996c
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Oggetto My.Settings
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Fornisce proprietà e metodi per accedere alle impostazioni dell'applicazione.  
  
## <a name="remarks"></a>Note  
 Il `My.Settings` oggetto fornisce accesso alle impostazioni dell'applicazione e consente di archiviare e recuperare le impostazioni delle proprietà e altre informazioni per l'applicazione in modo dinamico. Per ulteriori informazioni, vedere [Impostazioni applicazione di gestione (.NET)](/visual-studio/ide/managing-application-settings-dotnet).  
  
## <a name="properties"></a>Proprietà  
 Le proprietà del `My.Settings` oggetto forniscono accesso alle impostazioni dell'applicazione. Per aggiungere o rimuovere le impostazioni, utilizzare il **Progettazione impostazioni**.  
  
 Ogni impostazione ha un **nome**, **tipo**, **ambito**, e **valore**, e queste impostazioni determinano come la proprietà di accesso a ogni impostazione viene visualizzata nel `My.Settings` oggetto:  
  
-   **Nome** determina il nome della proprietà.  
  
-   **Tipo** determina il tipo della proprietà.  
  
-   **Ambito** indica se la proprietà è di sola lettura. Se il valore è **applicazione**, la proprietà è di sola lettura; se il valore è **utente**, la proprietà è di lettura-scrittura.  
  
-   **Valore** è il valore predefinito della proprietà.  
  
## <a name="methods"></a>Metodi  
  
|||  
|-|-|  
|Metodo|Descrizione|  
|`Reload`|Consente di ricaricare le impostazioni utente da ultimi valori salvati.|  
|`Save`|Salva le impostazioni utente correnti.|  
  
 Il `My.Settings` oggetto fornisce inoltre proprietà e metodi, ereditati da avanzati di <xref:System.Configuration.ApplicationSettingsBase> (classe).  
  
## <a name="tasks"></a>Attività  
 Nella tabella seguente sono elencati esempi di attività che coinvolgono il `My.Settings` oggetto.  
  
|||  
|-|-|  
|Per|Vedere|  
|Leggere un'impostazione dell'applicazione|[Procedura: leggere le impostazioni dell'applicazione in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)|  
|Modificare un'impostazione utente|[Procedura: modificare le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)|  
|Mantenere le impostazioni utente|[Procedura: mantenere le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)|  
|Creare una griglia delle proprietà per le impostazioni utente|[Procedura: creare griglie di proprietà per le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)|  
  
## <a name="example"></a>Esempio  
 Questo esempio viene visualizzato il valore di `Nickname` impostazione.  
  
 [!code-vb[VbVbalrMyResources#14](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-settings-object_1.vb)]  
  
 Per eseguire questo esempio, l'applicazione deve contenere un `Nickname` impostazione di tipo `String`.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Configuration.ApplicationSettingsBase>   
 [Procedura: leggere le impostazioni dell'applicazione in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [Procedura: modificare le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [Procedura: mantenere le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [Procedura: creare griglie di proprietà per le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)   
 [Gestione delle impostazioni dell'applicazione (.NET)](/visual-studio/ide/managing-application-settings-dotnet)