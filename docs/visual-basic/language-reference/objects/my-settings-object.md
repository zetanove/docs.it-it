---
title: Oggetto My. Settings | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- My.MySettingsProperty.Settings
- My.Settings
dev_langs:
- VB
helpviewer_keywords:
- My.Settings object
ms.assetid: 41f30dc1-202a-4273-b9b7-5728941f996c
caps.latest.revision: 16
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d48d3556f55ef286e2f501e2df5bf5035d3aff90
ms.lasthandoff: 03/13/2017

---
# <a name="mysettings-object"></a>Oggetto My.Settings
Fornisce proprietà e metodi per accedere alle impostazioni dell'applicazione.  
  
## <a name="remarks"></a>Note  
 Il `My.Settings` oggetto fornisce accesso alle impostazioni dell'applicazione e consente di archiviare e recuperare le impostazioni delle proprietà e altre informazioni per l'applicazione in modo dinamico. Per ulteriori informazioni, vedere [impostazioni applicazione di gestione (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-settings-dotnet).  
  
## <a name="properties"></a>Proprietà  
 Le proprietà del `My.Settings` oggetto forniscono accesso alle impostazioni dell'applicazione. Per aggiungere o rimuovere le impostazioni, utilizzare il **Progettazione impostazioni**.  
  
 Ogni impostazione ha un **nome**, **tipo**, **ambito**, e **valore**, e queste impostazioni determinano come la proprietà di accesso a ogni impostazione viene visualizzata nel `My.Settings` oggetto:  
  
-   **Nome** determina il nome della proprietà.  
  
-   **Tipo** determina il tipo della proprietà.  
  
-   **Ambito** indica se la proprietà è di sola lettura. Se il valore è **applicazione**, la proprietà è di sola lettura; se il valore è **utente**, la proprietà è di lettura-scrittura.  
  
-   **Valore** è il valore predefinito della proprietà.  
  
## <a name="methods"></a>Metodi  
  
|Metodo|Descrizione|  
|---|---|  
|`Reload`|Consente di ricaricare le impostazioni utente da ultimi valori salvati.|  
|`Save`|Salva le impostazioni utente correnti.|  
  
 Il `My.Settings` oggetto fornisce inoltre le proprietà avanzate ed ereditati dalla <xref:System.Configuration.ApplicationSettingsBase>classe.</xref:System.Configuration.ApplicationSettingsBase>  
  
## <a name="tasks"></a>Attività  
 Nella tabella seguente sono elencati esempi di attività che coinvolgono il `My.Settings` oggetto.  
  
|Per|Vedere|  
|---|---|  
|Leggere un'impostazione dell'applicazione|[Procedura: leggere le impostazioni dell'applicazione in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)|  
|Modificare un'impostazione utente|[Procedura: modificare le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)|  
|Mantenere le impostazioni utente|[Procedura: mantenere le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)|  
|Creare una griglia delle proprietà per le impostazioni utente|[Procedura: creare griglie di proprietà per le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)|  
  
## <a name="example"></a>Esempio  
 Questo esempio viene visualizzato il valore di `Nickname` impostazione.  
  
 [!code-vb[VbVbalrMyResources&#14;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-settings-object_1.vb)]  
  
 Per eseguire questo esempio, l'applicazione deve contenere un `Nickname` impostazione di tipo `String`.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Configuration.ApplicationSettingsBase></xref:System.Configuration.ApplicationSettingsBase>   
 [Procedura: leggere le impostazioni dell'applicazione in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [Procedura: modificare le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [Procedura: mantenere le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [Procedura: creare griglie di proprietà per le impostazioni utente in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)   
 [Gestione delle impostazioni di un'applicazione (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-settings-dotnet)
