---
title: Ottimizzazione dell&quot;applicazione Async (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 4c3e7997-a95f-4fbe-a6ac-60ba042d30b9
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 7d0cac2fe7305031b93a375a08e785285a291320
ms.lasthandoff: 03/13/2017

---
# <a name="fine-tuning-your-async-application-visual-basic"></a>Ottimizzazione dell'applicazione Async (Visual Basic)
È possibile aggiungere precisione e flessibilità alle applicazioni asincrone utilizzando i metodi e proprietà che la <xref:System.Threading.Tasks.Task>tipo rende disponibile.</xref:System.Threading.Tasks.Task> Negli argomenti di questa sezione mostrano esempi che utilizzano <xref:System.Threading.CancellationToken>e importante `Task` metodi quali <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>e <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName>.</xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName> </xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> </xref:System.Threading.CancellationToken>  
  
 Utilizzando `WhenAny` e `WhenAll`, è possibile avviare più attività e attendere il completamento da una singola attività di monitoraggio più facilmente.  
  
-   `WhenAny`Restituisce un'attività che viene completata quando un'attività in una raccolta è stata completata.  
  
     Per esempi che utilizzano `WhenAny`, vedere [annullare attività asincrone rimanenti dopo una completa (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md)e [avviare più attività asincrone e processo li come essi completa (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md).  
  
-   `WhenAll`Restituisce un'attività che viene completata quando sono state completate tutte le attività in una raccolta.  
  
     Per ulteriori informazioni e un esempio che utilizza `WhenAll`, vedere [procedura: estendere la Async Walkthrough da tramite Task. whenall (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md).  
  
 In questa sezione sono inclusi gli esempi seguenti.  
  
-   [Annullare un'attività asincrona o un elenco di attività (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-an-async-task-or-a-list-of-tasks.md).  
  
-   [Annullare attività asincrone dopo un periodo di tempo (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-async-tasks-after-a-period-of-time.md)  
  
-   [Annullare le attività asincrone rimanenti dopo che ne è completa (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md)  
  
-   [Avviare più attività asincrone ed elaborarle quando vengono completate (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md)  
  
> [!NOTE]
>  Per eseguire gli esempi, è necessario disporre di Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versioni successive installato nel computer in uso.  
  
 I progetti di creare un'interfaccia utente che contiene un pulsante che avvia il processo e un pulsante che consente di annullare, come mostrato nell'immagine seguente. I pulsanti sono denominati `startButton` e `cancelButton`.  
  
 ![Finestra WPF con pulsante Annulla](../../../../csharp/programming-guide/concepts/async/media/cancellation.png "annullamento")  
  
 È possibile scaricare i progetti Windows Presentation Foundation (WPF) completa da [esempio asincrono: Fine ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046).  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)
