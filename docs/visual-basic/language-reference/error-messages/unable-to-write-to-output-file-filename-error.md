---
title: "Unable to write to output file &#39;&lt;filename&gt;&#39;: &lt;error&gt; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31019"
  - "bc31019"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31019"
ms.assetid: 0845b245-11bb-46fd-95ca-f6cef3c318ef
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Unable to write to output file &#39;&lt;filename&gt;&#39;: &lt;error&gt;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Si è verificato un problema durante la creazione del file.  
  
 Non è possibile aprire un file di output per la scrittura.  È possibile che il file \(o la cartella contenente il file\) sia aperto per l'uso esclusivo da parte di un altro processo o è stato impostato l'attributo di sola lettura del file.  
  
 Di seguito sono elencate alcune situazioni comuni in cui un file è aperto in modo esclusivo:  
  
-   L'applicazione è già in esecuzione e sta usando i file correlati.  Per risolvere il problema, assicurarsi che l'applicazione non sia in esecuzione.  
  
-   Un'altra applicazione ha aperto il file.  Per risolvere il problema, assicurarsi che altre applicazioni non accedano ai file.  Non è sempre semplice capire quale applicazione sta accedendo ai file. In questo caso, riavviare il computer potrebbe rappresentare il modo più semplice per arrestare l'applicazione.  
  
 Se anche uno solo dei file di output del progetto è contrassegnato come di sola lettura, sarà generata questa eccezione.  
  
 **ID errore:** BC31019  
  
### Per correggere l'errore  
  
1.  Ripetere la compilazione del programma, per controllare se l'errore si verifica di nuovo.  
  
2.  Se l'errore si ripresenta, salvare il lavoro e riavviare [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)].  
  
3.  Se l'errore si ripresenta, riavviare il computer.  
  
4.  Se l'errore si ripete, reinstallare [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
5.  Se l'errore persiste dopo la reinstallazione, inviare una notifica al Servizio Supporto Tecnico Clienti Microsoft.  
  
### Per controllare gli attributi di file in Esplora file  
  
1.  Aprire la cartella a cui si è interessati.  
  
2.  Fare clic sull'icona **Visualizza** e scegliere **Dettagli**.  
  
3.  Fare clic con il pulsante destro del mouse sull'intestazione di colonna, quindi scegliere **Attributi** dall'elenco a discesa.  
  
### Per modificare gli attributi di un file o una cartella  
  
1.  In **Esplora file** fare clic con il pulsante destro del mouse sul file o sulla cartella, quindi scegliere **Proprietà**.  
  
2.  Nella sezione **Attributi** della scheda **Generale** deselezionare la casella di controllo **Sola lettura**.  
  
3.  Fare clic su **OK**.  
  
## Vedere anche  
 [Comunicazioni con Microsoft](/visual-studio/ide/talk-to-us)