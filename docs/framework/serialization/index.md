---
title: "Serializzazione | Microsoft Docs"
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
  - "oggetti, serializzazione"
  - "serializzazione"
  - "serializzazione di oggetti"
  - "serializzazione XML, definizione"
ms.assetid: 4d1111c0-9447-4231-a997-96a2b74b3453
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Serializzazione
La serializzazione è il processo di conversione dello stato di un oggetto in un form che può essere mantenuto o trasportato.Il complemento della serializzazione è la deserializzazione, che converte un flusso in un oggetto.Insieme, questi processi consentono di archiviare e trasferire i dati in modo semplice.  
  
 .NET Framework dispone di due tecnologie di serializzazione:  
  
-   La serializzazione binaria mantiene la fedeltà dei tipi, utile per il mantenimento dello stato di un oggetto tra chiamate diverse di un'applicazione.È possibile, ad esempio, condividere un oggetto tra diverse applicazioni serializzandolo negli Appunti.La serializzazione di un oggetto può essere effettuata in un flusso, in un disco, in memoria, in rete e così via..NET Remoting utilizza la serializzazione per passare oggetti "per valore" da un computer o dominio dell'applicazione a un altro.  
  
-   La serializzazione XML serializza solo i campi e le proprietà pubbliche e non mantiene la fedeltà dei tipi.Ciò risulta utile se si vuole fornire o utilizzare dati senza limitare l'applicazione che utilizza i dati.Poiché XML è uno standard aperto, questa rappresenta una scelta interessante ai fini della condivisione di dati attraverso il Web.Analogamente, SOAP è uno standard aperto che rappresenta una scelta altrettanto interessante.  
  
## In questa sezione  
 [Argomenti sulle procedure relative alla serializzazione](../../../docs/framework/serialization/serialization-how-to-topics.md)  
 Vengono riportati collegamenti alle procedure contenute in questa sezione.  
  
 [Serializzazione binaria](../../../docs/framework/serialization/binary-serialization.md)  
 Descrive il meccanismo della serializzazione binaria incluso nel Common Language Runtime.  
  
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)  
 Descrive il meccanismo della serializzazione XML e SOAP incluso nel Common Language Runtime.  
  
 [Strumenti per la serializzazione](../../../docs/framework/serialization/serialization-tools.md)  
 Questi strumenti consentono di sviluppare codice di serializzazione.  
  
 [Esempi di serializzazione](../../../docs/framework/serialization/serialization-samples.md)  
 Negli esempi viene illustrato come eseguire la serializzazione.  
  
## Riferimenti  
 <xref:System.Runtime.Serialization>  
 Contiene classi utilizzabili per la serializzazione e la deserializzazione di oggetti.  
  
 <xref:System.Xml.Serialization>  
 Contiene classi utilizzabili per la serializzazione di oggetti in documenti XML o in flussi.  
  
## Sezioni correlate  
 [Remote Objects](http://msdn.microsoft.com/it-it/515686e6-0a8d-42f7-8188-73abede57c58)  
 Vengono descritti i diversi metodi di comunicazione disponibili in .NET Framework per le comunicazioni remote.  
  
 [Advanced Development Technologies](http://msdn.microsoft.com/it-it/c4a7e341-f0c6-4df4-a74f-223387ac6e4e)  
 Sono riportati collegamenti per accedere a ulteriori informazioni sulle tecniche e sulle attività di sviluppo avanzate in .NET Framework.  
  
 [XML Web Services Created Using ASP.NET and XML Web Service Clients](http://msdn.microsoft.com/it-it/1e64af78-d705-4384-b08d-591a45f4379c)  
 Fornisce gli argomenti che descrivono e spiegano come programmare i servizi Web XML creati tramite ASP.NET.