---
title: "Impossibile scrivere nel file di log. Verrebbe superato il valore MaximumSize | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrApplicationLog_FileExceedsMaximumSize"
ms.assetid: 61747a9c-e460-424b-a365-73cdba9dd428
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Impossibile scrivere nel file di log. Verrebbe superato il valore MaximumSize
La classe <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> non è riuscita a scrivere nel file di log perché:  
  
-   La dimensione del file di log \(in byte\) è maggiore rispetto al valore della proprietà <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.MaxFileSize%2A>  
  
     e  
  
-   Il valore della proprietà <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.DiskSpaceExhaustedBehavior%2A> è <xref:Microsoft.VisualBasic.Logging.DiskSpaceExhaustedOption>.  
  
### Per correggere l'errore  
  
1.  Archiviare i log esistenti e rimuoverli dal computer per consentire all'oggetto <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> di creare nuovi log.  
  
2.  Modificare il valore della proprietà <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.MaxFileSize%2A> per consentire log di dimensioni maggiori.  
  
3.  Impostare la proprietà <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.DiskSpaceExhaustedBehavior%2A> su <xref:Microsoft.VisualBasic.Logging.DiskSpaceExhaustedOption> per eliminare i messaggi senza avviso se il log è troppo grande.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.MaxFileSize%2A>   
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.DiskSpaceExhaustedBehavior%2A>   
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener>   
 [Oggetto My.Application.Log](../../visual-basic/language-reference/objects/my-application-log-object.md)   
 [My.Log Object](../../visual-basic/language-reference/objects/my-log-object.md)