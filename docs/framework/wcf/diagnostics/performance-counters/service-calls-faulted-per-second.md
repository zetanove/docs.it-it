---
title: "Servizio: chiamate non riuscite al secondo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 94247356-2b29-4b50-b639-91ca8c1cf3a9
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Servizio: chiamate non riuscite al secondo
Nome contatore: chiamate non riuscite al secondo  
  
## Descrizione  
 Numero di chiamate a questo servizio che hanno restituito errori in un secondo.  
  
 Si tratta di un contatore di prestazioni di tipo [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649), il cui valore viene calcolato utilizzando la formula seguente.  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)  
  
 Nelle applicazioni [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)], le informazioni sugli errori di elaborazione vengono comunicate dai metodi di servizio tramite messaggi di errore SOAP.Gli errori SOAP sono tipi di messaggio inclusi nei metadati per un'operazione del servizio e pertanto creano un contratto di errore che i client possono utilizzare per rendere l'esecuzione più affidabile o interattiva.Dato che gli errori SOAP sono espressi ai client in formato XML, sono estremamente interoperativi.  
  
## Vedere anche  
 [Specifica e gestione di errori in contratti e servizi](../../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)