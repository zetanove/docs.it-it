---
title: Errore di accesso percorso-File | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID75
dev_langs:
- VB
ms.assetid: 6ce3a161-7316-46bd-a785-0d50e5414020
caps.latest.revision: 8
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
ms.openlocfilehash: ac730bac76540331206daebe600445ca54cc15a9
ms.lasthandoff: 03/13/2017

---
# <a name="pathfile-access-error"></a>Errore di accesso al percorso/file
Durante un'operazione di accesso ai file o l'accesso al disco, il sistema operativo non ha potuto fare una connessione tra il percorso e il nome del file.  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Assicurarsi che la specifica del file è formattata correttamente. Un nome file può contenere un nome completo (assoluto) o il relativo percorso. Il percorso completo inizia con il nome dell'unità (se il percorso in un'altra unità) ed elenca il percorso esplicito dalla radice del file. Qualsiasi percorso che non è completo è relativo l'unità corrente e la directory.  
  
2.  Assicurarsi che non si tenta di salvare un file che è necessario sostituire un file di sola lettura esistente. In questo caso, modificare l'attributo di sola lettura del file di destinazione o salvare il file con un nome file diverso.  
  
3.  Assicurarsi di non aver tentato di aprire un file di sola lettura in sequenza`Output`o `Append` modalità. In questo caso, aprire il file in `Input` modalità o modifica l'attributo di sola lettura del file.  
  
4.  Assicurarsi di non aver tentato di modificare un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] progetto all'interno di un database o un documento.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di errore](../../../visual-basic/programming-guide/language-features/error-types.md)
