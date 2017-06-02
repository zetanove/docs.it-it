---
title: "Programmazione di protocolli di collegamento | Microsoft Docs"
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
  - "download di risorse Internet, protocolli di collegamento"
  - "WebRequest (classe), protocolli di collegamento"
  - "risposta a una richiesta Internet, protocolli di collegamento"
  - "WebResponse (classe), protocolli di collegamento"
  - "invio di dati, protocolli di collegamento"
  - "risorse di rete, protocolli di collegamento"
  - "Internet, protocolli di collegamento"
  - "programmazione di protocolli di collegamento"
  - "protocolli di collegamento, programmazione"
  - "richiesta di dati da Internet, protocolli di collegamento"
  - "ricezione di dati, protocolli di collegamento"
  - "collegamento, protocolli"
ms.assetid: 66ef8456-7576-4e97-8956-959b216373db
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# Programmazione di protocolli di collegamento
<xref:System.Net.WebRequest> le classi e astratti <xref:System.Net.WebResponse> forniscono la base per i protocolli innestabili.  Derivando le classi specifiche del protocollo da <xref:System.Net.WebRequest> e da <xref:System.Net.WebResponse>, un'applicazione può di richiedere dati da una risorsa Internet e leggere la risposta senza specificare il protocollo utilizzato.  
  
 Prima di poter creare <xref:System.Net.WebRequest>protocollo specifico, è necessario registrare il creare il metodo.  Utilizzare il metodo statico <xref:System.Net.WebRequest.RegisterPrefix%28System.String%2CSystem.Net.IWebRequestCreate%29><xref:System.Net.WebRequest> per registrare un discendente <xref:System.Net.WebRequest> per gestire un set di richieste a una combinazione specifica Internet, a una combinazione e un server, o una combinazione, in un server e un percorso.  
  
 Nella maggior parte dei casi sarà possibile inviare e ricevere i dati utilizzando i metodi e le proprietà <xref:System.Net.WebRequest> classe.  Tuttavia, se è necessario accedere alle proprietà specifiche del protocollo, è possibile eseguire su di essi un cast <xref:System.Net.WebRequest> a una specifica istanza della classe derivata.  
  
 Per sfruttare i protocolli innestabili, i discendenti <xref:System.Net.WebRequest> devono fornire una transazione predefinita di richiesta\-e\- risposta che non richiede le proprietà specifiche del protocollo di essere impostata.  Ad esempio, la classe <xref:System.Net.HttpWebRequest>, che implementa la classe <xref:System.Net.WebRequest> per HTTP, fornisce una richiesta `GET` per impostazione predefinita e restituisce <xref:System.Net.HttpWebResponse> che contiene il flusso restituito dal server Web.  
  
## Vedere anche  
 [Derivazione da WebRequest](../../../docs/framework/network-programming/deriving-from-webrequest.md)   
 [Derivazione da WebResponse](../../../docs/framework/network-programming/deriving-from-webresponse.md)   
 [Programmazione di rete in .NET Framework](../../../docs/framework/network-programming/index.md)   
 [Procedura: Eseguire il cast di tipo di un oggetto WebRequest per accedere a proprietà specifiche del protocollo](../../../docs/framework/network-programming/how-to-typecast-a-webrequest-to-access-protocol-specific-properties.md)