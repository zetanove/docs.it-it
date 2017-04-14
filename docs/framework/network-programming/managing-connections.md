---
title: "Gestione di connessioni | Microsoft Docs"
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
  - "Internet, connessioni"
  - "HTTP, classi per la connessione"
  - "richiesta di dati da Internet, connessioni"
  - "invio di dati, connessioni"
  - "ricezione di dati, connessioni"
  - "ServicePoint (classe), informazioni"
  - "risposta a richiesta Internet, connessioni"
  - "connessioni [.NET Framework], classi"
  - "risorse di rete, connessioni"
  - "download delle risorse Internet, connessioni"
  - "ServicePointManager (classe), informazioni"
ms.assetid: 9b3d3de7-189f-4f7d-81ae-9c29c441aaaa
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Gestione di connessioni
Le applicazioni che utilizzano HTTP per la connessione alle risorse di dati possono utilizzare le classi <xref:System.Net.ServicePoint> e <xref:System.Net.ServicePointManager> di .NET Framework per gestire le connessioni Internet e per aiutarle per ottenere la dimensione e prestazioni ottimali.  
  
 La classe **ServicePoint** viene illustrata un'applicazione con un endpoint che l'applicazione possa connettersi per accedere alle risorse Internet.  Ogni **ServicePoint** contiene informazioni che consente di ottimizzare le connessioni a un server Internet condividendo le informazioni di ottimizzazione tra connessioni per migliorare le prestazioni.  
  
 Ogni **ServicePoint** è identificato da un Uniform Resource Identifier \(URI\) e viene suddivisa in categorie come frammenti dell'identificatore e host di schema URI.  Ad esempio, la stessa istanza **ServicePoint** fornisce le richieste a URI http:\/\/www.contoso.com\/index.htm e http:\/\/www.contoso.com\/news.htm?date\=today poiché hanno lo stesso identificatore di schema \(HTTP\) e frammenti host \(www.contoso.com\).  Se l'applicazione dispone già di una connessione persistente in www.contoso.com server, utilizza tale connessione per recuperare entrambe le richieste, evitanti dover creare due connessioni.  
  
 **ServicePointManager** è una classe statica che gestisce la creazione e l'eliminazione di istanze **ServicePoint**.  **ServicePointManager** crea **ServicePoint** quando l'applicazione richiede una risorsa Internet non è presente nella raccolta di istanze esistenti **ServicePoint**.  Le istanze di**ServicePoint** vengono eliminati quando hanno superato il tempo di inattività massimo o quando il numero di istanze esistenti **ServicePoint** supera il numero massimo di istanze **ServicePoint** per l'applicazione.  È possibile controllare sia il tempo di inattività massimo predefinito che il numero massimo di istanze **ServicePoint** impostando le proprietà <xref:System.Net.ServicePointManager.MaxServicePoints%2A> e <xref:System.Net.ServicePointManager.MaxServicePointIdleTime%2A> su **ServicePointManager**.  
  
 Il numero di connessioni tra un client e server può avere un impatto significativo sulla velocità effettiva dell'applicazione.  Per impostazione predefinita, un'applicazione mediante la classe <xref:System.Net.HttpWebRequest> utilizza il massimo due connessioni permanenti in un server specificato, ma è possibile impostare il numero massimo di connessioni in base all'applicazione.  
  
> [!NOTE]
>  I limiti di HTTP\/1.1 specifica il numero di connessioni da un'applicazione a due connessioni per server.  
  
 Il numero ottimale delle connessioni effettive dipende dalle condizioni in cui viene eseguita l'applicazione.  L'aumento del numero di connessioni disponibili per l'applicazione non può influire sulle prestazioni dell'applicazione.  Per determinare l'impatto di più connessioni, test delle prestazioni di esecuzione e modificando il numero di connessioni.  È possibile modificare il numero di connessioni utilizzati da un'applicazione modificando la proprietà statica <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> nella classe **ServicePointManager** all'inizializzazione dell'applicazione, come illustrato nell'esempio di codice.  
  
```csharp  
// Set the maximum number of connections per server to 4.  
ServicePointManager.DefaultConnectionLimit = 4;  
```  
  
```vb  
' Set the maximum number of connections per server to 4.  
ServicePointManager.DefaultConnectionLimit = 4  
```  
  
 Modificare la proprietà **ServicePointManager.DefaultConnectionLimit** non influisce sulle istanze precedentemente inizializzate **ServicePoint**.  Il codice seguente viene illustrato modificare il limite di connessione in **ServicePoint** esistente per http:\/\/www.contoso.com server al valore archiviato in `newLimit`.  
  
```csharp  
Uri uri = new Uri("http://www.contoso.com/");  
ServicePoint sp = ServicePointManager.FindServicePoint(uri);  
sp.ConnectionLimit = newLimit;  
```  
  
```vb  
Dim uri As New Uri("http://www.contoso.com/")  
Dim sp As ServicePoint = ServicePointManager.FindServicePoint(uri)  
sp.ConnectionLimit = newLimit  
```  
  
## Vedere anche  
 [Raggruppamento delle connessioni](../../../docs/framework/network-programming/connection-grouping.md)   
 [Uso di protocolli applicativi](../../../docs/framework/network-programming/using-application-protocols.md)