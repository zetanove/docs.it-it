---
title: "/errorreport | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "-errorreport compiler option [Visual Basic]"
  - "/errorreport compiler option [Visual Basic]"
  - "errorreport compiler option [Visual Basic]"
ms.assetid: a7fe83a2-a6d8-460c-8dad-79a8f433f501
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# /errorreport
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di specificare in che modo il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] segnalerà i relativi errori interni.  
  
## Sintassi  
  
```  
/errorreport:{ prompt | queue | send | none }  
```  
  
## Note  
 Questa opzione fornisce un modo pratico per segnalare un errore interno del compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] al team [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] di Microsoft.  Per impostazione predefinita, il compilatore non invia alcuna informazione a Microsoft.  Se tuttavia si verifica un errore interno del compilatore, questa opzione consentirà di inviare un rapporto di errore a Microsoft.  Tali informazioni consentiranno al personale del supporto tecnico Microsoft di identificare la causa e di apportare eventuali migliorie alla versione successiva di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 La capacità di un utente di inviare report dipende dalle autorizzazioni relative ai criteri utente e del computer.  
  
 Nella tabella riportata di seguito viene fornito un riepilogo dei risultati ottenuti utilizzando l'opzione `/errorreport`.  
  
|||  
|-|-|  
|Opzione|Comportamento|  
|`prompt`|Se si verifica un errore interno del compilatore, verrà visualizzata una finestra di dialogo dove sono visualizzati i dati esatti raccolti dal compilatore.  È possibile determinare se vi sono informazioni riservate nel messaggio di errore e prendere una decisione relativa all'invio di queste informazioni a Microsoft.  Se si decide di inviarle e il computer e le impostazioni dei criteri utente lo consentono, il compilatore invierà i dati a Microsoft.|  
|`queue`|Accoda la segnalazione errori.  Quando si esegue l'accesso con privilegi di amministratore, è possibile segnalare gli eventuali errori che si sono verificati dall'ultimo accesso \(non verrà richiesto di inviare segnalazioni di errori più di una volta ogni tre giorni\).  Si tratta dell'impostazione predefinita quando non è specificata l'opzione `/errorreport`.|  
|`send`|Se si verifica un errore interno del compilatore e il computer e le impostazioni dei criteri utente lo consentono, il compilatore invierà i dati a Microsoft.<br /><br /> L'opzione `/errorReport:send` viene utilizzata per tentare di inviare automaticamente informazioni sull'errore a Microsoft.  Questa opzione dipende dal Registro di sistema.  Per ulteriori informazioni sull'impostazione dei valori appropriati nel Registro di sistema, vedere la pagina relativa alla [modalità di abilitazione della segnalazione degli errori automatica negli strumenti da riga di comando di Visual Studio 2008](http://go.microsoft.com/fwlink/?LinkID=184695).|  
|`none`|Se si verifica un errore interno del compilatore, non verrà raccolto né inviato a Microsoft.|  
  
 Il compilatore invia i dati che includono lo stack al momento dell'errore, che generalmente include parti di codice sorgente.  Se `/errorreport` viene utilizzata con l'opzione [\/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md), verrà inviato l'intero file di origine.  
  
 Questa opzione risulta particolarmente utile con l'opzione [\/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md) in quanto consente ai tecnici Microsoft di riprodurre l'errore più facilmente.  
  
> [!NOTE]
>  L'opzione `/errorreport` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Nel codice riportato di seguito si tenterà di compilare `T2.vb` e se si verifica un errore interno del compilatore verrà richiesto di inviare il messaggio di errore a Microsoft.  
  
```  
vbc /errorreport:prompt t2.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [\/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)