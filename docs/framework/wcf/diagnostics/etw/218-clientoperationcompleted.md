---
title: "218 - ClientOperationCompleted | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b069bced-7bb2-4e01-8227-e5dbda17af09
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 218 - ClientOperationCompleted
## Proprietà  
  
|||  
|-|-|  
|ID|218|  
|Parole chiave|Troubleshooting, ServiceModel|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene generato dai client al termine di un'operazione.Per le operazioni unidirezionali, si tratta del momento successivo all'invio di un messaggio.Per le operazioni request\-response, si tratta del momento successivo alla ricezione della risposta.  
  
## Messaggio  
 L'azione client '%1' associata al contratto '%2' è completa.Il messaggio è stato inviato a '%3'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Azione|xs:string|Intestazione dell'azione SOAP del messaggio in uscita.|  
|Nome contratto|`xs:string`|Nome del contratto.Esempio: ICalculator.|  
|Destinazione|`xs:string`|Indirizzo dell'endpoint servizio a cui è stato inviato il messaggio.|  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|