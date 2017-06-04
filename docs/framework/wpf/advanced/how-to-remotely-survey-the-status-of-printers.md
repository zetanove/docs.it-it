---
title: "Procedura: verificare lo stato delle stampanti da postazione remota | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "stato stampante, verifica da postazione remota"
  - "verificare dello stato delle stampanti da postazione remota"
  - "STATO, stampanti, verifica da postazione remota"
  - "verifica dello stato delle stampanti da postazione remota"
ms.assetid: d6324759-8292-4c23-9584-9c708887dc94
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: verificare lo stato delle stampanti da postazione remota
Nelle aziende di medie e grandi dimensioni può verificarsi in qualsiasi momento l'arresto di più stampanti a causa di fogli bloccati o di carta esaurita o di qualche altro imprevisto.  La vasta gamma di proprietà delle stampanti esposta nelle [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] di [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] consente la rapida verifica dello stato delle stampanti.  
  
## Esempio  
 Di seguito vengono descritti i passaggi principali per la creazione di questo tipo di utilità.  
  
1.  Ottenere un elenco di tutti i server di stampa.  
  
2.  Scorrere i server per eseguire una query sulle relative code di stampa.  
  
3.  In ogni passaggio del ciclo del server, scorrere tutte le code del server e leggere ciascuna proprietà che consenta di identificare la coda che non è in funzione.  
  
 Il codice riportato di seguito è costituito da una serie di frammenti.  Per semplicità, nell'esempio si presuppone l'esistenza di un elenco di server di stampa delimitato da CRLF.  La variabile `fileOfPrintServers` è un oggetto <xref:System.IO.StreamReader> per questo file.  Poiché il nome di ciascun server si trova su una riga distinta, qualsiasi chiamata a <xref:System.IO.StreamReader.ReadLine%2A> ottiene il nome del server successivo e determina lo spostamento del cursore di <xref:System.IO.StreamReader> all'inizio della riga successiva.  
  
 Nel ciclo esterno, il codice crea un oggetto <xref:System.Printing.PrintServer> per l'ultimo server di stampa e specifica che l'applicazione deve disporre di diritti di amministrazione sul server.  
  
