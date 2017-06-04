---
title: "Procedura: specificare le credenziali del client per una richiesta del servizio dati (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, personalizzazione delle richieste"
ms.assetid: 1632f9af-e45f-4363-9222-03823daa8e28
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: specificare le credenziali del client per una richiesta del servizio dati (WCF Data Services)
Per impostazione predefinita, la libreria client non fornisce le credenziali quando viene inviata una richiesta a un servizio [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Tuttavia, è possibile specificare che le credenziali vengano inviate per autenticare richieste al servizio dati fornendo un elemento <xref:System.Net.NetworkCredential> per la proprietà <xref:System.Data.Services.Client.DataServiceContext.Credentials%2A> di <xref:System.Data.Services.Client.DataServiceContext>.  Per altre informazioni, vedere [Protezione di WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md).  Nell'esempio in questo argomento viene illustrato come fornire in modo esplicito le credenziali che vengono usate dal client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per richiedere i dati dal servizio dati.  
  
 Nell'esempio riportato in questo argomento vengono usati il servizio dati Northwind di esempio e le classi del servizio dati client generate automaticamente.  Questo servizio e le classi di dati client vengono creati al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  È anche possibile usare il [servizio dati di esempio di Northwind](http://go.microsoft.com/fwlink/?LinkId=187426) pubblicato sul sito Web [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]. Questo servizio dati di esempio è di sola lettura e viene restituito un errore se si tenta di salvare le modifiche.  I servizi dati di esempio del sito Web [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] permettono l'autenticazione anonima.  
  
## Esempio  
 L'esempio seguente è tratto dalla pagina code\-behind per un file XAML \(Extensible Application Markup Language\) che costituisce la pagina principale dell'applicazione Windows Presentation Framework.  In questo esempio viene visualizzata un'istanza di `LoginWindow` per raccogliere le credenziali di autenticazione dall'utente e usare quindi queste credenziali per una richiesta al servizio dati.  
  
  
  
## Esempio  
 Tramite il codice XAML seguente viene definita la pagina principale dell'applicazione WPF.  
  
  
  
## Esempio  
 L'esempio seguente è tratto dalla pagina code\-behind per la finestra usata per raccogliere le credenziali di autenticazione dall'utente prima di effettuare una richiesta al servizio dati.  
  
  
  
## Esempio  
 Il codice XAML seguente definisce l'accesso dell'applicazione WPF.  
  
  
  
## Sicurezza di .NET Framework  
 Le considerazioni sulla sicurezza riportate di seguito si applicano all'esempio di questo argomento:  
  
-   Per verificare le credenziali fornite in questo esempio, il servizio dati Northwind deve usare uno schema di autenticazione diverso dall'accesso anonimo.  In caso contrario, il sito Web che ospita il servizio dati non richiederà le credenziali.  
  
-   Le credenziali utente devono essere richieste solo durante l'esecuzione e non devono essere memorizzate nella cache.  Le credenziali devono essere archiviate sempre in modo protetto.  
  
-   I dati inviati con l'autenticazione di base o digest non sono crittografati, pertanto possono essere visti da un avversario.  Le credenziali di autenticazione di base \(nome utente e password\) inoltre vengono inviate in testo non crittografato e possono essere intercettate.  
  
 Per altre informazioni, vedere [Protezione di WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md).  
  
## Vedere anche  
 [Protezione di WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)   
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)