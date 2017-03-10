---
title: "End Statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.End"
  - "End"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "execution, ending"
  - "files, closing"
  - "End keyword, End statements"
  - "programs, quitting"
  - "code, exiting"
  - "program termination"
  - "End statement"
  - "execution, stopping"
ms.assetid: 0e64467c-0f34-4aab-9ddd-43f8b9d55d90
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# End Statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di interrompere immediatamente l'esecuzione.  
  
## Sintassi  
  
```  
End  
```  
  
## Note  
 È possibile posizionare ovunque l'istruzione `End` in una procedura per imporre l'intera applicazione per l'arresto dell'esecuzione.  `End` chiude qualsiasi file aperto con un'istruzione `Open` e cancella tutte la variabili di applicazione.  L'applicazione viene chiusa non appena nessuna parte del codice è in esecuzione e quando cessano di essere attivi tutti i riferimenti di altri programmi agli oggetti dell'applicazione.  
  
> [!NOTE]
>  L'istruzione `End` determina l'immediata interruzione dell'esecuzione del codice, senza richiamare il metodo `Dispose` o `Finalize` o altro codice Visual Basic.  e l'annullamento dei riferimenti a oggetti eventualmente attivati da altri programmi.  Se viene rilevata un'istruzione `End` in un blocco `Try` o `Catch`, il controllo non viene passato al blocco corrispondente `Finally`.  
  
 L'istruzione `Stop` sospende l'esecuzione ma, diversamente da `End`, non chiude file né cancella variabili, a meno che non venga rilevata in un file eseguibile \(EXE\) compilato.  
  
 Poiché l'istruzione `End` termina l'applicazione senza tenere conto di eventuali risorse ancora aperte, è consigliabile chiudere correttamente l'applicazione prima di utilizzarla.  Se, ad esempio, l'applicazione presenta form aperti, è necessario chiuderli prima che venga raggiunta l'istruzione `End`.  
  
 È consigliabile utilizzare l'istruzione `End` sporadicamente e solo quando è necessaria un'interruzione immediata.  Le normali operazioni per interrompere una routine \([Return Statement](../../../visual-basic/language-reference/statements/return-statement.md) and [Exit Statement](../../../visual-basic/language-reference/statements/exit-statement.md)\) non solo consentono di chiudere correttamente la routine, ma forniscono la stessa possibilità anche al codice chiamante.  Un'applicazione console, ad esempio, può uscire tramite `Return` dalla routine `Main`.  
  
> [!IMPORTANT]
>  L'istruzione `End` chiama il metodo <xref:System.Environment.Exit%2A> della classe <xref:System.Environment> nello spazio dei nomi <xref:System>.  <xref:System.Environment.Exit%2A> richiede che si disponga di autorizzazione `UnmanagedCode`.  Se tale autorizzazione non è disponibile, verrà generato un errore <xref:System.Security.SecurityException>.  
  
 Con l'ausilio di una parola chiave supplementare, [End \<keyword\> Statement](../../../visual-basic/language-reference/statements/end-keyword-statement.md) consente di stabilire la fine della definizione della routine o del blocco richiesto.  L'istruzione `End Function`, ad esempio, consente di terminare la definizione della routine `Function`.  
  
## Esempio  
 Nell'esempio seguente viene utilizzata l'istruzione `End` per terminare l'esecuzione del codice se l'utente lo richiede.  
  
 [!code-vb[VbVersHelp60Controls#64](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVersHelp60Controls/Form1.vb#64)]  
  
## Note per gli sviluppatori di applicazioni per Smart Device  
 Questa istruzione non è supportata.  
  
## Vedere anche  
 <xref:System.Security.Permissions.SecurityPermissionFlag>   
 [Stop Statement](../../../visual-basic/language-reference/statements/stop-statement.md)   
 [End \<keyword\> Statement](../../../visual-basic/language-reference/statements/end-keyword-statement.md)