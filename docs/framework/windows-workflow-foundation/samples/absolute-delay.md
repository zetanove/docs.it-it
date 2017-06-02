---
title: "Ritardo assoluto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b483139a-39bb-4560-8003-8969a8fc2cd1
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Ritardo assoluto
Lo scenario principale di questo esempio è ritardare un flusso di lavoro fino a una <xref:System.DateTime> specificata utilizzando timer durevoli in un'applicazione flusso di lavoro.Si tratta di uno scenario diverso rispetto all'utilizzo dell'attività <xref:System.Activities.Statements.Delay> incorporata in quanto in questo caso sarà possibile ritardare un flusso di lavoro solo per un determinato <xref:Sysem.TimeSpan> \(o numero di minuti\/secondi\).  
  
 Di seguito sono elencati alcuni scenari reali nei quali potrebbe essere necessario fare questa distinzione:  
  
1.  Si desidera ritardare di 30 secondi l'invio di un messaggio di posta elettronica per verificare che non contenga errori.  
  
2.  In caso di straordinari sul lavoro, si desidera ritardare l'invio di tutti i messaggi di posta elettronica fino al normale orario di lavoro \(ad esempio 8 del mattino\).  
  
## Dimostrazione  
  
1.  <xref:System.Activities.Statements.DurableTimerExtension> per l'implementazione del ritardo assoluto  
  
2.  Configurazione della persistenza utilizzando <xref:System.Activities.WorkflowApplication> per timer durevoli  
  
3.  Utilizzo di <xref:System.Activities.NativeActivity%601> per i punti di estensibilità  
  
4.  Utilizzo di <xref:System.Activities.CodeActivity%601> nell'attività SendEmail.  
  
5.  <xref:System.Activities.Statements.Delay>  
  
6.  Flusso di lavoro solo XAML  
  
 Questo esempio dimostra come creare un'attività personalizzata che accetta una <xref:System.DateTime> e utilizza timer durevoli per registrare la durata del ritardo.In caso di utilizzo di timer durevoli, è necessario utilizzare un'attività <xref:System.Activities.NativeActivity> per creare un segnalibro, in quanto è necessario registrare questo segnalibro con l'estensione del timer.In questo esempio, quando il timer durevole scade, viene chiamato il metodo `OnTimerExpired`.Verificare che l'estensione del timer venga aggiunta all'evento <xref:System.Activities.NativeActivity%601.CacheMetadata%2A> per garantire che venga fornito il runtime con queste informazioni.Come unico altro dettaglio di implementazione, sarà necessario implementare la logica per la conversione da <xref:System.DateTime> a <xref:Sysem.TimeSpan>, in quanto i timer durevoli accettano solo <xref:System.DateTime>.Notare la piccola perdita di precisione.  
  
> [!NOTE]
>  La conversione da <xref:System.DateTime> a <xref:Sysem.TimeSpan> determina una minima perdita di precisione.  
  
 Questo esempio dimostra inoltre come attivare la persistenza per una <xref:System.Activities.WorkflowApplication>.Per questo particolare esempio, verranno utilizzati timer durevoli in cui i dati del flusso di lavoro verranno scaricati nel database di persistenza durante il tempo di inattività in attesa della scadenza del timer.Questa implementazione può essere utilizzata anche per altre azioni di persistenza.Questo esempio mostra come configurare la stringa di connessione della persistenza con SQL Server e come creare l'archivio di istanze per rendere persistenti i dati delle istanze del flusso di lavoro.Viene fornita la logica per riprendere il flusso di lavoro una volta generato un evento che rende eseguibile l'istanza del flusso di lavoro.  
  
 Nel corso di questo esempio verrà mostrato il momento di inizio e fine del ritardo incorporato, che a sua volta determina l'invio di un messaggio di posta elettronica.A questo punto, l'attività AbsoluteDelay verrà interrotta fino a una determinata <xref:System.DateTime> \(o 0 secondi se <xref:System.DateTime> è scaduta\), che a sua volta invierà un messaggio di posta elettronica alla scadenza.In questo modo verranno mostrati i due diversi casi di utilizzo della funzionalità <xref:System.Activities.Statements.Delay> incorporata rispetto all'utilizzo di un'attività AbsoluteDelay.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare che sul computer sia installato SQL Server Express \(o versione successiva\).  
  
2.  Eseguire setup.cmd \(da WF\/Basic\/Services\/AbsoluteDelay\/CS\) in un prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] per creare il database AbsoluteDelaySampleDB, lo schema di persistenza e la logica di persistenza.  
  
3.  Aprire la soluzione in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
4.  Specificare Duration nell'attività Delay.  
  
5.  Specificare ExpirationTime nell'attività AbsoluteDelay.  
  
6.  Aggiornare i campi SendMailTo, SendMailFrom, SendMailSubject, SendMailBody e SmtpHost nell'attività SendMail.  
  
    > [!NOTE]
    >  Se non si specifica un host SMTP valido, l'applicazione genera un'eccezione SMTP.  
  
7.  Compilare la soluzione scegliendo **Compila soluzione** dal menu **Compila**.  
  
8.  Eseguire la soluzione premendo **F5**.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Services\AbsoluteDelay`