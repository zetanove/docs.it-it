---
title: "Richiesta di dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "invio di dati"
  - "WebRequest (classe), invio e ricezione di dati"
  - "richiesta di dati da Internet, informazioni sulla richiesta di dati"
  - "WebClient (classe), invio e ricezione di dati"
  - "rete, richiesta di dati"
  - "ricezione di dati"
  - "invio di dati, informazioni sull'invio di dati"
  - "risposta a una richiesta Internet, informazioni sulla risposta a richieste Internet"
  - "richieste di dati"
  - "ricezione di dati, informazioni sulla ricezione di dati"
  - "Internet, richiesta di dati"
ms.assetid: df6f1e1d-6f2a-45dd-8141-4a85c3dafe1d
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Richiesta di dati
Sviluppo di applicazioni in esecuzione nell'ambiente operativo distribuito su Internet rende richiede un metodo efficace e facile da utilizzare per recuperare dati dalle risorse dei tipi.  I protocolli innestabili consentono di compilare le applicazioni che utilizzano una singola interfaccia per recuperare i dati dai protocolli più Internet.  
  
## Caricamento e download dei dati da un server Internet  
 Per le transazioni semplici di risposta e richiesta, la classe <xref:System.Net.WebClient> fornisce il metodo più semplice per caricare i dati o scaricare i dati da un server Internet.  **WebClient** fornisce metodi per caricare e scaricare file, inviare e i canali di raccolta e inviare un buffer di dati al server e la ricezione della risposta.  **WebClient** utilizza le classi <xref:System.Net.WebResponse> e <xref:System.Net.WebRequest> per rendere effettive le connessioni alle risorse Internet, in modo da qualsiasi protocollo innestabile registrato è disponibile per l'utilizzo.  
  
 Applicazioni client che devono eseguire i dati della richiesta più complessi di transazioni dai server utilizzando la classe **WebRequest** e dei relativi discendenti.  **WebRequest** incapsula i dettagli della connessione al server, di inviare la richiesta e di ottenere una risposta.  **WebRequest** è una classe astratta che definisce un set di proprietà e metodi disponibili per tutte le applicazioni che utilizzano i protocolli innestabili.  I discendenti **WebRequest**, come <xref:System.Net.HttpWebRequest>, implementano le proprietà e i metodi definiti da **WebRequest** in modo coerente con il protocollo sottostante.  
  
 La classe **WebRequest** crea istanze specifiche del protocollo dei discendenti **WebRequest**, utilizzando il valore dell'URI passato al metodo <xref:System.Net.WebRequest.Create%2A> per determinare l'istanza specifica della classe derivata da creare.  Le applicazioni indicano i discendenti **WebRequest** deve essere utilizzato per gestire una richiesta registrando il costruttore discendente con il metodo <xref:System.Net.WebRequest.RegisterPrefix%2A?displayProperty=fullName>.  
  
 Viene effettuata una richiesta alla risorsa Internet chiamando il metodo <xref:System.Net.WebRequest.GetResponse%2A> su **WebRequest**.  Il metodo **GetResponse** costruire la richiesta protocollo specifica le proprietà **WebRequest**, effettua la connessione socket di UDP o TCP al server e invia la richiesta.  Per le richieste che inviano dati al server, ad esempio le richieste HTTP **Post** o FTP **Put**, il metodo <xref:System.Net.WebRequest.GetRequestStream%2A?displayProperty=fullName> fornisce un flusso di rete in cui inviare dati.  
  
 Il metodo **GetResponse** restituisce **WebResponse** protocollo specifico che corrisponde **WebRequest.**  
  
 La classe **WebResponse** è una classe astratta che definisce le proprietà e i metodi disponibili per tutte le applicazioni che utilizzano i protocolli innestabili.  I discendenti di**WebResponse** implementano tali metodi e proprietà per il protocollo sottostante.  La classe <xref:System.Net.HttpWebResponse>, ad esempio, implementa la classe **WebResponse** per HTTP.  
  
 I dati restituiti dal server vengono visualizzati all'applicazione nel flusso restituito dal metodo <xref:System.Net.WebResponse.GetResponseStream%2A?displayProperty=fullName>.  È possibile utilizzare questo flusso come qualsiasi altro, come illustrato nell'esempio seguente.  
  
```csharp  
StreamReader sr =  
   new StreamReader(resp.GetResponseStream(), Encoding.ASCII);  
  
```  
  
```vb  
Dim sr As StreamReader  
sr = New StreamReader(resp.GetResponseStream(), Encoding.ASCII)  
```  
  
## Vedere anche  
 [Programmazione di rete in .NET Framework](../../../docs/framework/network-programming/index.md)   
 [Procedura: Richiedere una pagina Web e recuperare i risultati sotto forma di flusso](../../../docs/framework/network-programming/how-to-request-a-web-page-and-retrieve-the-results-as-a-stream.md)   
 [Procedura: Recuperare un oggetto WebResponse specifico del protocollo corrispondente a un oggetto WebRequest](../../../docs/framework/network-programming/how-to-retrieve-a-protocol-specific-webresponse-that-matches-a-webrequest.md)