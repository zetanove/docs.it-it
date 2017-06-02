---
title: "Serializzazione binaria | Microsoft Docs"
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
  - "serializzazione binaria"
  - "serializzazione binaria, informazioni sulla serializzazione"
  - "deserializzazione"
  - "serializzazione, informazioni sulla serializzazione"
ms.assetid: 2b1ea3be-1152-4032-b2b3-07794054c405
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Serializzazione binaria
La serializzazione può essere definita come il processo di archiviazione dello stato di un oggetto su un supporto di archiviazione.Durante tale processo, i campi pubblici e privati dell'oggetto e il nome della classe, incluso l'assembly contenente la classe, vengono convertiti in un flusso di byte che viene scritto in un flusso di dati.Quando l'oggetto viene successivamente deserializzato, viene creato un clone esatto dell'oggetto originale.  
  
 Quando si implementa un meccanismo di serializzazione in un ambiente orientato agli oggetti, è necessario fare una serie di compromessi tra semplicità di utilizzo e flessibilità.Il processo può essere automatizzato in un ambito di grandi dimensioni, purché si disponga di controllo sufficiente sul processo.Ad esempio, possono verificarsi situazioni in cui non è sufficiente la semplice serializzazione binaria o potrebbe esserci una ragione specifica per decidere quali campi in una classe devono essere serializzati.Le seguenti sezioni esaminano l'affidabile meccanismo di serializzazione fornito con .NET Framework ed evidenziano una serie di importanti funzionalità che consentono di personalizzare il processo in base alle necessità.  
  
> [!NOTE]
>  Lo stato di un oggetto codificato UTF\-7 o UTF\-8 non viene mantenuto se le relative operazioni di serializzazione e deserializzazione vengono eseguite con versioni di .NET Framework diverse.  
  
## In questa sezione  
 [Concetti relativi alla serializzazione](../../../docs/framework/serialization/serialization-concepts.md)  
 Vengono illustrati due scenari in cui la serializzazione risulta utile: quando si conservano i dati da archiviare e quando si trasferiscono oggetti tra più domini dell'applicazione.  
  
 [Serializzazione di base](../../../docs/framework/serialization/basic-serialization.md)  
 Descrive come utilizzare i formattatori binari e SOAP per serializzare gli oggetti.  
  
 [Serializzazione selettiva](../../../docs/framework/serialization/selective-serialization.md)  
 Descrive come impedire la serializzazione di alcuni membri di una classe.  
  
 [Serializzazione personalizzata](../../../docs/framework/serialization/custom-serialization.md)  
 Descrive come personalizzare la serializzazione per una classe tramite l'utilizzo dell'interfaccia <xref:System.Runtime.Serialization.ISerializable>.  
  
 [Passaggi del processo di serializzazione](../../../docs/framework/serialization/steps-in-the-serialization-process.md)  
 Descrive il corso di azioni intraprese dalla serializzazione quando viene chiamato il metodo <xref:System.Runtime.Serialization.Formatter.Serialize%2A> su un formattatore.  
  
 [Serializzazione a tolleranza di versione](../../../docs/framework/serialization/version-tolerant-serialization.md)  
 Spiega come creare tipi serializzabili modificabili nel tempo evitando che le applicazioni generino eccezioni.  
  
 [Linee guida relative alla serializzazione](../../../docs/framework/serialization/serialization-guidelines.md)  
 Fornisce alcune linee guida generali che consentono di decidere quando serializzare un oggetto.  
  
## Riferimenti  
 <xref:System.Runtime.Serialization>  
 Contiene classi utilizzabili per la serializzazione e la deserializzazione di oggetti.  
  
## Sezioni correlate  
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)  
 Descrive il meccanismo della serializzazione XML incluso nel Common Language Runtime.  
  
 [Security and Serialization](../../../docs/framework/misc/security-and-serialization.md)  
 Descrive le linee guida per la creazione di codice protetto da seguire in caso di scrittura di codice che esegue la serializzazione.  
  
 [Remote Objects](http://msdn.microsoft.com/it-it/515686e6-0a8d-42f7-8188-73abede57c58)  
 Vengono descritti i diversi metodi di comunicazione disponibili in .NET Framework per le comunicazioni remote.  
  
 [XML Web Services Created Using ASP.NET and XML Web Service Clients](http://msdn.microsoft.com/it-it/1e64af78-d705-4384-b08d-591a45f4379c)  
 Fornisce gli argomenti che descrivono e spiegano come programmare i servizi Web XML creati tramite ASP.NET.