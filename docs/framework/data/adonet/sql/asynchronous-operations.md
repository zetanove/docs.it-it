---
title: "Operazioni asincrone | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Operazioni asincrone
Il completamento di alcune operazioni di database, ad esempio l'esecuzione di comandi, può richiedere parecchio tempo.  In questi casi, le applicazioni a thread singolo devono bloccare altre operazioni e attendere il comando per il completamento prima di continuare le rispettive operazioni.  Al contrario, la possibilità di assegnare l'operazione a esecuzione prolungata a un thread in background consente al thread in primo piano di restare attivo per l'intera durata dell'operazione.  In un'applicazione Windows, ad esempio, la delega dell'operazione a esecuzione prolungata a un thread in background consente al thread dell'interfaccia utente di rimanere attivo mentre l'operazione è in esecuzione.  
  
 .NET Framework fornisce diversi modelli di progettazione asincroni standard che gli sviluppatori possono usare per sfruttare i thread in background e liberare i thread dell'interfaccia utente o i thread ad alta priorità e usarli per completare altre operazioni.  ADO.NET supporta questi modelli di progettazione nella propria classe <xref:System.Data.SqlClient.SqlCommand>.  In particolare, i metodi <xref:System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:System.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> e <xref:System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A>, abbinati ai metodi <xref:System.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>, <xref:System.Data.SqlClient.SqlCommand.EndExecuteReader%2A> e <xref:System.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A>, forniscono il supporto asincrono.  
  
> [!NOTE]
>  La programmazione asincrona è una funzionalità centrale di .NET Framework e ADO.NET sfrutta pienamente i modelli di progettazione standard.  Per altre informazioni sulle diverse tecniche asincrone disponibili per gli sviluppatori, vedere [Calling Synchronous Methods Asynchronously](../../../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md).  
  
 Benché l'uso di tecniche asincrone con le funzionalità ADO.NET non comporti ulteriori considerazioni, è probabile che gli sviluppatori utilizzeranno le funzionalità asincrone più in ADO.NET che in altre aree di .NET Framework.  Quando si creano applicazioni multithreading è importante essere a conoscenza sia dei vantaggi che dei potenziali problemi.  Negli esempi seguenti vengono illustrate diverse problematiche importanti di cui gli sviluppatori dovranno tenere conto quando compilano applicazioni che incorporano funzionalità multithreading.  
  
## In questa sezione  
 [Applicazioni Windows che utilizzano callback](../../../../../docs/framework/data/adonet/sql/windows-applications-using-callbacks.md)  
 Viene fornito un esempio che illustra come eseguire un comando asincrono in modo sicuro, gestendo in modo corretto l'interazione con un form e il relativo contenuto in un thread separato.  
  
 [Applicazioni ASP.NET che utilizzano handle di attesa](../../../../../docs/framework/data/adonet/sql/aspnet-apps-using-wait-handles.md)  
 Viene fornito un esempio che illustra come eseguire più comandi simultanei da una pagina ASP.NET, usando handle di attesa per gestire l'operazione al completamento di tutti i comandi.  
  
 [Utilizzo del polling nelle applicazioni console](../../../../../docs/framework/data/adonet/sql/polling-in-console-applications.md)  
 Viene fornito un esempio che illustra l'uso del polling per attendere il completamento dell'esecuzione di un comando asincrono da un'applicazione console.  Questa tecnica è valida anche in una libreria di classi o in altre applicazioni senza interfaccia utente.  
  
## Vedere anche  
 [SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [Calling Synchronous Methods Asynchronously](../../../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)