> [!NOTE]
>  Se i server sono numerosi, è possibile migliorare le prestazioni utilizzando i costruttori [PrintServer\(String, String\<xref:System.Printing.PrintServer.%23ctor%28System.String%2CSystem.String%5B%5D%2CSystem.Printing.PrintSystemDesiredAccess%29> che consentono di inizializzare soltanto le proprietà che saranno necessarie.  
  
 Nell'esempio viene quindi utilizzato <xref:System.Printing.PrintServer.GetPrintQueues%2A> per creare una raccolta di tutte le code del server e iniziare a scorrerle.  Il ciclo interno include una struttura con diramazioni, corrispondente alle due modalità di verifica dello stato di una stampante:  
  
-   È possibile leggere i flag della proprietà <xref:System.Printing.PrintQueue.QueueStatus%2A> di tipo <xref:System.Printing.PrintQueueStatus>.  
  
-   È possibile leggere tutte le proprietà rilevanti, ad esempio <xref:System.Printing.PrintQueue.IsOutOfPaper%2A> e <xref:System.Printing.PrintQueue.IsPaperJammed%2A>.  
  
 Nell'esempio vengono illustrati entrambi i metodi. All'utente è stato pertanto richiesto di scegliere il metodo da utilizzare e di rispondere con "y" per utilizzare i flag della proprietà <xref:System.Printing.PrintQueue.QueueStatus%2A>.  Per informazioni dettagliate relative ai due metodi vedere di seguito.  
  
 I risultati vengono infine presentati all'utente.  
  
 [!code-cpp[PrinterStatusSurvey#SurveyQueues](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#surveyqueues)]
 [!code-csharp[PrinterStatusSurvey#SurveyQueues](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#surveyqueues)]
 [!code-vb[PrinterStatusSurvey#SurveyQueues](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#surveyqueues)]  
  
 Per controllare lo stato delle stampanti utilizzando i flag della proprietà <xref:System.Printing.PrintQueue.QueueStatus%2A>, esaminare ogni flag pertinente per verificare se è impostato.  La modalità standard per verificare se in un set di flag di bit è stato impostato un determinato bit consiste nell'eseguire un'operazione di AND logico in cui un operando sia costituito dal set di flag e l'altro dal flag stesso.  Dal momento che il flag stesso dispone di un solo bit impostato, il risultato dell'operazione di AND logico consisterà, al più, nell'impostazione dello stesso bit.  Per verificare se il bit è impostato, confrontare il risultato dell'operazione di AND logico con il flag stesso.  Per ulteriori informazioni, vedere <xref:System.Printing.PrintQueueStatus>, [Operatore & \(Riferimenti per C\#\)](../Topic/&%20Operator%20\(C%23%20Reference\).md) e <xref:System.FlagsAttribute>.  
  
 Per ciascun attributo in cui il bit è impostato, il codice aggiunge un avviso al report finale che sarà inviato all'utente.  Il metodo **ReportAvailabilityAtThisTime** chiamato alla fine del codice viene illustrato di seguito.  
  
 [!code-cpp[PrinterStatusSurvey#SpotTroubleUsingQueueAttributes](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#spottroubleusingqueueattributes)]
 [!code-csharp[PrinterStatusSurvey#SpotTroubleUsingQueueAttributes](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#spottroubleusingqueueattributes)]
 [!code-vb[PrinterStatusSurvey#SpotTroubleUsingQueueAttributes](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#spottroubleusingqueueattributes)]  
  
 Per controllare lo stato delle stampanti utilizzando tutte le proprietà, leggere ciascuna proprietà e aggiungere una nota al report finale che sarà presentato all'utente se tale proprietà è `true`.  Il metodo **ReportAvailabilityAtThisTime** chiamato alla fine del codice viene illustrato di seguito.  
  
 [!code-cpp[PrinterStatusSurvey#SpotTroubleUsingQueueProperties](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#spottroubleusingqueueproperties)]
 [!code-csharp[PrinterStatusSurvey#SpotTroubleUsingQueueProperties](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#spottroubleusingqueueproperties)]
 [!code-vb[PrinterStatusSurvey#SpotTroubleUsingQueueProperties](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#spottroubleusingqueueproperties)]  
  
 Il metodo **ReportAvailabilityAtThisTime** è stato creato per i casi in cui è necessario determinare la disponibilità della coda all'ora corrente.  
  
 Il metodo non eseguirà alcuna operazione se le proprietà <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> e <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> coincidono, perché in tal caso la stampante sarà sempre disponibile.  Se non coincidono, il metodo ottiene l'ora corrente, che deve quindi essere convertita nel conteggio dei minuti complessivi trascorsi dalla mezzanotte, poiché le proprietà <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> e <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> sono oggetti <xref:System.Int32> che rappresentano i minuti trascorsi dalla mezzanotte e non oggetti <xref:System.DateTime>.  Infine, il metodo verifica se l'ora corrente è compresa tra l'ora di inizio e l'ora di fine.  
  
 [!code-cpp[PrinterStatusSurvey#UsingStartAndUntilTimes](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#usingstartanduntiltimes)]
 [!code-csharp[PrinterStatusSurvey#UsingStartAndUntilTimes](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#usingstartanduntiltimes)]
 [!code-vb[PrinterStatusSurvey#UsingStartAndUntilTimes](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#usingstartanduntiltimes)]  
  
## Vedere anche  
 <xref:System.Printing.PrintQueue.StartTimeOfDay%2A>   
 <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A>   
 <xref:System.DateTime>   
 <xref:System.Printing.PrintQueueStatus>   
 <xref:System.FlagsAttribute>   
 <xref:System.Printing.PrintServer.GetPrintQueues%2A>   
 <xref:System.Printing.PrintServer>   
 <xref:System.Printing.LocalPrintServer>   
 <xref:System.Printing.EnumeratedPrintQueueTypes>   
 <xref:System.Printing.PrintQueue>   
 [Operatore & \(Riferimenti per C\#\)](../Topic/&%20Operator%20\(C%23%20Reference\).md)   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)