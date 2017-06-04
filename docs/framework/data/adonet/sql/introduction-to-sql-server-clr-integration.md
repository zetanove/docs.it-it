---
title: "Introduzione all&#39;integrazione CLR di SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 551d2290-ed80-49be-b377-44b32444da1c
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Introduzione all&#39;integrazione CLR di SQL Server
Common Language Runtime \(CLR\) rappresenta l'elemento essenziale di Microsoft .NET Framework e fornisce l'ambiente di esecuzione per tutto il codice .NET Framework.  Il codice eseguito all'interno di CLR viene definito codice gestito.  CLR fornisce diverse funzioni e vari servizi richiesti per l'esecuzione del programma, che includono la compilazione JIT \(Just\-In\-Time\), l'allocazione e la gestione della memoria, l'applicazione dell'indipendenza dai tipi, la gestione delle eccezioni e dei thread e la sicurezza.  
  
 Con CLR incluso in Microsoft SQL Server \(integrazione di CLR\), è possibile creare nuove stored procedure, trigger, funzioni definite dall'utente e aggregati definiti dall'utente nel codice gestito.  Poiché il codice gestito viene processato con il codice nativo prima dell'esecuzione, in determinati scenari è possibile ottenere significativi aumenti di prestazioni.  
  
 Il codice gestito usa la sicurezza dall'accesso di codice \(CAS, Code Access Security\), i collegamenti del codice e i domini dell'applicazione per impedire alle assembly di eseguire determinate operazioni.  In SQL Server viene usato CAS per proteggere il codice gestito e per impedire il danneggiamento del sistema operativo o del server di database.  
  
 In questa sezione vengono fornite solo le informazioni di base per iniziare a programmare con l'integrazione CLR di SQL Server. Tali informazioni non sono da considerarsi esaustive.  Per informazioni più dettagliate, vedere la versione della documentazione online di SQL Server corrispondente alla versione di SQL Server in uso.  
  
 **Documentazione online di SQL Server**  
  
-   [Panoramica dell'integrazione con CLR \(Common Language Runtime\)](http://go.microsoft.com/fwlink/?LinkId=115242)  
  
## Abilitazione dell'integrazione con CLR  
 In Microsoft SQL Server la funzione di integrazione CLR \(Common Language Runtime\) è disattivata per impostazione predefinita e deve essere abilitata in modo da usare oggetti implementati mediante l'integrazione CLR.  Per abilitare l'integrazione CLR mediante Transact\-SQL, usare l'opzione `clr enabled` della stored procedure `sp_configure`, come illustrato di seguito:  
  
```  
sp_configure 'clr enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
 È possibile disabilitare l'integrazione CLR impostando l'opzione `clr enabled` su 0.  Quando si disabilita l'integrazione CLR, SQL Server non esegue più le routine CLR e scarica tutti i domini dell'applicazione.  
  
 Per informazioni più dettagliate, vedere la versione della documentazione online di SQL Server corrispondente alla versione di SQL Server in uso.  
  
 **Documentazione online di SQL Server**  
  
-   [Abilitazione dell'integrazione con CLR](http://go.microsoft.com/fwlink/?LinkId=115230)  
  
## Distribuzione di un assembly CLR  
 Dopo che i metodi CLR sono stati testati e verificati nel server di prova, possono essere distribuiti nei server di produzione usando uno script di distribuzione.  Lo script di distribuzione può essere generato manualmente o tramite SQL Server Management Studio.  Per informazioni più dettagliate, vedere la versione della documentazione online di SQL Server corrispondente alla versione di SQL Server in uso.  
  
 **Documentazione online di SQL Server**  
  
1.  [Distribuzione di oggetti di database CLR](http://go.microsoft.com/fwlink/?LinkId=115232)  
  
## Sicurezza dell'integrazione con CLR  
 Il modello di sicurezza dell'integrazione di Microsoft SQL Server con CLR \(Common Language Runtime\) di Microsoft .NET Framework consente di gestire e di proteggere l'accesso tra diversi tipi di oggetti CLR e non CLR in esecuzione in SQL Server.  Questi oggetti possono essere chiamati da un'istruzione Transact\-SQL o da un altro oggetto CLR in esecuzione sul server.  
  
 Per informazioni più dettagliate, vedere la versione della documentazione online di SQL Server corrispondente alla versione di SQL Server in uso.  
  
 **Documentazione online di SQL Server**  
  
-   [Protezione per l'integrazione con CLR](http://go.microsoft.com/fwlink/?LinkId=115234)  
  
## Debug di un assembly CLR  
 Microsoft SQL Server fornisce il supporto per il debug di oggetti Transact\-SQL e CLR \(Common Language Runtime\) nel database.  Il debug può essere eseguito in entrambi i linguaggi, ovvero gli utenti possono passare agevolmente da oggetti Transact\-SQL a oggetti CLR e viceversa.  
  
 Per informazioni più dettagliate, vedere la versione della documentazione online di SQL Server corrispondente alla versione di SQL Server in uso.  
  
 **Documentazione online di SQL Server**  
  
-   [Debug di oggetti di database CLR](http://go.microsoft.com/fwlink/?LinkId=115236)  
  
## Vedere anche  
 [Creating SQL Server 2005 Objects In Managed Code](http://msdn.microsoft.com/it-it/5358a825-e19b-49aa-8214-674ce5fed1da)   
 [Sicurezza dall'accesso di codice e ADO.NET](../../../../../docs/framework/data/adonet/code-access-security.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)