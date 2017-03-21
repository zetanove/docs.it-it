---
title: 'Impossibile scrivere nel file di output &quot;&lt;filename&gt;&quot;: &lt;errore&gt; | Documenti di Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc31019
- bc31019
dev_langs:
- VB
helpviewer_keywords:
- BC31019
ms.assetid: 0845b245-11bb-46fd-95ca-f6cef3c318ef
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
ms.openlocfilehash: fe093ec3b36ba733cb9b0c162e242c8dce6b7c78
ms.lasthandoff: 03/13/2017

---
# <a name="unable-to-write-to-output-file-39ltfilenamegt39-lterrorgt"></a>Impossibile scrivere nel file di output '&lt;filename&gt;': &lt;errore&gt;
Si è verificato un problema durante la creazione del file.  
  
 Non è possibile aprire un file di output per la scrittura. È possibile che il file (o la cartella contenente il file) sia aperto per l'uso esclusivo da parte di un altro processo o è stato impostato l'attributo di sola lettura del file.  
  
 Di seguito sono elencate alcune situazioni comuni in cui un file è aperto in modo esclusivo:  
  
-   L'applicazione è già in esecuzione e sta usando i file correlati. Per risolvere il problema, assicurarsi che l'applicazione non sia in esecuzione.  
  
-   Un'altra applicazione ha aperto il file. Per risolvere il problema, assicurarsi che altre applicazioni non accedano ai file. Non è sempre semplice capire quale applicazione sta accedendo ai file. In questo caso, riavviare il computer potrebbe rappresentare il modo più semplice per arrestare l'applicazione.  
  
 Se anche uno solo dei file di output del progetto è contrassegnato come di sola lettura, sarà generata questa eccezione.  
  
 **ID errore:** BC31019  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Ripetere la compilazione del programma, per controllare se l'errore si verifica di nuovo.  
  
2.  Se l'errore si ripresenta, salvare il lavoro e riavviare [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)].  
  
3.  Se l'errore si ripresenta, riavviare il computer.  
  
4.  Se l'errore si ripete, reinstallare [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
5.  Se l'errore persiste dopo la reinstallazione, inviare una notifica al Servizio Supporto Tecnico Clienti Microsoft.  
  
### <a name="to-check-file-attributes-in-file-explorer"></a>Per controllare gli attributi di file in Esplora file  
  
1.  Aprire la cartella a cui si è interessati.  
  
2.  Fare clic su di **viste** icona e scegliere **dettagli**.  
  
3.  Fare clic sull'intestazione di colonna e scegliere **attributi** dall'elenco a discesa.  
  
### <a name="to-change-the-attributes-of-a-file-or-folder"></a>Per modificare gli attributi di un file o una cartella  
  
1.  In **Esplora File**, fare doppio clic su file o della cartella e scegliere **proprietà**.  
  
2.  Nel **attributi** sezione il **generale** scheda, deseleziona il **Read-only** casella.  
  
3.  Press **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Talk to Us](https://docs.microsoft.com/visualstudio/ide/talk-to-us) (Comunicazioni con Microsoft)
