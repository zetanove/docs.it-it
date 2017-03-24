---
title: /errorreport | Documenti di Microsoft
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
- -errorreport compiler option [Visual Basic]
- /errorreport compiler option [Visual Basic]
- errorreport compiler option [Visual Basic]
ms.assetid: a7fe83a2-a6d8-460c-8dad-79a8f433f501
caps.latest.revision: 19
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2ebe5646256926f68a1a900b91c25a1768505785
ms.lasthandoff: 03/13/2017

---
# <a name="errorreport"></a>/errorreport
Specifica la modalità di segnalazione degli errori interni del compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
/errorreport:{ prompt | queue | send | none }  
```  
  
## <a name="remarks"></a>Note  
 Questa opzione offre un modo pratico per segnalare un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] errore interno del compilatore (ICE) per il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] team di Microsoft. Per impostazione predefinita, il compilatore non invia alcuna informazione a Microsoft. Tuttavia, se si verifica un errore interno del compilatore, questa opzione consente di segnalare l'errore a Microsoft. Tali informazioni consentiranno tecnici Microsoft di identificare la causa e potrebbe contribuire a migliorare la prossima versione di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 Capacità di un utente di inviare report dipende dalle autorizzazioni di criteri utente e computer.  
  
 Nella tabella seguente sono riepilogati gli effetti di `/errorreport` (opzione).  
  
|Opzione|Comportamento|  
|---|---|  
|`prompt`|Se si verifica un errore interno del compilatore, una finestra di dialogo viene visualizzata in modo che sia possibile visualizzare i dati esatti raccolti dal compilatore. È possibile determinare se c'è informazioni riservate nella segnalazione errori e decidere se inviarlo a Microsoft. Se si decide di inviarlo, e le impostazioni dei criteri computer e l'utente lo consentono, il compilatore invia i dati a Microsoft.|  
|`queue`|Accoda la segnalazione errori. Quando si accede con privilegi di amministratore, è possibile segnalare gli eventuali errori dall'ultima volta che si fosse connessi in (non verrà richiesto di inviare segnalazioni di errori più di una volta ogni tre giorni). Questo è il comportamento predefinito quando il `/errorreport` opzione non è specificata.|  
|`send`|Se si verifica un errore interno del compilatore e le impostazioni di criteri computer e l'utente lo consentono, il compilatore invia i dati a Microsoft.<br /><br /> L'opzione `/errorReport:send` tenta di inviare automaticamente informazioni sugli errori a Microsoft. Questa opzione varia a seconda del Registro di sistema. Per ulteriori informazioni sull'impostazione i valori appropriati nel Registro di sistema, vedere [come attivare la segnalazione degli errori automatica negli strumenti della riga di comando di Visual Studio 2008](http://go.microsoft.com/fwlink/?LinkID=184695).|  
|`none`|Se si verifica un errore interno del compilatore, non verrà essere raccolti né inviato a Microsoft.|  
  
 Il compilatore invia i dati che includono lo stack al momento dell'errore, che in genere include codice sorgente. Se `/errorreport` viene utilizzato con il [/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md) opzione, viene inviato l'intero file di origine.  
  
 Questa opzione risulta particolarmente utile con il [/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md) opzione perché consente tecnici Microsoft più facilmente riprodurre l'errore.  
  
> [!NOTE]
>  Il `/errorreport` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente tenta di compilare `T2.vb`, e se il compilatore rileva un errore interno del compilatore, viene richiesto di inviare una segnalazione a Microsoft.  
  
```  
vbc /errorreport:prompt t2.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)
