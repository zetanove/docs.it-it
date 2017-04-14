---
title: "Raggruppamento delle connessioni | Microsoft Docs"
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
  - "connessioni [.NET Framework], raggruppamento"
  - "WebRequest (classe), raggruppamento delle connessioni"
  - "risorse di rete, connessioni"
  - "pool di connessioni"
ms.assetid: 2ec502e8-4ba0-4c22-9410-f28eaf4eee63
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Raggruppamento delle connessioni
Il raggruppamento di connessione associa le richieste specifiche l'interno di una singola applicazione a un pool di connessioni definito.  Ciò può essere richiesta da un'applicazione di livello intermedio che si connette a un server di back\-end un nome di un utente e utilizza un protocollo di autenticazione che supporta la delega Kerberos, come, o da un'applicazione di livello intermedio che fornisce le proprie credenziali, come nell'esempio riportato di seguito.  Si supponga, ad esempio un utente, Joe, visita un sito Web interno per visualizzare le informazioni dei fogli paga.  Dopo autenticante Operazione, il server di applicazioni di livello intermedio utilizzano le credenziali dell'operazione per connettersi al server di back\-end per recuperare le informazioni dei fogli paga.  Successivamente, Susan visita il sito e richiede le informazioni dei fogli paga.  Poiché l'applicazione di livello intermedio già stata eseguita una connessione utilizzando le credenziali dell'operazione, il server di back\-end risponde alle informazioni dell'operazione.  Tuttavia, se l'applicazione assegna ogni richiesta inviata al server di back\-end a un gruppo di connessioni formato dal nome utente, ogni utente appartiene a un pool di connessioni separato e non è possibile condividere accidentalmente le informazioni di autenticazione con un altro utente.  
  
 Per assegnare una richiesta a un gruppo di connessioni specifico, è necessario assegnare un nome alla proprietà <xref:System.Net.WebRequest.ConnectionGroupName%2A> del <xref:System.Net.WebRequest> prima di effettuare la richiesta.  
  
## Vedere anche  
 [Gestione di connessioni](../../../docs/framework/network-programming/managing-connections.md)   
 [Procedura: Assegnare informazioni utente a connessioni di gruppo](../../../docs/framework/network-programming/how-to-assign-user-information-to-group-connections.md)