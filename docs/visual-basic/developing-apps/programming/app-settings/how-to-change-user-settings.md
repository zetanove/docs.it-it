---
title: 'Procedura: Modificare le impostazioni dell&quot;utente in Visual Basic | Documentazione Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- user settings, changing in Visual Basic
- user settings
- My.Settings object, changing user settings
- examples [Visual Basic], changing user settings
ms.assetid: 41250181-c594-4854-9988-8183b9eb03cf
caps.latest.revision: 18
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1637761f313d75e4385c009ca489ae9667cfd2ad
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-change-user-settings-in-visual-basic"></a>Procedura: modificare le impostazioni dell'utente in Visual Basic
È possibile modificare un'impostazione utente assegnando un nuovo valore alla proprietà dell'impostazione nell'oggetto `My.Settings`.  
  
 L'oggetto `My.Settings` espone ogni impostazione come una proprietà. Il nome della proprietà corrisponde allo stesso nome dell'impostazione e il tipo di proprietà al tipo di impostazione. L'**ambito** dell'impostazione determina se la proprietà è di sola lettura. La proprietà di un'impostazione dell'ambito dell'**applicazione** è di sola lettura, mentre la proprietà di un'impostazione dell'ambito dell'**utente**-è di lettura e scrittura. Per altre informazioni, vedere [Oggetto My.Settings](../../../../visual-basic/language-reference/objects/my-settings-object.md).  
  
> [!NOTE]
>  Sebbene sia possibile modificare e salvare i valori delle impostazioni dell'ambito dell'utente in fase di esecuzione, le impostazioni dell'ambito dell'applicazione sono di sola lettura e non possono essere modificate a livello di codice. È possibile modificare le impostazioni dell'ambito dell'applicazione quando si crea l'applicazione tramite **Creazione progetti** o modificando il file di configurazione dell'applicazione. Per altre informazioni, vedere [Gestione delle impostazioni di un'applicazione (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-settings-dotnet).  
  
## <a name="example"></a>Esempio  
 Questo esempio modifica il valore dell'impostazione utente `Nickname`.  
  
 [!code-vb[VbVbalrMyResources#7](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/how-to-change-user-settings_1.vb)]  
  
 Affinché l'esempio funzioni, l'applicazione deve contenere un'impostazione utente `Nickname` di tipo `String`.  
  
 Alla chiusura dell'applicazione vengono salvate le impostazioni utente. Per salvare immediatamente le impostazioni, chiamare il metodo `My.Settings.Save`. Per altre informazioni, vedere [Procedura: Mantenere le impostazioni dell'utente in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto My.Settings](../../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [Procedura: Leggere le impostazioni dell'applicazione in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [Procedura: Mantenere le impostazioni dell'utente in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [Procedura: Creare griglie di proprietà per impostazioni utente in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)   
 [Gestione delle impostazioni di un'applicazione (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-settings-dotnet)
