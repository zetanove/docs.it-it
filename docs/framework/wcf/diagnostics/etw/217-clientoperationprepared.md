---
title: "217 - ClientOperationPrepared | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad207f04-b038-4f33-95e9-27a361df8ecd
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 217 - ClientOperationPrepared
## Proprietà  
  
|||  
|-|-|  
|ID|217|  
|Parole chiave|Troubleshooting, ServiceModel|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene generato dai client prima che un'operazione venga inviata al servizio.  
  
## Messaggio  
 Esecuzione dell'azione client '%1' associata al contratto '%2'.Il messaggio verrà inviato a '%3'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Azione|`xs:string`|Intestazione dell'azione SOAP del messaggio in uscita.|  
|Nome contratto|`xs:string`|Nome del contratto.Esempio: ICalculator.|  
|Destinazione|`xs:string`|Indirizzo dell'endpoint servizio a cui viene inviato il messaggio.|  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|