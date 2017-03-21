---
title: AddHandler (istruzione) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.AddHandlerMethod
- addhandler
- vb.addhandler
dev_langs:
- VB
helpviewer_keywords:
- AddHandler statement
ms.assetid: cfe69799-2a0f-42c0-a99e-09fed954da01
caps.latest.revision: 15
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
ms.openlocfilehash: 728d8393c44d777f9cc016d9cf66030036582ae4
ms.lasthandoff: 03/13/2017

---
# <a name="addhandler-statement"></a>Istruzione AddHandler
Associa un evento al gestore eventi in fase di esecuzione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
AddHandler event, AddressOf eventhandler  
```  
  
## <a name="parts"></a>Parti  
 `event`  
 Il nome dell'evento da gestire.  
  
 `eventhandler`  
 Il nome di una routine che gestisce l'evento.  
  
## <a name="remarks"></a>Note  
 Il `AddHandler` e `RemoveHandler` istruzioni consentono di avviare e interrompere la gestione degli eventi in qualsiasi momento durante l'esecuzione del programma.  
  
 La firma di `eventhandler` procedura deve corrispondere alla firma dell'evento `event`.  
  
 La parola chiave `Handles` e l'istruzione `AddHandler` consentono entrambe di specificare che quelle particolari routine gestiscono particolari eventi, ma esistono alcune differenze. L'istruzione `AddHandler` connette le routine agli eventi in fase di esecuzione. Usare la parola chiave `Handles` quando si definisce una routine, per specificare che questa gestisce un particolare evento. Per ulteriori informazioni, vedere [gestisce](../../../visual-basic/language-reference/statements/handles-clause.md).  
  
> [!NOTE]
>  Per gli eventi personalizzati, il `AddHandler` istruzione richiama l'evento `AddHandler` della funzione di accesso. Per ulteriori informazioni sugli eventi personalizzati, vedere [istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md).  
  
## <a name="example"></a>Esempio  
 [!code-vb[VbVbalrEvents n.&17;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/addhandler-statement_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [RemoveHandler (istruzione)](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [Handle](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Eventi](../../../visual-basic/programming-guide/language-features/events/index.md)
