---
title: "Procedura: registrare messaggi all&#39;avvio o all&#39;arresto dell&#39;applicazione (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "log eventi, arresto"
  - "oggetto My.Application.Log, registrazione"
  - "Startup (evento)"
  - "log eventi, avvio"
  - "Shutdown (evento)"
  - "oggetto My.Log, registrazione"
ms.assetid: 67624d05-cddf-48b7-8c36-5c99baa4c621
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Procedura: registrare messaggi all&#39;avvio o all&#39;arresto dell&#39;applicazione (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile usare gli oggetti `My.Application.Log` e `My.Log` per registrare informazioni sugli eventi che si verificano nell'applicazione. Questo esempio illustra come usare il metodo `My.Application.Log.WriteEntry` con gli eventi `Startup` e `Shutdown` per scrivere informazioni di traccia.  
  
### Per accedere al codice del gestore eventi dell'applicazione  
  
1.  Selezionare un progetto in **Esplora soluzioni**. Scegliere **Proprietà** dal menu **Progetto**.  
  
2.  Fare clic sulla scheda **Applicazione**.  
  
3.  Fare clic sul pulsante **Visualizza eventi applicazione** per aprire l'editor di codice.  
  
     Verrà aperto il file ApplicationEvents.vb.  
  
### Per registrare messaggi all'avvio dell'applicazione  
  
1.  Aprire il file ApplicationEvents.vb nell'editor di codice. Scegliere **Eventi MyApplication** dal menu **Generale**.  
  
2.  Scegliere **Avvio** dal menu **Dichiarazioni**.  
  
     L'applicazione genera l'evento <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> prima dell'esecuzione dell'applicazione principale.  
  
3.  Aggiungere il metodo `My.Application.Log.WriteEntry` al gestore eventi `Startup`.  
  
     [!code-vb[VbVbalrMyApplicationLog#1](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/how-to-log-messages-when-the-application-starts-or-shuts-down_1.vb)]  
  
### Per registrare messaggi all'arresto dell'applicazione  
  
1.  Aprire il file ApplicationEvents.vb nell'editor di codice. Scegliere **Eventi MyApplication** dal menu **Generale**.  
  
2.  Scegliere **Arresto** dal menu **Dichiarazioni**.  
  
     L'applicazione genera l'evento <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown> dopo l'esecuzione dell'applicazione principale, ma prima dell'arresto.  
  
3.  Aggiungere il metodo `My.Application.Log.WriteEntry` al gestore eventi `Shutdown`.  
  
     [!code-vb[VbVbalrMyApplicationLog#2](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/how-to-log-messages-when-the-application-starts-or-shuts-down_2.vb)]  
  
## Esempio  
 Per accedere agli eventi dell'applicazione nell'editor del codice è possibile usare **Creazione progetti**. Per altre informazioni, vedere [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic).  
  
 [!code-vb[VbVbalrMyApplicationLog#3](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/how-to-log-messages-when-the-application-starts-or-shuts-down_3.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>   
 <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>   
 [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)   
 [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)