---
title: /bugreport | Documenti di Microsoft
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
- -bugreport compiler option [Visual Basic]
- bugreport compiler option [Visual Basic]
- /bugreport compiler option [Visual Basic]
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
caps.latest.revision: 22
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 9c64ec49d7e6842edbc0fed7407a34132a8f5a88
ms.lasthandoff: 03/13/2017

---
# <a name="bugreport"></a>/bugreport
Crea un file che è possibile utilizzare quando si invia una segnalazione di bug.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/bugreport:file  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`file`|Obbligatorio. Il nome del file che conterrà il report sui bug. Racchiudere il nome del file tra virgolette ("") se il nome contiene uno spazio.|  
  
## <a name="remarks"></a>Note  
 Le informazioni seguenti vengono aggiunte a `file`:  
  
-   Una copia di tutti i file di codice sorgente nella compilazione.  
  
-   Un elenco di opzioni del compilatore utilizzate nella compilazione.  
  
-   Informazioni sulla versione su cui il compilatore, common language runtime e del sistema operativo.  
  
-   Compilatore di output, se presente.  
  
-   Descrizione del problema, per cui viene richiesto.  
  
-   Una descrizione di come si ritiene che il problema deve essere corretto per il quale viene richiesto.  
  
 Poiché una copia di tutti i file di codice sorgente è incluso `file`, è possibile riprodurre l'errore del codice (sospetta) nel programma più breve.  
  
> [!IMPORTANT]
>  Il `/bugreport` opzione produce un file che contiene informazioni potenzialmente riservate. Ora corrente, versione del compilatore, [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] versione, versione del sistema operativo, nome utente, gli argomenti della riga di comando con cui il compilatore è stato eseguito, tutto il codice sorgente e il formato binario di qualsiasi assembly a cui viene fatto riferimento. Questa opzione è possibile accedere specificando le opzioni della riga di comando nel file Web. config per una compilazione sul lato server di un [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] dell'applicazione. Per evitare questo problema, modificare il file Machine. config per impedire agli utenti di compilazione sul server.  
  
 Se questa opzione viene utilizzata con `/errorreport:prompt`, `/errorreport:queue`, o `/errorreport:send`, e l'applicazione rileva un errore interno del compilatore, le informazioni contenute in `file` viene inviato a Microsoft Corporation. Tali informazioni consentirà tecnici Microsoft di identificare la causa dell'errore e di migliorare la prossima versione di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Per impostazione predefinita, viene inviata alcuna informazione a Microsoft. Tuttavia, quando si compila un'applicazione utilizzando `/errorreport:queue`, che è attivata per impostazione predefinita, l'applicazione recupera i report degli errori. Quindi, quando l'amministratore del computer accede, il sistema di segnalazione errori visualizza una finestra popup che consente all'amministratore di inoltrare a Microsoft i report degli errori che si sono verificati dopo l'accesso.  
  
> [!NOTE]
>  Il `/bugreport` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo quando si compila dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene compilato `T2.vb` e tutte le informazioni di segnalazione dei bug nel file `Problem.txt`.  
  
```  
vbc /bugreport:problem.txt t2.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)   
 [/errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Elemento trustLevel per securityPolicy (Schema delle impostazioni ASP.NET)](http://msdn.microsoft.com/en-us/729ab04c-03da-4ee5-86b1-be9d08a09369)
