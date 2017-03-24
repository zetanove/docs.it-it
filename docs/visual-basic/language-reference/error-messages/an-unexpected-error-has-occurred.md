---
title: "Si è verificato un errore imprevisto perché non è possibile acquisire una risorsa del sistema operativo necessaria per l&quot;avvio singola istanza | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrAppModel_CantGetMemoryMappedFile
dev_langs:
- VB
ms.assetid: 0d9f2a30-ff72-4355-8060-744f22339359
caps.latest.revision: 10
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
ms.openlocfilehash: 44432a2c393abb01141d09cf5f28c6fd29c5bc43
ms.lasthandoff: 03/13/2017

---
# <a name="an-unexpected-error-has-occurred-because-an-operating-system-resource-required-for-single-instance-startup-cannot-be-acquired"></a>Errore imprevisto. Impossibile acquisire una risorsa del sistema operativo necessaria per l'avvio di istanze singole
L'applicazione non è riuscita ad acquisire una risorsa del sistema operativo necessaria. Alcune possibili cause di questo problema sono:  
  
-   L'applicazione non dispone di autorizzazioni per la creazione di oggetti del sistema operativo denominati.  
  
-   Common Language Runtime non dispone di autorizzazioni per la creazione di file mappati alla memoria.  
  
-   L'applicazione deve accedere a un oggetto del sistema operativo, ma un altro processo lo sta usando.  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Verificare che l'applicazione disponga di autorizzazioni sufficienti per la creazione di oggetti del sistema operativo denominati.  
  
2.  Verificare che Common Language Runtime disponga di autorizzazioni sufficienti per la creazione di file mappati alla memoria.  
  
3.  Riavviare il computer per cancellare i processi che stanno usando la risorsa necessaria per la connessione all'istanza originale.  
  
4.  Prendere nota delle circostanze in cui si è verificato l'errore e contattare il Servizio Supporto Tecnico Clienti Microsoft.  
  
## <a name="see-also"></a>Vedere anche  
 [Application Page, Project Designer (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic)  (Pagina Applicazione, Creazione progetti (Visual Basic))  
 [Nozioni di base del debugger](https://docs.microsoft.com/visualstudio/debugger/debugger-basics)   
 [Comunicazioni con Microsoft](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
