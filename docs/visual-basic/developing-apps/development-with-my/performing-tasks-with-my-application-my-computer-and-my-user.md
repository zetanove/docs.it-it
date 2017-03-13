---
title: "Performing Tasks with My.Application, My.Computer, and My.User (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Application object, developing applications"
  - "rapid application development (RAD), My.Application"
  - "rapid application development (RAD), My.Computer"
  - "rapid application development (RAD), My.User"
  - "My.Computer object, developing applications"
  - "My.User object, developing applications"
ms.assetid: c8af61bd-4dd3-4a0f-9af5-795b594b240b
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# Performing Tasks with My.Application, My.Computer, and My.User (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

I tre oggetti `My` principali che consentono di accedere alle informazioni e alle funzionalità più comuni sono `My.Application` \(<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>\), `My.Computer` \(<xref:Microsoft.VisualBasic.Devices.Computer>\) e `My.User` \(<xref:Microsoft.VisualBasic.ApplicationServices.User>\).  È possibile utilizzare questi oggetti per accedere alle informazioni correlate rispettivamente all'applicazione corrente, al computer sul quale è installata l'applicazione o all'utente corrente dell'applicazione.  
  
## Oggetti My.Application, My.Computer e My.User  
 Negli esempi riportati di seguito viene illustrata la modalità con cui è possibile recuperare le informazioni mediante l'oggetto `My`.  
  
 [!code-vb[VbVbcnMy#1](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/performing-tasks-with-my-application-my-computer-and-my-user_1.vb)]  
  
 [!code-vb[VbVbcnMy#2](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/performing-tasks-with-my-application-my-computer-and-my-user_2.vb)]  
  
 Oltre al recupero delle informazioni, i membri esposti attraverso questi tre oggetti consentono anche l'esecuzione dei metodi correlati a quell'oggetto.  È possibile, ad esempio, accedere a diversi metodi per modificare file o aggiornare il Registro di sistema mediante l'oggetto `My.Computer`.  
  
 L'I\/O dei file è significativamente più semplice e più veloce con l'oggetto `My`, che include diversi metodi e proprietà per modificare file, directory e unità.  L'oggetto <xref:Microsoft.VisualBasic.FileIO.TextFieldParser> consente la lettura da file con struttura di grandi dimensioni che presentano campi delimitati o a larghezza fissa.  Nell'esempio viene aperto il `TextFieldParser` `reader` e quindi utilizzato per leggere da `C:\TestFolder1\test1.txt`.  
  
 [!code-vb[VbVbalrTextFieldParser#23](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/performing-tasks-with-my-application-my-computer-and-my-user_3.vb)]  
  
 L'oggetto `My.Application` consente di modificare le impostazioni cultura per l'applicazione.  Nell'esempio riportato di seguito viene illustrata la modalità con la quale è possibile chiamare questo metodo.  
  
 [!code-vb[VbVbcnMy#3](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/performing-tasks-with-my-application-my-computer-and-my-user_4.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.ApplicationServices.User>   
 [How My Depends on Project Type](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)