---
title: "Resume without error | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID20"
dev_langs: 
  - "VB"
ms.assetid: f9631804-fd36-4443-b36c-30db827e6176
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Resume without error
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È stata rilevata un'istruzione `Resume` all'esterno del codice di gestione degli errori o il codice è passato in un gestore degli errori anche se non si è verificato alcun errore.  
  
### Per correggere l'errore  
  
1.  Spostare l'istruzione `Resume`in un gestore errori o eliminarla.  
  
2.  I salti a etichette non sono consentiti tra routine, quindi è necessario cercare nella routine l'etichetta che identifica il gestore errori.  Se viene trovata un'etichetta duplicata specificata come destinazione di un'istruzione `GoTo` che non corrisponde a un'istruzione `On Error GoTo`, cambiare l'etichetta della riga in modo che corrisponda alla destinazione prevista.  
  
## Vedere anche  
 [Resume Statement](../../../visual-basic/language-reference/statements/resume-statement.md)   
 [On Error Statement](../../../visual-basic/language-reference/statements/on-error-statement.md)