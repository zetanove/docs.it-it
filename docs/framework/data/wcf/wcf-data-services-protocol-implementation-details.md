---
title: "Dettagli di implementazione del protocollo WCF Data Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 712d689b-fada-4cbb-bcdb-d65a3ef83b4c
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Dettagli di implementazione del protocollo WCF Data Services
## Dettagli di implementazione del protocollo OData  
 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] richiede che un servizio dati che implementa il protocollo fornisca un determinato set di funzionalità minimo.  Queste funzionalità sono descritte nei documenti del protocollo in termini che fanno riferimento ad azioni consigliate e necessarie. Le altre funzionalità facoltative vengono descritte in termini che fanno riferimento ad azioni ipotetiche. In questo argomento vengono descritte tali funzionalità facoltative che non sono attualmente implementate da [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  Per altre informazioni, vedere [Documentazione del protocollo OData](http://go.microsoft.com/fwlink/?LinkID=184554).  
  
### Supporto dell'opzione query $format  
 Il protocollo [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] supporta i feed JSON \(JavaScript Notation\) e Atom e [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] fornisce l'opzione query di sistema `$format` per consentire a un client di richiedere il formato del feed di risposta.  Questa opzione query di sistema, se supportata dal servizio dati, deve eseguire l'override del valore dell'intestazione Accept della richiesta.  [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] supporta la restituzione dei feed JSON e Atom.  Tuttavia, l'implementazione predefinita non supporta l'opzione query `$format` e usa solo il valore dell'intestazione Accept per determinare il formato della risposta.  In alcuni casi è necessario che il servizio dati supporti l'opzione query `$format`, ad esempio quando i client non possono impostare l'intestazione Accept.  Per supportare questi scenari, è necessario estendere il servizio dati per gestire questa opzione nell'URI.  È possibile aggiungere questa funzionalità al servizio dati scaricando il progetto di esempio [Supporto del formato controllato da JSONP e URL per ADO.NET Data Services](http://go.microsoft.com/fwlink/?LinkId=208228) dal sito Web della raccolta di codice MSDN e aggiungendolo al progetto del servizio dati.  Questo esempio rimuove l'opzione query `$format` e imposta l'intestazione Accept su `application/json`.  Quando si include il progetto di esempio aggiungendo `JSONPSupportBehaviorAttribute` alla classe del servizio dati, si consente al servizio di gestire l'opzione query `$format``$format=json`.  È necessario personalizzare ulteriormente questo progetto di esempio per gestire anche `$format=atom` o gli altri formati personalizzati.  
  
## Comportamenti di WCF Data Services  
 I comportamenti di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] seguenti non sono definiti in modo esplicito dal protocollo [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]:  
  
### Comportamento di ordinamento predefinito  
 Quando una richiesta di query inviata al servizio dati include un'opzione query di sistema `$top` o `$skip` e non include l'opzione query di sistema `$orderby`, il feed restituito viene ordinato in base alle proprietà chiave in ordine crescente,  poiché l'ordinamento è necessario per garantire il paging corretto dei risultati.  A tale scopo, il servizio dati aggiunge un'espressione di ordinamento alla query.  Questo comportamento si verifica anche quando viene abilitato il paging basato su server nel servizio dati.  Per altre informazioni, vedere [Configurazione del servizio dati](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md). Per controllare l'ordinamento del feed restituito, è necessario includere `$orderby` nell'URI di query.  
  
## Vedere anche  
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)