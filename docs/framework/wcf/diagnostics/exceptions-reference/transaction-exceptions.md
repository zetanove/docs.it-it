---
title: "Eccezioni di transazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1d27ed51-7eda-477f-9eca-94fa129f3e07
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Eccezioni di transazione
In questo argomento vengono elencate tutte le eccezioni generate dalla transazione [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  
  
## Elenco delle eccezioni  
  
|Codice sorgente|Stringa di risorsa|  
|---------------------|------------------------|  
|SFxCannotHaveDifferentTransactionProtocolsInOneBinding|Le informazioni sui criteri importate dai metadati specificano valori diversi per TransactionProtocol tra le operazioni.È supportato un solo TransactionProtocol per ogni endpoint.|  
|SFxTransactionAutoCompleteFalseAndInstanceContextMode|TransactionAutoComplete non può essere false, a meno che InstanceContextMode del servizio non sia PerSession.È stato trovato un errore nell'implementazione del contratto e dell'operazione specificati.|  
|SFxTransactionInvalidSetTransactionComplete|OperationContext.SetTransactionComplete può essere chiamato in un'operazione solo quando TransactionAutoComplete è impostato su false e TransactionScopeRequired è impostato su true.Questo scenario non è valido e la transazione corrente è stata terminata.|  
|TransactionFlowRequiredIssuedTokens|Per poter propagare una transazione, deve essere supportata anche la propagazione dei token rilasciati.|  
|TrustDriverVersionDoesNotSupportIssuedTokens|La versione Trust configurata non supporta i token rilasciati.Utilizzare WSTrustFeb2005 o superiore.|