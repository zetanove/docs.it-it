---
title: 'Procedura: Controllare lo stato della connessione in Visual Basic | Microsoft Docs'
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
- Web connections
- IsAvailable property, about IsAvailable
- connections, checking status
- connection status
ms.assetid: 4d9ee8ab-9a6f-4279-ace4-b75afc976a74
caps.latest.revision: 26
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
ms.openlocfilehash: 81386ee1f8c8cefbcd34a05d594277b9de772b8d
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-check-connection-status-in-visual-basic"></a>Procedura: controllare lo stato di connessione in Visual Basic
Per determinare se il computer ha una rete o una connessione Internet funzionante, è possibile usare la proprietà <xref:Microsoft.VisualBasic.Devices.Network.IsAvailable%2A>.  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-check-whether-a-computer-has-a-working-connection"></a>Per verificare se un computer ha una connessione funzionante  
  
-   Determinare se la proprietà `IsAvailable` è `True` o `False`. Il codice seguente controlla lo stato della proprietà e lo segnala:  
  
     [!code-vb[VbResourceTasks#3](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-check-connection-status_1.vb)]  
  
     Questo esempio di codice è disponibile anche come frammento di codice IntelliSense. Nella selezione del frammento di codice si trova in **Connettività e rete**. Per altre informazioni, vedere [Code Snippets](https://docs.microsoft.com/visualstudio/ide/code-snippets) (Frammenti di codice).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Network?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Devices.Network.IsAvailable%2A>

