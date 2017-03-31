---
title: 'Procedura: Leggere le impostazioni dell&quot;applicazione in Visual Basic | Microsoft Docs'
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
- reading application settings
- My.Settings object, reading application settings
- application settings, reading
ms.assetid: eb3428ef-115e-49a8-a878-e0613183fee0
caps.latest.revision: 12
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
ms.openlocfilehash: e5ad120e52896476447d892438ed9a5d2979da8c
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-read-application-settings-in-visual-basic"></a>Procedura: leggere le impostazioni dell'applicazione in Visual Basic
È possibile leggere un'impostazione utente accedendo alla proprietà dell'impostazione nell'oggetto `My.Settings`.  
  
 L'oggetto `My.Settings` espone ogni impostazione come proprietà. Il nome della proprietà corrisponde al nome dell'impostazione e il tipo di proprietà al tipo di impostazione. L'**ambito** dell'impostazione indica se la proprietà è di sola lettura. La proprietà di un'impostazione dell'ambito **applicazione** è di sola lettura, mentre la proprietà di un'impostazione dell'ambito **utente** è di lettura e scrittura. Per altre informazioni, vedere [Oggetto My.Settings](../../../../visual-basic/language-reference/objects/my-settings-object.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio riportato di seguito viene mostrato il valore dell'impostazione `Nickname`.  
  
 [!code-vb[VbVbalrMyResources#14](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/how-to-read-application-settings_1.vb)]  
  
 Affinché l'esempio funzioni, l'applicazione deve contenere un'impostazione `Nickname` di tipo `String`. Per altre informazioni, vedere [Gestione delle impostazioni di un'applicazione (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-settings-dotnet).  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto My.Settings](../../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [Procedura: Modificare le impostazioni dell'utente in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [Procedura: Mantenere le impostazioni dell'utente in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [Procedura: Creare griglie di proprietà per impostazioni utente in Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)   
 [Gestione delle impostazioni di un'applicazione (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-settings-dotnet)
